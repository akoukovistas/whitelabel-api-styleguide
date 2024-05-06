---
Design
---

## General

*   There must be no difference on the design conventions between internal and external APIs.
*   Use a RESTful API style for HTTP APIs. SOAP, and other API design styles should not be used for public-facing services. GraphQL can be used, however it should be restricted to cases where it would be the best solution, e.g. a more complex search or filtering solution. 
*   All aspects of our API (requests, responses, paths, etc.) must be in US English, unless there’s an explicit product, or legal requirement.
*   An API should be more than a JSON and HTTP representation of the database. A single resource might include fields from different parts of the database, some that come from other microservices, and fields that are derived from calculations. Only include fields from the database that the developer-user will need.
*   Use intelligent defaults when creating a new resource. Consider if there’s business logic that would be best executed in the API layer.

## Naming

*   Your API resources should be nouns, not verbs. Instead of `/foobar/search?q={query}` use `/foobar/?q={query}`. By modeling things instead of behaviors, the API is more flexible. The world of behaviors a developer might want to do is infinite. Modeling based on the things a developer can interact with instead of the things they can do will keep your API clean and give developers more flexibility. 
*   Property names and resource names must be meaningful and human readable.
*   You must not use a property name that’s used elsewhere in the API unless the two properties are describing the exact same thing. This can exclude “name” and “ID” if they appear in the context of a strongly typed response. This helps developers with debugging and understanding the systems.
*   Use {camelCase/snake_case/kebab-case} as the standard.

## Paths

*   Our recommended path template is the following: `{url}/resourceName/{id}/subresourceName/{id}?queryKey={queryValue)` 
*   Avoid deeply nested resources such as /project/{id}/foo/{id}/bar/{id}/content/{id}. All resources should be restricted to 2 levels deep. This style increases complexity with no real benefit to us or the developer. It reduces flexibility for us to do things later. 
*   Subresources should only be added in cases where a subresource would not exist without the main resource. For example: A BlogPost can contain Ads, but Ads can be created and managed regardless of if they are part of a BlogPost. Ads should be accessible in the API via {url}/ads, rather than under {url}/blogposts/{id}/ads/{id}. All three paths are valid, but represent vastly different things.
*   If a subresource exists, all previous resources must also exist and be valid URIs. For example, if blogs/{id}/blogposts/{id} is a valid resource, then blogs/{id} and blogs/{id}/blogposts should also be one.

## Requests

*   If a resource ID is ambiguous because it could exist in more than one space, then consider using unambiguous IDs instead. Alternatively, use the query string to specify the resource, as in /blogpost/{id}?blogId={id}. This adds flexibility for future designs. For example, you might later wish to let a user retrieve a blog post that exists in any of several blogs using a URL like /blogposts/{id}?blogId={id}.{id2}
*   For similar reasons, avoid metadata in the resource URL. For example, instead of a request like POST /foo/bar/{id}, place the metadata in the resource body like POST /foo/{id} and using a body that includes “type”:“bar” in the JSON.
*   Do not use query strings to introduce functionality, especially if it’s a single-use operation. In the blog post example, if the payload is to be adjusted for let’s say Hubspot, it should be part of the body of the request rather than something like /blogposts/{id}?exportForHubspot=1.

## Responses

### Body

*   Always prefer to respond with objects over specific data types. For instance, if we had an endpoint that returns potatoes, wrap it in a JSON object inside a relevant field. For example { potatoes: \[ { id: "id1" }, { id: "id2" } ] }. That way, we can have stronger response types (in this example, ID is 100% referring to a potato ID and the objects are potatoes) and in future iterations we can introduce more data and metadata without breaking existing integrations.
*   Response content types must not change regardless of if an error occurred or if the response contains a singular item or a collection of items. For example, for a route that returns a BlogPost (blogposts/{id}) should respond with a JSON Object with the BlogPost data on a successful request, but should respond with a JSON Object containing the error information if an error occurred.

### Pagination

*   All routes returning a collection of items need to be paginated.

*   All routes returning a collection of items must be implementing cursor-based pagination.

*   Collection responses must include a previousPageToken and nextPageToken in the response, even if there is only one page of results. If there is no previous or next page, the relevant Token must be set to null.

*   Example response of a paginated resource collection:


        {
          "items": [
            {
              "...": "...",
              ...
            }
          ],
          "previousPageToken": "string",
          "currentPageToken": "string",
          "nextPageToken": "string",
        }

### Filtering

*   Routes returning a collection of items need to have a default filter set for the maximum number of items per page. This should be modifiable by the user in most cases, up to a maximum number of records set by us. For example, a BlogPosts route might be returning 20 records by default and a user can use an itemsPerPage key in the query string to modify it, up to a 200 records per page we have set as the ultimate maximum.

## Verbs and us: why and how to avoid them (or how to peacefully coexist with them)

As with many things affecting the human psyche, the answer to why we do not want to be using verbs with our REST APIs is complex and multi-faceted. It dips into linguistics, semantics, technical and designs reasons. As such we are presenting a brief collection of reasons why using verbs can harm your API and afterwards we'll talk about things which might help with your design decisions.

### 13 Reasons why (actually about 8)

*   Users already interact with your REST API via a full CRUD set of standard HTTP verbs (POST/GET/DELETE...). It makes sense to be doing CRUD operations on nouns, not verbs.

*   REST isn't "RPC over HTTP" and you shouldn't think of your resources like function calls. REST is a representation of objects, not the actions those objects do.

*   There are some very important architectural decisions we should be considering:

    *   If a user does a POST to a URL, they should also be able to do a GET to that URL to receive a list of resources of that type.
    *   If an action does not cause a CRUD operation on a resource, how do I check that the action worked? If it DOES do a CRUD operation, why did I need a verb?
    *   The idempotency of HTTP verbs is well documented and understood. GET, DELETE, PUT can be called repeatedly and always have the same result. POST will create a new result every time is called. How would your custom verbs operate? How does the user know?
    *   The average user of your API, internal or external is not going to spend as much time thinking about or working with your API as you do. Routes and interactions need to be intuitive and prevent the user from failing.

*   A lot of experts on REST design, do in fact account for a "command" verb. However, they do stress that it must be used sparingly and it must always act on the preceding resource.

*   The need to use verbs usually crops up in more complex applications/operations. It should be a sign that you need to consider your solution design carefully. Adding a verb can be the easy solution which becomes a future problem.

*   Verbs are not scalable. Especially when everyone is able to quickly introduce a new verb endpoint. Let's use two examples to showcase this: a BlogPosts and an Agents resource.

    *   BlogPosts: a simple GET on /BlogPosts is not powerful enough to return all the BlogPosts in the format I would need them. I need more complex functionality to manage them via the API that matches the front end. Let's investigate some endpoints:


        *   GET /blogposts/get-blogposts-by-filter
        *   POST /blogposts/delete-by-filter
        *   GET /blogposts/get-unassigned-blogposts
        *   GET /blogposts/{id}/export-for-hubspot
        *   POST /blogposts/import-from-shopify
        *   DELETE /blogposts/remove-and-reindex
        *   GET /blogposts/reindex
        *   GET /blogposts/get-by-user
        *   POST /blogposts/assign-to-user
        *   POST /blogposts/assign-to-blog
        *   POST /blogposts/tag-all
        *   POST /blogposts/untag
        *   POST /blogposts/{id}/remove-tags
        *   and so on

*   [The set of supported HTTP methods](https://www.iana.org/assignments/http-methods/http-methods.xhtml#methods) is growing. There's going to be more verbs to play around with.

*   **In conclusion: It is not completely wrong to use verbs in your endpoints, but you probably don’t need them.**

***

For any points not explicitly covered in this guide, or our design philosophy, the open API standards can be utilized to make a decision (<https://oai.github.io/Documentation/best-practices.html>).
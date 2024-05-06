---
Common Feedback Points
---

## No verbs or actions in REST API paths

This is already covered in the [relevant section]({% link api-style-guide/design.md %}#verbs-and-us-why-and-how-to-avoid-them-or-how-to-peacefully-coexist-with-them) of the API style guide, but as a short summary:

REST APIs should expose resources, not actions. The preferred way to specify actions in a REST API is through HTTP methods, such as GET, POST, PUT, DELETE, etc. These methods should be used to perform operations on the resources specified in the resource path.

The structure of the API should be based on the resources it exposes, rather than the specific functions it performs.

Consider the following:

1.  Resource-oriented paths are more intuitive and easier to understand. They clearly indicate the type of resource being accessed, which can make it easier for developers to understand and use the API.
2.  Resource-oriented paths are more flexible and scalable. If an API's path structure is based on the functions it performs, it can be inflexible and difficult to change or extend. On the other hand, if the path structure is based on resources, it can be more flexible and easier to evolve over time.
3.  Resource-oriented paths are more consistent with RESTful principles. One of the core principles of REST is that it should be resource-oriented. By basing the path structure on resources rather than functions, it is easier to design an API that adheres to this principle.

Overall, resource-oriented paths tend to be more intuitive, flexible, and consistent with RESTful principles than functionality-oriented paths. As a result, they are generally considered a better choice when designing a REST API. If you have to use verbs, we have a preferred method to do so (also covered in the style guide).

## The paths are too lengthy or deeply-nested

There's a few reasons why we want to avoid lengthy paths:

1.  They can be hard to read and understand. Long, deeply-nested paths can be difficult for developers to read and understand, especially if there are a lot of levels of nesting. This can make it harder to use the API effectively.
2.  They can be inflexible. Deeply-nested paths can be inflexible and difficult to change or extend. If the structure of the API needs to be modified, it can be difficult to do so if the paths are deeply nested.
3.  They make bulk operations on resources more difficult. Let's take the following as an example: each TestCase can include a bunch of Modules. If the only way to access Modules is through `potato.com/api/v1/{projectId}/testCases/{testCaseId}/modules`, doing any bulk operations across modules would be very difficult and messy.

## No, or not cursor-based pagination

Cursor-based pagination can be more efficient and user-friendly than other types of pagination, particularly for large result sets.

Some of the key reasons we want to use it as a standard:

1.  It is more efficient. With cursor-based pagination, the API only needs to return a single cursor value, rather than the entire result set. This can be more efficient, particularly for large result sets, because it reduces the amount of data that needs to be transferred.
2.  It allows users to bookmark results. Cursor-based pagination allows users to bookmark a particular position in the result set and return to it later. This can be useful if a user wants to keep track of their progress or return to a specific point in the results.
3.  It is more flexible. Cursor-based pagination allows users to move forward and backward through the result set, rather than being limited to a fixed set of pages. This can be more flexible and allow users to more easily navigate through the results.
4.  It is more consistent. The results maintain their ordering even after resources are added or removed while the lookup operation is ongoing.

Review our pagination standards [here]({% link api-style-guide/design.md %}#pagination).

## Responses must be objects

In REST APIs, it is generally considered a best practice to always return objects in responses, rather than returning other types of data such as strings, numbers, or arrays. This is because objects provide a more structured and self-describing way to represent data, which can make it easier for clients to parse and understand the responses.

Specifically:

1.  Objects provide a clear structure. By using objects, you can clearly define the structure of the data being returned, including the names and types of each field. This can make it easier for clients to parse and understand the responses.
2.  Objects can include metadata. Objects can include additional fields that provide metadata about the data being returned. This can include information such as the total number of results, the current page, etc.
3.  Objects are easier to extend. If you need to add additional fields to the responses in the future, it is generally easier to do so with objects than with other types of data. This can help to make the API more flexible and easier to evolve over time.
---
How to use verbs & actions in your REST API design.
---

While we should be avoiding relying on custom verbs and actions in our REST APIs, we also make specialized products that might require the use of verbs & actions for the sake of simplicity and usability. As such, we have a preferred method to do this.

**tl;dr:** follow the Google custom methods <https://cloud.google.com/apis/design/custom_methods>

In detail:

*   Custom methods **should** use HTTP `POST` verb since it has the most flexible semantics, except for methods serving as an alternative get or list which **may** use `GET` when possible.
*   Custom methods **should not** use HTTP `PATCH`, but **may** use other HTTP verbs. In such cases, the methods **must** follow the standard [HTTP semantics](https://tools.ietf.org/html/rfc2616#section-9) for that verb.
*   Notably, custom methods using HTTP `GET` **must** be idempotent and have no side effects. For example custom methods that implement special views on the resource **should** use HTTP `GET`.
*   The URL path **must** end with a suffix consisting of a colon followed by the *custom verb*.
*   Before you start implementing routes with custom verbs you **must **decide on the vocabulary to be used. **Avoid unnecessary synonyms.**
*   You **must** ensure that the same verbs are used consistently across your service and ideally have a similar function to other {Company Name} products.
*   You **should** create a glossary with all your custom verbs with descriptions on where they should be used.

Example of a glossary of custom verbs (please note, these are just an example, you don't have to follow this specific design):

`:start`

*   Starts an operation on a resource.
*   Can be synchronous, or asynchronous.
*   The operation must reach an end state.

`:activate`

*   Changes the state of a resource and makes it available for interaction/consumption.
*   Must happen immediately or within a short amount of time.

`:stop`

*   Immediately stops the current operation.
*   Cannot be resumed.

`:pause`

*   Immediately stops the current operation.
*   Can be resumed.

`:cancel`

*   Immediately stops the current operation.
*   Cannot be resumed.
*   Clears all operational artifacts generated up to that point.

`:clone`

*   Creates a duplicate of the resource under a different ID.
*   Maintains any associations to other resources the original resource has.

Based on the words above, any time an operation that fits the description of let's say "`cancel`" **must** be using :cancel as its custom action verb and not :abort, :dismiss, :cancelRun, :cancelTest, and so on.

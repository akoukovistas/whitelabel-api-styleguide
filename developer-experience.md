---
Developer Experience
---


## General

*   API design has a lot to do with a good developer experience. Consistency within the API and across APIs is important. So is consistency in your output. Think of it this way, if you decide to return a numeric resource "cost" as a string, then all occurrences of this "cost" must also be strings.
*   All responses, positive or negative, must provide value to the API consumer. We must be aiming for something more than simply a 200 status code with an empty body for a successful operation or simply returning "an error has occurred, please try again" for every error. Provide context for what has gone wrong, or what has happened as a result of the users API request.
*   Responses should be for a user to successfully complete the intended action and continue operating within our product. For example, if a user successfully triggers an upload, return the upload ID so they can use it for further requests. If a user queries a blog post, return all the data required to describe a blog post as a model.


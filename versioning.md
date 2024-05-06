---
Versioning
---

## Version format

*   API version numbers must be limited to major versions only. Semver is not needed here. Prefix with a ‘v’, e.g., v1, v2, v3.
*   API version numbers do not have to match the product versions.

## Setting a version

*   A user can select a specific version via a variable on the path of the endpoint.

## Supporting multiple versions

*   If a user does not specify a version, we have two options:

    *   Return the latest version of the API,
    *   Respond with an error informing the user that they need to specify and API version and ideally containing a list of our currently supported API versions.

*   We strongly suggest going with the second option and responding with an error if the version is omitted, unless you are building an endpoint that wouldn't get integrated into someone's system, or if the format of the response would have little to no impact. For example, an analytics endpoint that someone would manually query and simply save the response into a CSV as it is.

*   API versions should only be incremented when a breaking change is introduced. \[Need to decide on the definition of a “Breaking Change”]

*   Each API should have a migration strategy from the legacy to the unified APIs.

*   Each API needs its own long term support plan.

    *   It should probably be decoupled from the LTS version of the product.
    *   APIs can last longer than the product itself.
    *   API support terms can be quite different to the product support term.
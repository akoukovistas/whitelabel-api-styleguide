---
Authentication
---


## General

*   Customers should have access to all the services of a product they are entitled to without having to authenticate multiple times.

## Types Supported

*   We are supporting OAuth 2.0 and OIDC (OpenID Connect) only.

## Methods Supported

*   We also should be able to support non-header authentication. These can help citizen-developers, older clients, and clients with unsophisticated HTTP stacks. The token MUST be treated as a secret and be filtered away from any logs and other forms of output. Examples: ?bearer={token}, basic auth with user:bearer pass:token.

## Scopes

*   We need to make use of scopes that grant only the access required. Once a broad scope has been granted, it is difficult to revert into a more restrictive one.
*   Scopes need to be namespaced. This is to be based on the access granted and not on a product basis on i.e., foo:read rather than productName:read. This will also allow us to share scope namespaces between products.
*   Scope descriptions need to be well-written. These will be visible to the end-users. Scopes are used to decide about data access and users will have to decide to grant access based on these descriptions. Bad example: “Give the application access to your account data.” Good example: “Allow this application to see your name, username, and email address only. The application cannot see your password, birthdate, or location.
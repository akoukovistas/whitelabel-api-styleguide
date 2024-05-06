---
Errors
---

## General

*   Appropriate HTTP codes should be used in the responses.
*   Provide a human readable error in the response. For example: HTTP 403 {“error”:”scope mismatch”, “message”:”The scope for this token does not grant write access to the resource”}
*   Treat catch-all error responses as the exception rather than a generic safety net. If something triggers a catch-all response, it needs to be logged as a bug and further investigated and handled.
*   50X errors must be treated as severe bugs.

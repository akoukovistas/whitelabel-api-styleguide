---
Security
---

## General

*   These must be always followed.
*   Info returned for troubleshooting needs to be balanced against info exposure. If something is sensitive info, for instance a tenant name, return a 404 instead of a 403 if the request is not authorized to access it.
*   No security through obscurity. If a specific user group shouldn’t be accessing an endpoint or API, they shouldn’t have access to it at all.

## API Responses

*   Do not include any sensitive data in responses (unless that's the intended functionality of the route - like retrieving a client secret). Examples of things that must be avoided: “Resource not authorized for user: TenantName token: abcd12345”, “Success! A new user has been added. ID: 123, Name: John Smith, Address: Potato Avenue 12345, Company: {Company Name}, Phone:1234556677”, "You have successfully changed your password to potato123"

---
Documentation
---

All APIs must be producing an up to date (3.0 or newer at the time of writing) OpenAPI compliant json reference file (swagger.json).

## Types of Documentation

There are a few types of documentation we should support:

### Authentication

*   Always document how a user can get access to the API and all the ways they can Authenticate.

### Quickstart

*   Can be as simple as an overview or ReadMe with examples. It needs to be focused on what the API does and how.

### Tutorials

*   These are aimed to teach dev users how to do something. Usually, it’s a longer example involving multiple tasks and API calls.

### How-To Guides

*   Step-by-step guidance for how to complete a specific task. It can be as simple as guiding a user through making one API call, or can be a more involved example, guiding a user using multiple API endpoints working together.

### API Reference Guide

*   OpenAPI json
*   One unified front-end portal rendering the API reference (Swagger UI, ReDoc, Slate Docs, etc). Ideally this must be published through our chosen API documentation tool.
*   Postman Collection

### Examples of Fail States

*   This can exist as part of the ReadMe, as an FAQ, or a Troubleshooting guide.

*   Can Include detailed examples of fail states.

*   Think of scenarios such as:

    *   What happens when a user goes over their allocated limit and makes one additional call to the API
    *   What if a user starts a mass-delete process by mistake? Can they cancel? Are there any guard rails? Can the data be recovered?

### Simulations and Tests

*   Can be represented as a JSON file.
*   It shows that we are using our own products, which can act as an additional trust signal and it can also assist in customers adopting more of our products.
*   Customers, other internal devs and integrators can make use of these to test, learn and integrate APIs without affecting real data and processes independently from their usage quotas.
*   Contract tests can assist in debugging for users of the API. Let's say something breaks, they can check against our contract to determine if it's their integration or our API that's the issue.
*   We can leverage simulations and tests to prepare our API users for the release of a new version, or during the deprecation of a previous one.

Minimum Documentation Required

As a minimum we expect an OpenAPI Reference file and Authentication instructions for every API we are publishing. These should be published and available to both internal developers and customers of the product.

Further reading

<https://diataxis.fr/>
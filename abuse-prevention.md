---
Abuse Prevention
---

## Limits

*   All APIs need be built with limits and filters in place. Outside of any requirements set by the business, we need to have hard limits in place for all APIs. This can be decided on a product basis based on the functionality of the API. For example, only allow up to 10k executions per day, 60k queries and 300 uploads

## Caching

*   All responses must include the appropriate cache-control headers. Even routes that should be returning “live” data, should have at least a few seconds of caching, in case of multiple duplicate requests. 

## API Gateway

*   All our APIs must make use of an API gateway. Further details with regards to the vendor, usage and configuration will be published in future versions of the guide and other relevant material. 
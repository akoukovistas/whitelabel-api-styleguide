---
API Style Guide
nav_API Style Guide
navigation_weight: 0
---

This is the Style Guide for APIs at {Company Name}. All {Company Name} HTTP APIs should strive to match this style guide. Currently the guide covers REST-like HTTP APIs, but principles of it can be applied on a wider scope.

***

## Chapters
* TOC
{:toc}
---

## The Vision

We ship many different APIs as part of our products. We should strive for consistency so we can create a uniform experience for both our customers and our own teams. We want to enable fellow developers to easily understand, adopt and adapt our APIs.

We create great products, and we want engineers to adopt them and make them integral parts of their systems. Our APIs themselves are part of our products and should not be treated as a feature or something extra. It is likely that developers will only interact with our products via our APIs and documentation.

## The principles

Our API style should be based on a few core principles.

Our APIs should be designed to be:

•    **Predictable**: APIs should behave in an expected way. Parameters & paths must be descriptive of the route’s function.\
•    **Accessible**: The requirements to access and use our APIs should be clear. Any responses, including errors, should be specific and clear.\
•    **Reliable**: Prevent users from reaching fail states. Handle errors gracefully.\
•    **Consistent**: APIs should follow the same route structure rules, maintain a consistent naming scheme across products, return data in a standard format. Data and functions exposed should be as uniform as possible across all products.

## Our Philosophy

•    **APIs are forever**. Yes you can version them, but deprecating the old API is painful for everyone involved and should be avoided. By getting it right before anyone uses it, we save everyone a lot of headaches. \
•    **There’s no such thing as a private API**, only ones we haven’t decided to publish yet. Designing every API as if it’s public helps with internal developer experience, saves re-work down the road, and encourages robust APIs. \
•    **A product has one API**, not one API per component, microservice, or product team. Implementation details like our service architecture shouldn’t affect how we design a product’s API. \
•    **An API design isn’t just the request and response bodies**. It’s the URL structure, The authentication scheme. The pagination strategy. Rate limits. Error handling. 

## The Reality

It is unlikely we’ll get everything right the first time. We need to be able to change and update our APIs without a massive amount of overhead or risk for us and our customers.

There are a few key objectives we are trying to achieve with these standards:\
•    Create a consistent language between products.\
•    Assist product teams with design decisions.\
•    Be able to onboard new products and teams to the “{Company Name} way.”\
•    Enable cross-product cooperation.\
•    Improve maintainability.\
•    Reduce “toil” tasks for the product teams.\
•    Increase transparency between teams.\
•    Promote our products as a source of trust for our developer customers.

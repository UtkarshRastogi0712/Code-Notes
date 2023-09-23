REST API stands for __Representational State Transfer Application Programming Interface__.
It is an architecture style used to designed web applications and services that adheres to a set of constraints or principles. It is not a protocol, merely a set of guidelines for building scalable, stateless APIs.

### Key principles of REST APIs:
- __Statelessness__ : Each HTTP request is independent and can process the request without reliance on any previous request or session stored on the server. Each HTTP request must contain all the information necessary to process it.
- __Resource__ : Every entity (_object, service, data etc._) in a REST API is a resource and can be identified by a unique URI (_Uniform Resource Identifier_)
- __Uniform Interface__ : All REST APIs should have a uniform and consistent interface across all the URIs by employing [HTTP methods headers and status codes](HTTP%20cheatsheet) for operations on resources.
- __Representation__ : Resources can be represented in multiple forms such as XML, JSON, HTML etc. as specified by the client in the _ACCEPT header_.
- __Idempotence__ : HTTP methods are idempotent meaning performing the same operation several times results in the same output/response as if they were performed once. This ensures safety in cases of network failure and multiple requests.
- __Layered__ : REST APIs allow clients to communicate directly with the server without knowing if they are going through an intermediary such as a proxy or a cache. This allows for a scalable network architecture.
- __Security__ : REST APIs should be designed with security in mind by including authentication methods such a OAuth2 or API Keys.
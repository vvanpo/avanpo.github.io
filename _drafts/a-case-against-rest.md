---
title: "A Case Against REST"
post_author:
    name: "Victor van Poppelen"
    link: "https://github.com/vvanpo"
categories: [REST, RPC, Network-based software architecture]
---

1.1 REST is the architecture of the Web

The term <abbr title="Representational State Transfer">REST</abbr> originates from Roy Fielding's dissertation[^1] on network-based software architecture, where it is used to describe an architectural style for distributed hypermedia. Fielding's research into REST influenced his development of pivotal Internet standards---namely <abbr title="Hypertext Transfer Protocol">HTTP</abbr>[^2] and <abbr title="Uniform Resource Identifier">URI</abbr>[^3]---that established the technologies underpinning the Web.

1.2 The Web is successful largely due to the interface uniformity required by REST, and hypermedia is a core part of the Web's interface

1.3 Hypermedia is uniquely suited to how humans interact with information, but difficult for machines

## Hypermedia-less applications lose the control interface uniformity inherent in hyperlinks

2.1 Tight coupling of the control interface means an application surrenders interoperability

2.2 The interface generality constraint of REST forces applications to have coarse-grained data transfer, weakly-defined types, and restricts operations to CRUD

2.3 REST's uniformity is intuitive and protects API designs from becoming too complicated, but attempts to do anything out of the ordinary results in convoluted methods of skirting the constraints

## The current state of REST

3.1 No one implements HATEOAS, and that means that what almost everyone considers "REST" is really just <abbr title="Remote Procedural Call">RPC</abbr> in disguise

3.2 JSON does not have primitives for hyperlinks, so further standardization is needed to implement HATEOAS (e.g. [JSON:API](https://jsonapi.org/format/))

3.3 OpenAPI and other resource description standards are the antithesis of REST, as they necessitate the client to have thorough knowledge of the API before any interactions take place

## Abstractions are universal

4.1 Object, component, module, entity, resource, element, are all vague terms variously used to signify abstraction, and are conceptually equivalent. URIs can be used to identify abstraction without needing to adhere to other REST constraints

4.2 You can take advantage of HTTP and its capability for transparent use of Web infrastructure (caching, load balancers, proxies, firewalls) without also restricting your application to CRUD

4.3 Strongly typed message formats (e.g. gRPC) improve upon media types and don't require coarse-grained data transfer



### Notes

The constraints characterizing REST were carefully chosen to meet the demands of a worldwide distributed hypermedia system. The Web needs to facilitate the identification and access of information in an unrestricted and universal manner. As such, a differentiating constraint of REST is how it prescribes interface uniformity. REST introduces the concept of a _resource_, which is an abstract mapping to a set of entities. A resource is defined by the semantics of this mapping, rather than the entities themselves (which can change with time). Identifying information as resources rather than concrete representations allows for longevity of references. The Web performs resource identification using a standardized format for hyperlink references, called URI.

The analysis of architectural properties required by the Web did not consider whether they would be suitable for non-hypermedia-based applications. Indeed, an application not centered on hypermedia as its primary control mechanism cannot adhere to all of REST's constraints. Such an application loses some interface generality, as the well-defined semantics of state transition using links is no longer available.

- Hypermedia incorporates control information with presentation, necessitating coarse-grained data transfer.

- Resource representations heed generality via pre-defined data formats, called media types[^4].

// - Concrete examples of how interface generality is implemented in the Web include the standardizations of resource reference formats (URI), hypermedia data formats (<abbr title="Hypertext Markup Language">HTML</abbr>), resource manipulation (standard HTTP methods), and HTTP headers that facilitate content negotiation, cache control, and other resource or representation metadata.

    - Resource collections are conceptually similar to OOP classes, or at least class constructors (since you POST to a collection in order to create a resource)
      - More specifically you could argue that media types == classes and resource collections == constructors, but no one ever defines media types (again skirting REST fundamentals) so it's not a super important distinction to make
    - A resource is analogous to an object in OOP parlance
    - HTTP verbs are just a restricted set of object methods
      - "REST" has been successful probably because it restricts APIs to a few simple and consistent operations (as HTTP verbs are just CRUD), and making large deviations from these standard behaviours requires encoding behavioural descriptions within parameters, which is generally discouraged and considered bad design
    - Status codes cover the bare minimum of error states, and any reasonably complex API exposes their own error codes on top of status codes, leading to redundancy and general messiness
    - If you look at HTTP APIs in the same way that you look at OOP APIs, there isn't any good reason to be scared of RPC, and the ability to declare whatever methods you like gives you more flexibililty
      - If you always structure your endpoints in the hierarchy of `<class>/<object>/<method>`, you're maintaining consistency in a similar way to how REST tries to force consistency.
      - gRPC and other strongly-typed protocols are waaay better than media types or half-assed service descriptions

## References

[^1]: [Architectural Styles and the Design of Network-based Software Architectures](https://roy.gbiv.com/pubs/dissertation/top.htm)
[^2]: [Hypertext Transfer Protocol -- HTTP/1.1](https://tools.ietf.org/html/rfc2616)
[^3]: [Uniform Resource Identifier (URI): Generic Syntax](https://tools.ietf.org/html/rfc3986)
[^4]: [Media Types - IANA](https://www.iana.org/assignments/media-types)

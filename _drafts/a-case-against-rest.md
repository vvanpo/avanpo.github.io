---
title: "A Case Against REST"
post_author:
    name: "Victor van Poppelen"
    link: "https://github.com/vvanpo"
categories: [REST, RPC, Network-based software architecture]
---

The term <abbr title="Representational State Transfer">REST</abbr> originates from Roy Fielding's dissertation[^1] on network-based software architecture, where it is used to describe an architectural style for hypermedia applications. Fielding's research into REST influenced his development of pivotal Internet standards---namely <abbr title="Hypertext Transfer Protocol">HTTP</abbr>[^2] and <abbr title="Uniform Resource Identifier">URI</abbr>[^3]---that established the technologies underpinning the Web.

The constraints characterizing REST were carefully chosen to meet the demands of a worldwide distributed hypermedia system, i.e. the Web. The analysis of architectural properties required for the Web did not consider whether they would be suitable for non-hypermedia-based applications. Indeed, an application not centred on hypermedia as its primary control mechanism cannot properly adhere to all of the constraints.

The differentiating constraint of REST is how it mandates interface uniformity. As hypermedia often couples control data with content presentation, client and server need to agree on data format together with operations for retrieval and manipulation. In practice this is achieved with media type specifications[^4] and standardized HTTP methods (`GET`, `POST`, `PUT`, and `DELETE`).

Concrete examples of how interface generality is implemented in the Web include the standardizations of resource reference formats (URI), hypermedia data formats (<abbr title="Hypertext Markup Language">HTML</abbr>), resource manipulation (standard HTTP methods), and HTTP headers that facilitate content negotiation, cache control, and other resource or representation metadata.

## What is <abbr title="Remote Procedural Call">RPC</abbr>?

#### Notes

  - No one implements HATEOAS, and that means that what almost everyone considers "REST" is really just RPC in disguise
    - The HTML representation format has primitives for hrefs, JSON does not
    - Resource collections are conceptually similar to OOP classes, or at least class constructors (since you POST to a collection in order to create a resource)
      - More specifically you could argue that media types == classes and resource collections == constructors, but no one ever defines media types (again skirting REST fundamentals) so it's not a super important distinction to make
    - A resource is analogous to an object in OOP parlance
      - Object, component, module, entity, resource, element, are all vague and generic terms variously used to signify encapsulation, and are conceptually equivalent
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

[Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content](https://httpwg.org/specs/rfc7231.html)
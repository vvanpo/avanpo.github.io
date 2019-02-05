---
title: "A Case for RPC"
post_author:
    name: "Victor van Poppelen"
    link: "https://github.com/vvanpo"
categories: [RPC, REST, API design]
---

## What is RPC?

## What is REST?


#### Notes

  - No one implements HATEOAS, and that means that what almost everyone considers "REST" is really just RPC in disguise
    - Resource collections are conceptually similar to OOP classes, or at least class constructors (since you POST to a collection in order to create a resource)
      - More specifically you could argue that media types == classes and resource collections == constructors, but no one ever defines media types (again skirting REST fundamentals) so it's not a super important distinction to make
    - A resource is analogous to an object in OOP parlance
    - HTTP verbs are just a restricted set of object methods
      - "REST" has been successful probably because it restricts APIs to simple and consistent operations (due to HTTP verbs just being CRUD), and making large changes to behaviour would need to be done through parameters, which is generally discouraged and considered bad design
    - Status codes cover the bare minimum of error states, and any reasonably complex API exposes their own error codes on top of status codes, leading to redundancy and general messiness
  - If you look at HTTP APIs in the same way that you look at OOP APIs, there isn't any good reason to be scared of RPC, and the ability to declare whatever methods you like gives you more flexibililty
    - If you always structure your endpoints in the hierarchy of `<class>/<object>/<method>`, you're maintaining consistency in a similar way to how REST tries to force consistency.
    - gRPC and other strongly-typed protocols are waaay better than media types or half-assed service descriptions

## References

[^1]: [Architectural Styles and the Design of Network-based Software Architectures](https://roy.gbiv.com/pubs/dissertation/top.htm)

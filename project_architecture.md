# Project architecture

Project architecture describes how we should consider software architecture design.

# Table of Contents

* [General knowledge](#general-knowledge)
* [Shared Code](#shared-code)
  * [Goals](#goals)
    * [More Productivity](#more-productivity)
    * [Easier Standardization](#easier-standardization)
  * [Pitfalls and Antipatterns](#pitfalls-and-antipatterns)
    * [Code Reuse Abuse](#code-reuse-abuse)
      * [Risks](#risks)
      * [Conclusion](#conclusion)

# General knowledge

We want to follow the clean architecture paradigm.

Good to be aware of:

- [SOLID](https://en.wikipedia.org/wiki/SOLID)
- [12 Factor App](https://www.12factor.net/)
- [Testing Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
- [Agile Manifesto](http://agilemanifesto.org/principles.html)

# Shared Code

We sometimes need to share code through internal components, libraries, frameworks...
It can be done because of different reasons, we try here to list them and mitigate this risky choice.

## Goals

### More Productivity

We want to improve our efficiency. When we bootstrap a service or add features, a lot of infrastructure code built on top of some low-level code - such as http requests as an example - must be done.

One goal of the shared code is then to be able to re-use some code components or get inspiration from.

### Easier Standardization

We want to standardize interaction with _Infrastucture Services_.

_Infrastructure Services_ handles service logging, monitoring, authentication/authorization...

Our suite of services should adopt common ways to interact with them such as implementing structured logging as an example.

One goal of this collection is to be able to abstract these interactions using _Interfaces_ such as Loggers, in order to be able to change our _Infrastucture Services_ without changing our services logics.

See [Infrastructure Conventions](conventions.md#infrastructure) section.

# Pitfalls and Antipatterns

### Code Reuse Abuse

#### Risks

    "Software reuse is more like an organ transplant than snapping together Lego blocks."

  _John D. Cook_

The more effort developers put into making code resuable the harder it is to use. Making code reusable involves adding additional options and decision points to accommodate the different uses. The more developers add hooks to enable reusability the more they harm the basic _usability_ of the code: The more resuable code is, the less usable it is.

In other words, ease of code use if ogten inversely proportional to how reusable that code is. When developers build code to be reusable, they must add features to accommodate the myriad ways developers will will eventually use the code. All that future-proofing makes it more difficult for developers to use the code for a single purpose.

#### Conclusion:

1. **templates components**: prefer duplication to coupling: reuse implies coupling, and our services architecture goal is to be decoupled.
2. **infrastructure components**: use directly this repository importing it as a package. We must ensure an upgrade on infrastructure services is handled orthogonally from services teams, transparently.

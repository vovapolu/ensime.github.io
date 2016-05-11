---
layout: page
order: 1
title: Scala Center Community Input
---

This document outlines some of the ENSIME maintainers' thoughts for the consideration of the Scala Center, impacting the entire Scala Community.

- TOC
{:toc}


# Dotty and IDEs

It is concerning that Dotty does not yet have a presentation compiler. Without a presentation compiler, it could mean the end of the road for both ENSIME and Scala IDE.

ENSIME and Scala IDE share several common backends including the `PresentationCompiler` and `scala-refactoring`. We committed to expand the collaboration through the recently awarded Google Summer of Code project on Source Code Preserving ASTs.

In contrast, IntelliJ IDEA provides Scala editing support via an independently developed type-aware parser. Although the GSoC could allow for collaboration, it is highly likely that IDEA will continue autonomously. IDEA's commercial backing allows for development on features that could see it become the only editor for Dotty.

We hope that Dotty will shortly provide a replacement for the interactive PresentationCompiler (and something like scalap for TASTY), addressing the shortcomings of the current presentation compiler. We are aware that the amount of effort required to do this is significant. Indeed, it is too much for the volunteers at ENSIME to take on. This initiative requires an experienced full time developer in EPFL / Scala Center, with close access to the Dotty team, in order to complete.


# Licensing

The Scala Contributor License Agreement (the "Scala CLA") is similar to the Apache CLA: effectively an exclusive Apache 2.0 License Agreement from contributor to EPFL.

The Apache 2.0 is a permissive Free / Libre Software license, recommended by the Free Software Foundation and held in high esteem by Corporates and small companies all over the globe. Importantly, the Apache 2.0 includes a "Grant of Patent License" and a patent retaliation clause, which nullifies any legal wranglings over patents between contributors and users of the project.

However, the Scala distribution is made available under the Scala License, a 3-Clause Simplified BSD License. Although a permissive Free / Libre software license, the Scala License does not provide any grant of patent. This is concerning because there is no guarantee to recipients of the scala compiler and standard libraries that they have the right to use the software without being liable to pay a patent royalty.

It would be consistent, and fair to contributors, for the Scala distribution to be made available under the terms of the Apache 2.0 License. We trust that the Apache 2.0 is a better reflection of EPFL's approach so far, so this is simply a formal commitment to continue doing the same thing!


# Simple Streaming Framework

TODO: Akka isn't typesafe, Streams are too heavyweight, Spark is a beast, Futures aren't powerful enough, we need something with a very limited scope like `clojure.async` in Scala.

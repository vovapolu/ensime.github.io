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

We hope that Dotty will shortly provide a replacement for the interactive `PresentationCompiler` (and something like `scalap` for TASTY), addressing the shortcomings of the current presentation compiler. We are aware that the amount of effort required to do this is significant. Indeed, it is too much for the volunteers at ENSIME to take on. This initiative requires an experienced full time developer in EPFL / Scala Center, with close access to the Dotty team, in order to complete.


# Licensing

The Scala Contributor License Agreement (the "Scala CLA") is similar to the Apache CLA: effectively an exclusive Apache 2.0 License Agreement from contributor to EPFL.

The Apache 2.0 is a permissive Free / Libre Software license, recommended by the Free Software Foundation and held in high esteem by Corporates and small companies all over the globe. Importantly, the Apache 2.0 includes a "Grant of Patent License" and a patent retaliation clause, which nullifies any legal wranglings over patents between contributors and users of the project.

However, the Scala distribution is made available under the Scala License, a 3-Clause Simplified BSD License. Although a permissive Free / Libre software license, the Scala License does not provide any grant of patent. This is concerning because there is no guarantee to recipients of the scala compiler and standard libraries that they have the right to use the software without being liable to pay a patent royalty.

It would be consistent, and fair to contributors, for the Scala distribution to be made available under the terms of the Apache 2.0 License. We trust that the Apache 2.0 is a better reflection of EPFL's approach so far, so this is simply a formal commitment to continue doing the same thing!


# Investment in current PresentationCompiler

The current `PresentationCompiler` is sadly lacking in the area of macro support and is unable to keep up with the many boilerplate removal macro libraries that are becoming more common. As an example, the presentation compiler cannot cope with the macros used in the `sbt` API.

The ENSIME authors have set up an exploratory project, with the goal of raising awareness of this limitation to macro authors: https://github.com/fommil/imaginary-friend A possible short term workaround may be that some macro authors provide "presentation compiler plugins" that act only in the earlier phases of the compile.

It would be in the benefit of all ENSIME and Scala IDE users if the Scala Center were to become involved in improving the support for macros in the presentation compiler. The first step could be to create a lightweight testing library that macro authors can use to test the behaviour of their macros in the presentation compiler. Once tests can be written, a standalone regression suite could be produced, allowing for improvements in the presentation compiler itself.


# Investment in SBT

The amount of work happening on SBT is very small compared to the number of organisations and free / libre contributors using it. The reason for the lack of community engagement is simple: the sbt codebase is notoriously complicated and beyond the grasp of most volunteers who would otherwise be able to dip in and out with a simple patch. To make a difference requires an experienced full time developer.

It is no secret that the Scala compiler is slow. An efficient incremental compiler is the low hanging fruit that could speed up the workflow for many developers. There are many avenues to explore, from improved I/O and caching to better management and persistence of the graph structure (perhaps between developers and continuous integration servers).

The independent work on incremental compilation that is being undertaken by IntelliJ is, unfortunately, independent. If IntelliJ were to use the sbt incremental compiler, all hands could be working on improving the same code base. It is therefore vital that the technical hurdles of using sbt's incremental compiler are overcome.

It would be in the benefit of all Scala developers if the Scala Center could provide the resource to help sbt and IntelliJ integrate with each other and for the incremental compiler itself to receive a lot more attention.

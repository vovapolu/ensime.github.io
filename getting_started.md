---
layout: page
order: 1
title: Getting Started
site_nav_entry: true # this is an entry in the main site nav
---

Fantastic, and welcome!

ENSIME has a JVM process that indexes your dependencies and understands your source code using [scalac](http://www.scala-lang.org/files/archive/nightly/docs/compiler/index.html#scala.tools.nsc.interactive.package) and [javac](https://docs.oracle.com/javase/8/docs/jdk/api/javac/tree/) Abstract Syntax Trees.

It is important to realise that ENSIME is not an IDE, it is just one tool in a toolbox, following the UNIX philosophy of [Do One Thing and Do It Well](https://en.wikipedia.org/wiki/Unix_philosophy#Do_One_Thing_and_Do_It_Well). ENSIME's *thing* is to understand your source code. You must also have:

1. a build tool to compile your project and a `.ensime` file describing your project layout. To generate this file, [see which build tools we support](/build_tools/).
2. a text editor that is supported. To install the appropriate plugin, [learn about which editors we support](/editors/).

If things don't work as you expected, please read the [Getting Help](/getting_help) guide before asking for help.

If you're a Scala beginner, our [Learning Scala](/learning_scala) section has some excellent resources for you, and will help you get set up with a basic project.


We are volunteers with our own priorities to improve ENSIME. Our approach to feature requests is "we will enthusiastically help you to implement or fix it". The ENSIME codebase is surprisingly easy to understand and you are invited to read our [Contributing Guide](/contributing) and jump in.

Whether or not you can help with direct contributions, [please consider sponsoring a developer](/sponsor).

All interactions in ENSIME are governed by the [Typelevel Code of Conduct](http://typelevel.org/conduct.html).

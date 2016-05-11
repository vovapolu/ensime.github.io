---
layout: page
order: 1
title: Google Summer of Code Project Ideas
---

- TOC
{:toc}


## Source Code Preserving AST

Scala refactoring support is currently limited because the compiler provides a typed Abstract Syntax Tree (AST) which does not preserve whitespace, comments or important syntactic features such as `for` comprehensions. Adding support for a so-called Concrete Syntax Tree (CST), preserving source code attributes, would overly complicate the compiler internals.

A complementary - source-code preserving - AST would enable ENSIME and Scala IDEs to implement and share type-aware refactorings, addressing a major complaint of the scala developer community.

Efforts such as [`scala.meta`](http://scalameta.org) have shown that it is extremely difficult to convert a typed AST into a source-code preserving AST. Instead of attempting full conversion, we propose to provide Lens-like objects that map a limited set of elements in a typed AST into their equivalent in the source code AST, enabling a wide range of type-aware refactorings to be written.

Several parsers already exist for the scala language, but each falls short of the requirements of this exercise. Nevertheless, they serve as a good launchpad and may avoid the need to write a parser from scratch: `scala.meta`, [scalariform](https://github.com/scala-ide/scalariform), [fastparse](https://github.com/lihaoyi/fastparse/tree/master/scalaparse/shared/src/main/scala/scalaparse), [parboiled2](https://github.com/sirthias/parboiled2/tree/release-2.1/scalaParser/src) and IntelliJ.

Mentored by @fommil and/or @rorygraves and/or @xeno-by


## The Graphpocalypse

Several key features are missing from ENSIME that are frequently requested by users: *find usages* and *show implementing classes*.

We could implement some of these features using the current indexing mechanism, but we propose a step change by using a graph database to store the full bytecode and Scala pickled structure of a codebase, including all of its dependencies.

In addition to trivialising the implementation of the above feature requests, this approach opens up possibilities of completely new kinds of live code analysis: dead code detection, complexity measures and connectivity visualisations (find how *this* code is called by *that* code).

Further details are available in [ticket #1133](https://github.com/ensime/ensime-server/issues/1133), including an early proof of concept to assess graph database choices and their performance characteristics.

Mentored by @fommil


## Support for Dotty

There is currently no tooling support for Dotty, the next generation scala language and compiler. This unfortunate situation will reduce the interest in dotty (in the short term) and make it difficult for dotty to replace scala 2.x (in the long term). Dotty will soon be written in an early version of dotty itself, which could result in development efforts slowing down.

Support for Dotty in ENSIME will give dotty contributors a productive development environment to explore and improve new language features and address performance concerns in the 2.x series of compilers.

We propose to create an abstraction around the `ClassfileDepickler` and `RichPresentationCompiler` components of ENSIME to interchangeably support both scalac and dotty. Dotty does not currently have an interactive compiler, so this project will also involve implementing functionality within the compiler itself.

It is expected that parts of this abstracted layer would be released as a separate library, increasing the collaboration between ENSIME, scala-ide and EPFL.

This project offers the student a unique opportunity to explore and contribute to the next generation scala compiler, helping to shape the future of the language itself.

Mentored by @rorygraves

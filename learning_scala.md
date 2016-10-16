---
layout: page
order: 15
title: Learning Scala
site_nav_entry: true # this is an entry in the main site nav
---

This guide assumes no prior knowledge of Scala and will get you set up to the point where you have Scala installed on your computer and can hack on a project.

## Learn

We strongly recommend reading [Programming in Scala (Odersky/Spoon/Venners)](http://www.artima.com/shop/programming_in_scala_3ed) to learn the language, followed by [Functional Programming in Scala by Chiusano/Bjarnason](https://www.manning.com/books/functional-programming-in-scala), aka "the red book".

TODO: when scalanator has its intro course, link to it from here as an alternative to reading the book

## Install

1. Scala runs on the [Java Virtual Machine (JVM)](https://en.wikipedia.org/wiki/Java_virtual_machine). Prefer free/libre [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK) to proprietary versions of Java. You should be able to install OpenJDK using your system package manager:
  * `sudo pacman -S openjdk8-src` ([ArchLinux](https://wiki.archlinux.org/index.php/java))
  * `sudo apt-get install openjdk-8-source` ([Debian](https://wiki.debian.org/Java/))
  * [Zulu Java](http://www.azul.com/downloads/zulu/) for all other systems
2. (Optional) If you anticipate using multiple versions of Java, install [jenv](http://jenv.be).
3. The Scala Build Tool (SBT) will install everything you need for a project (including Scala itself), as it manages transitive dependencies via `~/.ivy2`. Until sbt 0.13.13 is released, we recommend that you add the executable [`paulp/sbt-extras`](https://raw.githubusercontent.com/paulp/sbt-extras/master/sbt) shell script to your `PATH`. Windows users should use the [Lightbend sbt installer](http://www.scala-sbt.org/0.13/docs/Installing-sbt-on-Windows.html) and may need to [take additional steps](https://github.com/ensime/ensime.github.io/issues/40) in some circumstances.

## Exercises

If a volunteer would like to pad out the following, that'd be great. Until then, try [Daniel Spiewak's "Getting Started in Scala" guide](https://gist.github.com/djspiewak/cb72c41ac335a3a9b28b3307be04aa43)

1. checkout a basic tutorial project (maybe 99 problems, or 47 degrees)
2. start sbt and cheatsheet of basic commands
3. hello world in the editor without ensime
4. start ensime server
5. learning resources: scalanator, coursera

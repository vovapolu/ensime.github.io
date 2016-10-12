---
layout: page
order: 15
title: Learning Scala
site_nav_entry: true # this is an entry in the main site nav
---

This guide assumes no prior knowledge of Scala and will get you set up to the point where you have Scala installed on your computer and can run some basic tutorial projects.

## Install

1. Scala runs on the [Java Virtual Machine (JVM)](https://en.wikipedia.org/wiki/Java_virtual_machine). Prefer free/libre [OpenJDK](https://en.wikipedia.org/wiki/OpenJDK) over proprietary releases. You may be able to install OpenJDK with your system package manager (make sure to grab the source code, you'll find it useful later)
  * `sudo pacman -S openjdk8-src` ([ArchLinux](https://wiki.archlinux.org/index.php/java))
  * `sudo apt-get install openjdk-8-source` ([Debian](https://wiki.debian.org/Java/))
  * `sudo apt-get install openjdk-8-jdk` ([Ubuntu](https://help.ubuntu.com/community/Java))
  * [Zulu Java](http://www.azul.com/downloads/zulu/) for all other systems
2. (Optional) Many projects use [jenv](http://jenv.be) to manage the version of java that they use, you may wish to install it now.
3. The Scala Build Tool (SBT) will install everything else you will need for a project, as it manages transitive dependencies in the `~/.ivy2` folder. Until sbt 0.13.13 is released, we recommend that you add the executable [`paulp/sbt-extras`](https://raw.githubusercontent.com/paulp/sbt-extras/master/sbt) shell script to your `PATH`. Windows users should use the [Lightbend sbt installer](http://www.scala-sbt.org/0.13/docs/Installing-sbt-on-Windows.html) and may need to [take additional steps](https://github.com/ensime/ensime.github.io/issues/40) in some circumstances.

## Learn

We strongly recommend reading [Programming in Scala (Odersky/Spoon/Venners)](http://www.artima.com/shop/programming_in_scala_3ed) to learn the language, followed by [Functional Programming in Scala by Chiusano/Bjarnason](https://www.manning.com/books/functional-programming-in-scala), aka "the red book".

## Exercises

If a volunteer would like to pad out the following, that'd be great:

1. checkout a basic tutorial project (maybe 99 problems, or 47 degrees)
2. start sbt and cheatsheet of basic commands
3. hello world in the editor without ensime
4. start ensime server
5. learning resources: scalanator, coursera

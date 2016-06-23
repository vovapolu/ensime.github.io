---
layout: section
order: 4
title: Workflow
---

You need to generate an `.ensime` configuration for your project. See how to do this based on which [build tool](/build_tools/) you are using . You will need to do this again if you change your project dependencies.

Edit a Scala file in your project. This will start an ENSIME server. The first time you run for your project, you will probably need to run `:EnClasspath` in Vim to generate the classpath for ENSIME and launch the server.

You probably want to set your build tool to continuously compile so that ENSIME keeps up to date as you edit your files (e.g. `~compile` in sbt).

For additional practical information on ENSIME workflows, you can find some useful information on the [Emacs page](/editors/emacs/userguide).

---
layout: section
order: 4
title: Workflow
---

First generate an `.ensime` configuration for your project. See how to do this based on which [build tool](/build_tools/) you are using. You will need to do this again if you change your project dependencies.

Then, edit a Scala file in your project. You will be prompted to run `:EnInstall` if it's your first time using ENSIME with the Scala version of your project. This will install and launch the server, then you're ready to go. ensime-vim will shut down the server when you exit your Vim session.

You probably want to set your build tool to continuously compile so that ENSIME keeps up to date as you edit your files (e.g. `~compile` in sbt). You can also ask ENSIME to type-check as you work—check `:help ensime-cookbook` for one automated way of doing this if you find it acceptably fast on your projects.

For additional practical information on ENSIME workflows, you can find some useful information on the [Emacs page](/editors/emacs/userguide).

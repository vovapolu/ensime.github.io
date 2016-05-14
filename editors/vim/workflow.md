---
layout: section
order: 4
title: Workflow
---

You need to generate a .ensime for your project. See how to do this based on which  [build tool](/build_tools/) you are using . You will need to do this again if you change your project dependancies.

Edit a scala file in your project. This will start an ensime server. The first time you run for your project, you will probably need to run ```:EnClasspath``` in vim to generate the classpath for ensime and launch the server.

You probably want to put your build tool to conitnuously compile so that ensime keeps up to date as you edit your files (```~compile``` in sbt)

For information on practical ENSIME workflows, you can find some useful information on the [Emacs page](/editors/emacs/userguide)

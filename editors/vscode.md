---
layout: section
order: 7
title: VS Code
---

There are two ongoing efforts to provide an Ensime-based [Visual Studio Code](https://code.visualstudio.com/) plugin. Currently there's only one published [on the Marketplace](https://marketplace.visualstudio.com/items?itemName=dragos.scala-lsp).

## Scala LSP

This plugin takes the approach of providing a native [Language Server Protocol](https://github.com/Microsoft/language-server-protocol) implementation based on an (in-process) Ensime library. There is only minimal code written in Typescript to hook the language server into the plugin, and plans are to move that to Scala.js, so this should be a 100% Scala implementation.

Head over to the repo:

- https://github.com/dragos/dragos-vscode-scala

to help out!

## ensime-vcode

The approach is to take out the atom-based Ensime client and use it from VS Code. This means it uses the ensime wire protocol instead of the LSP, leading to much more Javascript/Typescript code in the client.

The [ensime-atom](https://gitter.im/ensime/ensime-atom) gitter room is probably the best place to start asking questions.

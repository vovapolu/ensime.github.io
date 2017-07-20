---
layout: section
order: 7
title: VS Code
---

There are two ongoing efforts to provide an Ensime-based [Visual Studio Code](https://code.visualstudio.com/) plugin. Currently there's only one published [on the Marketplace](https://marketplace.visualstudio.com/items?itemName=dragos.scala-lsp).

## Scala LSP

This plugin takes the approach of providing a native [Language Server Protocol](https://github.com/Microsoft/language-server-protocol) implementation based on an (in-process) Ensime library. There is only minimal code written in Typescript to hook the language server into the plugin, and plans are to move that to Scala.js, so this should be a 100% Scala implementation.

Head over to the repo:

- [https://github.com/dragos/dragos-vscode-scala](https://github.com/dragos/dragos-vscode-scala)

to help out!

## ensime-vscode

This plugin aims to reuse the Atom-based Ensime client code. The difference is that it uses the Ensime wire protocol instead of the LSP, at the expense of somewhat more Javascript/Typescript code in the client (which is shared between Atom and VS Code).

The [ensime-atom](https://gitter.im/ensime/ensime-atom) gitter room is probably the best place to start asking questions.

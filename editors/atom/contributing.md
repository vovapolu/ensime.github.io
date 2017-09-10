---
layout: section
order: 2
title: Contributing
---

## Working with the Atom ENSIME Source

The basic cycle for interactive hacking on Atom ENSIME is: checkout the project (or a fork), install the package from your fork. Then: make edits, re-load Atom, repeat. Feel free to chat on gitter, and send a pull request.

Atoms package manager `apm` has a convenience command for woking on Atom
packages. By running `apm develop ensime <path-to-clone-to>` it will clone
`ensime/atom-ensime` to the specified location, install its dependencies, and
link it into Atoms package directory.

Alternatively you can perform these steps manually:

- Checkout the project from: https://github.com/ensime/ensime-atom

- Install the library dependencies: `apm install`

- Link the package into Atoms package directory: `apm link`

Once you've cloned and linked the code you can start developing

- In Atom: "Window: reload" (ctrl-option-cmd l) to reload plugin from source while developing.  Then start ENSIME in Atom as usual.

- View / Developer / Toggle Developer Tools gives you the usual console and other inspectors.


### Developing ensime-client node package in parallel

When developing ensime-atom, chances are high you will most likely need to develop the node package [ensime-client](https://www.npmjs.com/package/ensime-client) in parallel. This npm package was recently pulled out from ensime-atom to be a shared client lib for the node environment to use both in ensime-atom and a planned ensime-vscode.

To make the development smooth you will probably want to follow similar instructions as these:

[https://atom.io/docs/latest/behind-atom-developing-node-modules](https://atom.io/docs/latest/behind-atom-developing-node-modules)

Specific example of these follow.

Notice that as part of pulling these things out, the ensime-client is no longer depending on Atom's automatic compilation of coffeescript. It instead uses grunt to compile the coffescript into js that is exported. Therefore you'll need to set up a watch task as well.

- `git clone https://github.com/ensime/ensime-node`
- `cd ensime-node`
- `npm install`
- `npm link` (this creates a softlink from npm registry to this working directory)
- `apm rebuild` (atom special sauce)
- `npm run watch` (alias for grunt watch, but might replace for gulp) 

On the ensime-atom side:

- `cd ensime-atom`
- `npm link ensime-client` (this create a softlink from node_modules to the npm registry)

The npm link business is basically just this:
```
/Users/viktor/dev/projects/atom-ensime/node_modules/ensime-client -> /usr/local/lib/node_modules/ensime-client -> /Users/viktor/dev/projects/ensime-node
```

where `ensime-node` is my checked out git repo.


### Use server assembly jars

See [the server docs](/server/contributing/#manual-qa-testing) if you need to build your own server.


## Tricks and Tips

### Access ENSIME from the console

In the developer console, you can look up the package like this:

```
e = atom.packages.getActivePackage('Ensime').mainModule
```

From there you can access other parts of the package. E.g.,

```
client = e.clientOfEditor(atom.workspace.getActiveTextEditor())
```


## Inspiration (steal if you can)

- [Atom IDE support for Flow](https://github.com/lukehoban/atom-ide-flow/)
- [Atom TypeScript](https://github.com/TypeStrong/atom-typescript/)
- [IDE-Haskell](https://github.com/atom-haskell/ide-haskell)

## Useful Links

- [Atom Flight Manual](https://atom.io/docs) - see Chapter 3, _Hacking Atom_ in particular.
- [ENSIME project source](https://github.com/ensime/)
- [Swank Protocol source](https://github.com/ensime/ensime-server/blob/2.0/protocol-swanky/src/main/scala/org/ensime/server/protocol/swank/SwankFormats.scala)
- [Jerk Formats](https://github.com/ensime/ensime-server/blob/2.0/protocol-jerky/src/main/scala/org/ensime/jerky/JerkyFormats.scala)
- [Emacs command cheat sheet](editors/emacs/cheat_sheet/)
- [ENSIME Google Group](https://groups.google.com/forum/#!forum/ensime)
- [Startup of server from Emacs](https://github.com/ensime/ensime-emacs/blob/master/ensime-startup.el)
- [Space pen]( https://github.com/atom/space-pen/blob/master/src/space-pen.coffee)
- [Space pen views]( https://github.com/atom/atom-space-pen-views/blob/master/src/scroll-view.coffee)
- [Find and replace](https://github.com/atom/find-and-replace/blob/master/lib/project/results-pane.coffee)

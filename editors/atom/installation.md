---
layout: section
order: 1
title: Installation
---

## Prerequisites

Before you start make sure you have:

- generated a _.ensime_ for your project using one of the [supported build tools](http://ensime.github.io/build_tools/); and
- [Atom] installed.

## Installing Atom ENSIME

You can install Atom ENSIME either from the command line or from inside Atom.

#### From the command line

- `apm install ensime`

_or_

#### Inside Atom

- Open _Preferences_
- Click _Install_
- Search for _ENSIME_ in the search box
- Click _Install_


### Configuring Atom
  
Finally, you need to tell Atom where sbt is installed:

- Open _Preferences_ in Atom
- In _Packages_, search for _ENSIME_.
- Click _Settings_.
- In the _sbt Exec_ box, enter the path to the _sbt_ command.

For example, enter _/usr/local/bin/sbt_ if there's where sbt is for you.

## Using Atom

- Open any folder that contains at least one _.ensime_
- cmd-shift-P _ENSIME: Start_
- Then you can use the features above!

Every command in ENSIME can be found using cmd-shift-P and typing "ensime". Some are context bound and will turn up in a specific state, like "Ensime:lockTypeHover" which will only be available while a type hover tooltip is displayed.

## Related Atom Packages

### The following are automatically installed by Atom ENSIME:

- [language-scala] for syntax highlighting.
- [hyperclick] for code navigation. ENSIME hooks in as provider.
- [browser-plus] to display ScalaDoc.
- [linter] for display of errors and warnings.

This can be turned off via a setting if you for personal preference would like to uninstall or disable any of these packages.

### These are recommended:

- [Project manager] which is handy to keep track of projects.
- A plugin to navigate back to last cursor position when "code surfing" is useful. Something like [last-cursor-position], [cursor-history] or [navigation-history].


[sbt]: http://www.scala-sbt.org/download.html
[ensimeConfig]: /build_tools/sbt/
[language-scala]: https://atom.io/packages/language-scala
[linter]: https://atom.io/packages/linter
[hyperclick]: https://atom.io/packages/hyperclick
[browser-plus]: https://atom.io/packages/browser-plus
[Project manager]: https://github.com/danielbrodin/atom-project-manager
[last-cursor-position]: https://atom.io/packages/last-cursor-position
[navigation-history]: https://atom.io/packages/navigation-history
[cursor-history]: https://atom.io/packages/cursor-history
[Atom]: https://atom.io/

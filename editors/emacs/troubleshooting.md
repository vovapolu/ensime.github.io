---
layout: section
order: 10
title: Troubleshooting
---

Have you read all the documentation at [ensime.org/editors/emacs](http://ensime.org/editors/emacs)? Please do, we put a lot of effort into it.

Most problems can be resolved easily by following a simple process. Please do not skip these steps.

There are three classes of problem:

## Problem starting the ENSIME server

1. update `ensime` for Emacs, `M-x list-packages RET U RET x`.
1. update the server with `M-x ensime-server-update` (or manually update the assembly jar)
1. update your [build tool plugin](/build_tools).

Check the `*ENSIME-...*` server buffer and check for exceptions. If there is anything suspicios, kill the buffer (this stops the server), delete the `.ensime_cache`, and restart.

If that doesn't work, escalate matters: nuke old versions of ENSIME and restart Emacs:

```
rm -rf ~/.ivy2/cache/org.ensime ~/.ivy2/local/ ~/.emacs.d/ensime ~/.emacs.d/elpa/ensime* ~/.emacs.d/elpa/scala-mode* ~/.emacs.d/elpa/sbt-mode*
```

If **that** doesn't work, move your ivy folder aside, it has probably become corrupted:

```
mv ~/.ivy2 ~/.ivy2.bak
```

If that solved your problem, great!

If not, please join the conversation at [gitter.im/ensime/ensime-emacs](https://gitter.im/ensime/ensime-emacs) and let it be known that you have followed this guide (and you better not have skipped any steps). If you do not provide a reproduction, it is **extremely unlikely** that anybody will be able to help you. **Do not post stacktraces on the gitter channel**, instead yank the contents of `M-x ensime-troubleshooting` into a gist.

If you think you've found a bug you can file it at [github.com/ensime/ensime-emacs](https://github.com/ensime/ensime-emacs/issues/new) but do not ignore the [bug report template](https://github.com/ensime/ensime-emacs/blob/master/.github/ISSUE_TEMPLATE.md) or your ticket will be closed immediately.

Remember, everybody is here to help, but nobody is paid to maintain ENSIME. For ENSIME to be sustainable, we need you to engage in the bug fixing process rather heavily and (ideally) submit a pull request with a fix.

## Problem with red squiggly lines or broken completion / types

As documented in more detail in our [Contributing Guide](/contributing/#scala-compiler-and-refactoring), ENSIME relies on type information provided by Scala's Presentation
Compiler and it is known to issue false positives. But it is easier than you might think to fix the problems upstream.

However, many problems with red squiggly lines are actually a result of buggy macros or compiler plugins. To help you diagnose problems, we wrote [PC Plod](https://github.com/ensime/pcplod). The first thing you can do is to write a PC Plod unit test for the library that you are using to raise awareness with the author of that library that they not compatible with the presentation compiler (and error reporter).

It might also be appropriate for macro authors to provide alternative behaviour under the presentation compiler. As an example, consider the `cachedImplicit` macro within shapeless. It reports [false positives and can freeze the editor](https://github.com/milessabin/shapeless/issues/458). But if a variant of this macro was written to bypass the actual implementation, issuing a (configurable) warning, e.g. "This implicit derivation will be skipped in the editor", many developers would appreciate the workaround.

Then ask for help on the [gitter.im/scala/contributors](https://gitter.im/scala/contributors) channel to find out how to get involved in fixing the presentation compiler. Hopefully they will be able to advise if this is a macro or scalac problem, so don't raise a ticket on [issues.scala-lang.org](https://issues.scala-lang.org/secure/Dashboard.jspa) until you have confirmed where the problem is.

## Anything else

1. fully compile your project (did you skip the [User Guide](/editors/emacs/userguide/))? Time to read it, honestly it's full of good stuff.
1. following the steps in "Problem starting the ENSIME server" to ensure all your software is recent (this solves more than you'd expect)
1. check the [tickets flagged as FAQ for Emacs](https://github.com/ensime/ensime-emacs/issues?labels=FAQ) and do a quick search.
1. check the [tickets flagged as FAQ on the server](https://github.com/ensime/ensime-server/issues?labels=FAQ) and do a quick search.

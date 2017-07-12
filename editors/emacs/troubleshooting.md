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
1. update your [build tool plugin](/build_tools) and re-run the `.ensime` generator.

Check the `*ENSIME-...*` server buffer for exceptions. If there is anything suspicious, kill the buffer (this stops the server), delete the `.ensime_cache`, and restart.

If that doesn't work, escalate matters: nuke old versions of ENSIME and restart Emacs:

```
rm -rf ~/.coursier/cache/v1/https/oss.sonatype.org/content/repositories/snapshots \
       ~/.emacs.d/ensime* \
       ~/.emacs.d/elpa/ensime* \
       ~/.emacs.d/elpa/scala-mode* \
       ~/.emacs.d/elpa/sbt-mode*
```

If that doesn't work, try nuking your build tool's cache. e.g. if you're using `sbt`

```
rm -rf ~/.ivy2/cache/org.ensime \
       ~/.ivy2/local \
       project/target \
       ~/.sbt/0.13/target \
       ~/.sbt/0.13/plugins/target
```

If **that** doesn't work, move your ivy folder aside, it has probably become corrupted:

```
mv ~/.ivy2 ~/.ivy2.bak
```

## Problem with red squiggly lines or broken completion / types

As a side effect, you're probably experiencing hanging, remember to `C-g` or `ESC ESC ESC` to get Emacs back instantly.

1. compile your project, or open all dependent scala files
1. restart the presentation compiler: `C-c C-c r` (`ensime-reload-open-files`)

If that doesn't work, try a few more things:

1. restart the server with `M-x ensime-reload`
1. if macro related, close the file defining the macro ([known and sponsored issue](https://github.com/ensime/ensime-server/issues/1152))
1. if compiler plugin related, ensure plugins are in your `.ensime` (via your [build tool](/build_tools))

As documented in more detail in our [Contributing Guide](/contributing/#scala-compiler-and-refactoring), ENSIME relies on type information provided by Scala's Presentation
Compiler and it is known to issue false positives. But it is easier than you might think to fix the problems upstream.

To help you diagnose problems, we wrote [PC Plod](https://github.com/ensime/pcplod). The first thing you can do is to write a PC Plod unit test for the library that you are using to raise awareness with the author of that library that they not compatible with the presentation compiler (and error reporter).

## Anything else

1. fully compile your project (did you skip the [User Guide](/editors/emacs/userguide/))? Time to read it, honestly it's full of good stuff.
1. following the steps in "Problem starting the ENSIME server" to ensure all your software is recent (this solves more than you'd expect)
1. check [all ENSIME FAQ issues](https://github.com/search?utf8=%E2%9C%93&q=user%3Aensime+is%3Aissue+label%3AFAQ&type=Issues&ref=searchresults) and do a quick search.

If that solved your problem, great!

If not, please join the conversation at [gitter.im/ensime/ensime-emacs](https://gitter.im/ensime/ensime-emacs) and let it be known that you have followed this guide. If you do not provide a reproduction in the form of a project, it is **extremely unlikely** that anybody will be able to help you.

**Do not post stacktraces on the gitter channel**, instead yank the contents of `M-x ensime-troubleshooting` into a gist.

If you think you've found a bug you can file it at [github.com/ensime/ensime-emacs](https://github.com/ensime/ensime-emacs/issues/new) but do not ignore the [bug report template](https://github.com/ensime/ensime-emacs/blob/master/.github/ISSUE_TEMPLATE.md) or your ticket will be closed immediately.

Remember, everybody is here to help, but nobody is paid to maintain ENSIME (not even the sponsored developers). For ENSIME to be sustainable, we need you to engage in the bug fixing process rather heavily and (ideally) submit a pull request with a fix.

---
layout: section
order: 10
title: Troubleshooting
---

Have you read all the documentation at [ensime.org/editors/emacs](http://ensime.org/editors/emacs)? Please do, we put a lot of effort into it.

Most problems can be resolved easily by following a simple process. Please do not skip these steps.

## Problem starting the ENSIME server

1. update `ensime` for Emacs, `M-x list-packages RET U RET x`.
1. follow the troubleshooting guide for your [build tool plugin](/build_tools) and re-run the `.ensime` generator, e.g. the [`sbt-ensime` Troubleshooting Guide](/build_tools/sbt#starting-the-server)
1. check the `*ENSIME-...*` server buffer for exceptions. If there is anything suspicious, kill the buffer (this stops the server), delete the `.ensime_cache`, and restart.

## Problem with red squiggly lines and broken completion / types

As a side effect, you're probably experiencing hanging, remember to `C-g` or `ESC ESC ESC` to get Emacs back instantly.

1. compile your project, or open all dependent scala files
1. restart the presentation compiler: `C-c C-c r` (`ensime-reload-open-files`)
1. try restarting the server with `M-x ensime-reload`
1. read the [`ensime-server` Troubleshooting Guide](/server/troubleshooting)

## Anything else

1. get more information by [debugging emacs](/editors/emacs/contributing/)

If that solved your problem, great!

If not, please join the conversation at [gitter.im/ensime/ensime-emacs](https://gitter.im/ensime/ensime-emacs) and let it be known that you have followed this guide, and the linked guides, by introducing yourself with "wibble wibble I'm a fish", so that we know you read this far. If you do not provide a reproduction in the form of a project, it is **extremely unlikely** that anybody will be able to help you.

**Do not post stacktraces on the gitter channel**, instead yank the contents of `M-x ensime-troubleshooting` into a gist.

If you think you've found a bug you can file it at [github.com/ensime/ensime-emacs](https://github.com/ensime/ensime-emacs/issues/new) but do not ignore the [bug report template](https://github.com/ensime/ensime-emacs/blob/master/.github/ISSUE_TEMPLATE.md) or your ticket will be closed immediately.

Remember, everybody is here to help, but nobody is paid to maintain ENSIME (not even the sponsored developers). For ENSIME to be sustainable, we need you to engage in the bug fixing process rather heavily and (ideally) submit a pull request with a fix.

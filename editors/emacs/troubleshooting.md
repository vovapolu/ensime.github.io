---
layout: section
order: 10
title: Troubleshooting
---

Have you read all the documentation at [ensime.org/editors/emacs](http://ensime.org/editors/emacs)? Please do, we put a lot of effort into it.

Most problems can be resolved easily by following a simple process. Please do not skip these steps:

1. fully compile your project
1. update `ensime` for Emacs.
1. update the server with `M-x ensime-server-update`.
1. update your [build tool plugin](/build_tools).
1. check the [tickets flagged as FAQ for Emacs](https://github.com/ensime/ensime-emacs/issues?labels=FAQ) and do a quick search.
1. check the [tickets flagged as FAQ on the server](https://github.com/ensime/ensime-server/issues?labels=FAQ) and do a quick search.
1. nuke old versions of ENSIME and restart Emacs:
   - `rm -rf ~/.ivy2/cache/org.ensime`
   - `rm -rf ~/.ivy2/local/`
   - `rm -rf ~/.emacs.d/ensime`
   - `rm -rf ~/.emacs.d/elpa/ensime*`
   - `rm -rf ~/.emacs.d/elpa/scala-mode*`
   - `rm -rf ~/.emacs.d/elpa/sbt-mode*`

If that solved your problem, great!

If not, please join the conversation at [gitter.im/ensime/ensime-emacs](https://gitter.im/ensime/ensime-emacs) and let it be known that you have followed this guide (and you better not have skipped any steps). If you do not provide a reproduction, it is **extremely unlikely** that anybody will be able to help you. **Do not post stacktraces on the gitter channel**, instead yank the contents of `M-x ensime-troubleshooting` into a gist.

If you think you've found a bug you can file it at [github.com/ensime/ensime-emacs](https://github.com/ensime/ensime-emacs/issues/new) but do not ignore the [bug report template](https://github.com/ensime/ensime-emacs/blob/master/.github/ISSUE_TEMPLATE.md) or your ticket will be closed immediately.

Remember, everybody is here to help, but nobody is paid to maintain ENSIME. For ENSIME to be sustainable, we need you to engage in the bug fixing process rather heavily and (ideally) submit a pull request with a fix.

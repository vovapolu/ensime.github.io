---
layout: section
order: 99
title: Contributing
---

## Emacs Lisp

The [GNU Emacs Lisp Reference Manual](https://www.gnu.org/software/emacs/manual/elisp.html) is a very enjoyable read and will prepare you for everything you need to contribute to any Emacs package.

We have some suggested [hacks for Emacs Lisp](/editors/emacs/hacks#emacs-lisp) that you may enjoy.

If you want a playground to exercise your newly found Emacs Lisp muscles, consider forking @fommil's [port of 99 problems](https://github.com/fommil/e99) and re-implementing the answers.

## Debugging

Try setting the following and reading the documentation of what each does (recall you can do this with `C-h v` over any variable in Emacs)

```lisp
(setq debug-on-error t
      debug-on-quit t
      ensime-log-events t
      ensime--debug-messages t)
```

## Setup

First, clone the git repo hosted at [github.com/ensime/ensime-emacs](https://github.com/ensime/ensime-emacs). If you pick up a ticket, please comment on it to let us know so that we can help (and also to avoid overlapping with somebody else). Feel free to ask questions on the github issue tracker or [gitter.im/ensime/ensime-emacs](https://gitter.im/ensime/ensime-emacs).

The `.drone.yml` describes what our CI does and this can be followed for your local development.

You must install [Cask](http://cask.readthedocs.org/en/latest/guide/installation.html), the excellent build tool for Emacs Lisp projects and then initialise the repository and install the dependencies with:

```
cask pkg-file
cask install
```

## Testing

It all starts with a test.

The old tests are in `ensime-tests.el` but [we want to migrate](https://github.com/ensime/ensime-emacs/issues/389) to use [ert](http://www.gnu.org/software/emacs/manual/html_mono/ert.html) (see `test/ensime-emacs-test.el`) and [ecukes](https://github.com/ecukes/ecukes) (see the `features` directory).

To run the old tests, run the hacky `test/run_emacs_tests.sh` script.

To run the new, preferred style, tests, type `cask exec ert-runner` and `cask exec ecukes`.

## Performance

If you think the client side is suffering performance problems, use `M-x profiler-start`, edit some code and experience the slowdown, `M-x profiler-report`. Once you find the cause, you can stop profiling with `M-x profiler-stop`.


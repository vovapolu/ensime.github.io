---
layout: section
order: 3
title: Installation
---

- TOC
{:toc}


## System requirements

### Stable

- JDK 1.6+
- Emacs 24.3+
- Scala 2.10.4+ / 2.11.5+

### Unstable

- JDK 1.7+
- Emacs 24.5+
- Scala 2.10.6+ / 2.11.8+

## Installing

We assume that you already have [MELPA](http://melpa.org) set up as per our [Learning Emacs](/editors/emacs/learning) guide.

The recommended way to install ENSIME is via MELPA stable and `use-package`:

```elisp
(use-package ensime
  :pin melpa-stable)
```

If you used the sample Emacs configuration from our [`Learning Emacs`](/editors/emacs/learning) section, then you can add the above code to the end of your `~/.emacs.d/init.el` file and restart Emacs.  Emacs will automatically install Ensime during startup.  Alternatively, you can execute this without restarting Emacs by moving the cursor ("point" in Emacs nomenclature) to the end of the line and typing `C-x C-e`.

To use the unstable version of ENSIME from MELPA, remove `:pin melpa-stable` (not recommended unless you are contributing to ENSIME).

For the server installation to work, make sure `sbt` is on your `PATH` environment variable or `exec-path` Emacs variable, e.g.:

```elisp
(add-to-list exec-path "/usr/local/bin")
```

Basic Scala support is provided by [`scala-mode`](/editors/emacs/scala-mode) which provides many features specific to Scala major mode editing and sbt support is provided by [`sbt-mode`](/editors/emacs/sbt-mode). Both modes can be used independently of ENSIME and your are encouraged to read their standalone documentation to understand the role that they play.


## Updating

ENSIME uses a continuous release and the developers assume that you are staying up to date with releases.

The server will be automatically upgraded when you upgrade the client, which will result in a short `*ensime-update*` session. You can manually force a server update by typing:

```
M-x ensime-server-update
```


## Starting

Compile your project with your [build tool](/build_tools) and generate a `.ensime` file. Then navigate to a file or directory in your project and type:

```
M-x ensime
```

**Check that again**. It is very important that you compile your project and have generated a `.ensime` file from one of the supported build tools.

The first time you use ENSIME, you can expect to wait several minutes for the server and all of its dependencies to be downloaded.

On first use for a project, you will need to wait a few moments for indexing to complete.

Once the server is available, enjoy editing with the ENSIME commands that are documented in the [User Guide](/editors/emacs/userguide) and consider using some of the suggestions in our [Hacks](/editors/emacs/hacks) page to improve your productivity in Emacs when editing Scala code.

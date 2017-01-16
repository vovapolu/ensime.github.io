---
layout: section
order: 4
title: User Guide
---

- TOC
{:toc}


## Scala REPL

First, ensure that the classes you want to access are compiled, type `C-c C-v z` to launch the embedded Scala REPL. The REPL should be launched with all your project classes loaded and available.

The SCALA REPL mode highlights stacktraces and lets you jump to source locations.


## Understanding the Server

### How the typechecker works

ENSIME uses the Scala presentation compiler, a light-weight version of the full compiler that only performs the first few stages of a compilation. It returns syntax/type errors, as well as the type of every expression, in fractions of a second rather than several seconds. This is how you receive instant feedback when you edit a `.scala` file.

In order to parse a source file correctly, the presentation compiler needs to know the type of every external class or object the source file uses. That information must be kept up-to-date whenever you make changes. There are two ways to accomplish this: load all source files, or depend on the project being compiled.

### Loading all source files

This is the simplest mode to understand but it has a few drawbacks. Type `C-c C-c a` to activate it. In this mode, every `.scala` file in your project is parsed. Editing a file causes everything to be reparsed again (starting with the file you just modified). The presentation compiler is always in sync with the state of your project.

The major disadvantage is that re-parsing everything takes too long for anything except the smallest of projects.

### The project's .class files

This is ENSIME's default mode of operation. In this mode, the presentation compiler loads type information from `.class` files, and only load the source files that are being edited. This means that reparsing is always very fast. This only works if your project has been compiled, otherwise ENSIME will show you lots of spurious errors.

This mode works well if you spend most of your time editing a small number of files. The compiler's state will be up to date regarding the file being edited. You should recompile whenever you want to see the effects of inter-file dependencies. When you recompile, ENSIME notices the change and reloads all open file.

You can revert from the "load all sources" mode to the default mode by typing `C-c C-c r`. Also try that key combination whenever the typechecker seems to produce wrong information.

### Caveat: refactor features only in "source" mode

You must type `C-c C-c a` before using "Refactor/Rename" (`C-c C-r r`) and "Source/Find all references" (`C-c C-v r`). At the moment, these two commands will give incomplete results unless all source files are parsed. We plan to fix this in [ensime-server#425](https://github.com/ensime/ensime-server/issues/425).


## sbt

There is support for starting and interacting with sbt inside Emacs, provided by [`sbt-mode`](/editors/emacs/sbt-mode).

This section highlights some of the ENSIME specific extensions and integrations with `sbt-mode`.

Commands beginning `C-c C-b` are used to communicate with sbt. Type `C-c C-b C-h` to see the full list.

The extra sbt integration enables some convenient workflow options:

- For small projects, typing `C-c C-c a` may save you from having to use the build tool (fire and forget).
- For small to medium projects, you can customize `ensime-sbt-perform-on-save` to `"compile"`. This is much more efficient than using sbt's `~compile` polling support.
- For larger projects, compiling on every save may not be practical. You can type `C-c C-b c` every once in a while.
- If your workflow involves running tests often, this will keep your project compiled as a side effect.


## Editing

### Error Highlighting

ENSIME will highlight errors and warnings in source files through the use of the Scala presentation compiler, a lightweight version of the Scala compiler. This is triggered in several ways:

- when you save a file
- when you type `C-c C-c c`
- after a short pause in typing. The frequency of these checks is controlled through the variables `ensime-typecheck-idle-interval` and `ensime-typecheck-interval`. This 
feature can be disabled by setting `ensime-typecheck-when-idle` to `nil`.

Typing `C-c C-c e` lists all errors and warnings in a separate window. Hovering the mouse over a highlighted error or typing `C-c C-v e` displays the error details in the echo area.

### Semantic Highlighting

ENSIME's semantic highlighting adds true colour-coding based on the compiler's analysis of the source code.

Semantic Highlighting is enabled by default. To disable it, set the customization variable `ensime-sem-high-enabled-p` to `nil`. When Semantic Highlighting is enabled, colours are refreshed every time you save the file.

To customise the colours used during semantic highlighting, change the value of the variable `ensime-sem-high-faces`, which is a list of `(symbolType . face)` associations.

### Implicit conversion highlighting

ENSIME highlights implicit conversions during semantic highlighting. Hover over a highlighted area or type `C-c C-v e` to see the details of the implicit conversion.

### Code Completion

ENSIME completion is initiated automatically (via the `company-mode` backend) or by pressing the `TAB` key. Currently this works for local variables, method parameters, unqualified method names, and type names. An alternative completion backend is provided for users of the `ac` (auto complete) package, but it is unmaintained.

### Summarising the file

ENSIME provides an `imenu`-compatible summary of your source file, accessible through `M-x imenu` and compatible viewers. We recommend [`popup-imenu`](https://github.com/ancane/popup-imenu) as it gives a visual overview of your file.

### Source Formatting

ENSIME uses the Scalariform library to format Scala sources. Type `C-c C-v f` to format the current buffer. Your build tool should provide options to enable you to provide the exact formatting rules to use.


## Refactoring

Refactoring is provided by the [github.com/scala-ide/scala-refactoring](https://github.com/scala-ide/scala-refactoring) library.

### Add type to symbol

Place your cursor over the symbol you'd like to add the type and type `C-c C-r a`.

### Rename

Place your cursor over the symbol you'd like to rename. Type `C-c C-r r` and follow the minibuffer instructions.

### Organize Imports

Type `C-c C-r o` in a Scala source buffer. Follow the minibuffer instructions.

### Extract Method

Select a region by setting the mark using `C-SPACE` and then placing the point at the end of the region. All selected code will be extracted into a helper method. Type `C-c C-r m` and follow the minibuffer instructions.

### Inline Local

Place your cursor over the local val whose value you'd like to inline. Type `C-c C-r i` and follow the minibuffer instructions.


## Navigating

Most things in the inspector are hyper-linked. You can click these links with the mouse or position your cursor over them and press ENTER. A history is kept of all the pages you view in the inspector. Go back in this history by typing `,` and forward by typing `.`.

### Documentation Browsing

Type `C-c C-v d` to browse a symbol's Javadocs / Scaladocs in your browser.

You can also view a list of all the documentation available for your project by typing `M-x ensime-project-docs`.

### Type and Method Search

Type `C-c C-v v` to start a global search. This should provide a live search view with support for camel case. We'd really like to integrate this search with more conventional search feedback systems (e.g. ido / helm), see [ensime-emacs#186](https://github.com/ensime/ensime-emacs/issues/186).

### Jump to Test

ENSIME allows you to quickly jump to a class' unit test. With the cursor inside a class definition, type `C-c C-t t` to go to the corresponding test class. If the class doesn't exist, a new file will be created. With the cursor inside a test class, type `C-c C-t i` to go to the corresponding implementation class.

If your project uses an unusual convention, you must customize `ensime-goto-test-configs` or `ensime-goto-test-config-defaults`. These variables also specify the template to use when creating new test classes.

### Jump to Definition

Press `M-.` with the cursor on a variable, method, type, or package to visit that object's definition. `M-,` returns to where you were.

If this doesn't work for you, please try to create a fully reproducible example and submit it as a ticket on the server at [ensime-server#492](https://github.com/ensime/ensime-server/issues/492). We know it sometimes breaks, but we need solid reproduction cases to investigate further.

## Inspector

### Invocation

Typing `C-c C-v i` while the point is over a symbol will launch the type inspector. Typing `C-c C-v o` will open the inspector on the current project's main package. `C-c C-v p` will inspect the package of the current source file. Use the command `M-x ensime-inspect-by-path` to inspect an arbitrary type or package.

### Package Inspector

Displays a hierarchical view of a package, including all top-level types. Select a type to open the Type Inspector. This doesn't show implementing classes, but we would like to do that in [ensime-server#339](https://github.com/ensime/ensime-server/issues/339).

### Type Inspector

Lists the interfaces that contribute members to the inspected type. List each interface's methods, with full type signatures. If the type has a companion object/class, a link to the companion will appear under the heading.

## Helm

To enable helm support use `(setq ensime-use-helm t)` in your configuration. Alas not a lot is changed by this option. This will hopefully change in the future.

## Debugging

### Break Points

With your cursor on a line of Scala source, type `C-c C-d b` to set a breakpoint. Type `C-c C-d u` to remove the breakpoint. Note that breakpoints can be added and removed outside of any debug session. Breakpoints are not, however, persisted between runs of ENSIME.

### Launching the Debugger

Launch your application using your build tool with debugging enabled. e.g. via the [sbt-ensime debugging](http://ensime.github.io/build_tools/sbt/#debugging-example) support.

Then attach ENSIME to the running process with `M-x ensime-db-attach`. The first breakpoint your program hits will be highlighted and centered in Emacs.

### Run Control

Type `C-c C-d c` to continue after hitting a breakpoint, or `C-c C-d s` to step into the current line, or `C-c C-d n` to step to the next line, or `C-c C-d o` to step out of the current function.

### Value Inspection

When execution is paused, with your cursor over a local variable, type `C-c C-d i` to inspect the runtime value of a variable.

### Show Backtrace

When execution is paused, type `C-c C-d t` to display the current backtrace.

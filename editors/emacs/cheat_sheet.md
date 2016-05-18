---
layout: section
order: 1
title: Cheat Sheet
---

## Customisation

To customise your ENSIME Emacs experience, don't forget to read through the user-customisable variables with `M-x customize-group RET ensime RET`, as defined in [ensime-vars.el](http://github.com/ensime/ensime-emacs/blob/master/ensime-vars.el).

## Source

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-v f` | Format the current source file |
| `C-c C-v r` | List all references to the symbol under the cursor |
| `C-c C-v i` or `Control+Right-click` | Inspect the type of the expression under the cursor |
| `C-c C-v 5 i` | Inspect the type of the expression under the cursor, in other frame |
| `C-c C-v t` or hover mouse | Show the type of the symbol under the cursor |
| `C-c C-v e` or hover mouse | Show compile warnings under the cursor ; show implicit conversions when applicable |
| `C-c C-v p` | Inspect the package of the current source file, or the package under the cursor |
| `C-c C-v o` | Inspect the package specified in .ensime as :project-package. |
| `C-c C-v u` | Undo a refactoring or formatting change |

## Presentation Compiler

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-c c` | Typecheck the current file |
| `C-c C-c a` | Typecheck all files in the project |
| `C-c C-c r` | Reset the typechecker then typecheck all open files in the project |
| `C-c C-c e` | Show all errors and warnings from the last typecheck or compilation |


## Testing

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-t t` | Go to (or create) test for current class |
| `C-c C-t i` | Go to implementation of the current test |

## Refactoring

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-r a` | Add type to the symbol under the cursor |
| `C-c C-r o` | Organize imports in the current file |
| `C-c C-r t` | Import the type under the cursor |
| `C-c C-r r` | Rename the symbol under the cursor |
| `C-c C-r l` | Extract the region into a local value |
| `C-c C-r m` | Extract the region into a method |
| `C-c C-r i` | Inline the local value under the cursor |

## Navigation

| Shortcut    | Description |
|-------------|-------------|
| `M-.` or `Control+Left-Click` | Jump to the definition of the symbol under the cursor |
| `M-x ensime-edit-definition-other-window` | Jump to the definition of the symbol under the cursor, into another window |
| `M-x ensime-edit-definition-other-frame` | Jump to the definition of the symbol under the cursor, into another frame |
| `M-,` | Pop back to the previously visited position |
| `M-n` | Go to the next compilation note in the current buffer |
| `M-p` | Go to the previous compilation note in the current buffer |
| `C-c C-v .` | Select the surrounding syntactic context. Subsequent taps of '.' and ',' will grow and shrink the selection, respectively |
| `C-c C-v v` | Search globally for methods or types |

## Documentation

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-v d` | Browse the documentation of the symbol under the cursor |

## SBT

Much of this is a wrapper over [`sbt-mode`](https://github.com/hvesalai/sbt-mode), so don't forget that you also have commands provided as-is by that package.

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-b s` or `C-c C-v s` | Start a SBT process, or switch to an existing one |
| `C-c C-b S` | Switch to buffer containing the stack trace parser |
| `C-c C-b c` | Compile |
| `C-c C-b n` | Clean |
| `C-c C-b o` | Run the current test |
| `C-c C-b p` | Package |
| `C-c C-b r` | Run |
| `C-c C-b T` | Run all tests |
| `C-c C-b t` | Run "quick" tests (tests impacted by recent changes) |

## Type/package inspector

| Shortcut    | Description |
|-------------|-------------|
| `TAB` or `M-n` | Forward page |
| `M-p` | Backward page |
| `RET` or `Left-Click` | If the cursor is over a type, inspect that type. If the cursor is over a method, go to its source code |
| `,` | Go back in the inspector history|
| `.` | Go forward in the inspector history|

## Debugger

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-d d` | Start the debugger |
| `C-c C-d b` | Set a breakpoint at the current line |
| `C-c C-d u` | Remove the breakpoint at the current line |
| `C-c C-d a` | Remove all breakpoints |
| `C-c C-d r` | Start debugging the current program |
| `C-c C-d s` | Step into method invocations |
| `C-c C-d o` | Step out of method invocations |
| `C-c C-d n` | Step to the next line |
| `C-c C-d c` | Continue the program execution |
| `C-c C-d q` | Stop debugging the current program |
| `C-c C-d t` | Show the current backtrace |
| `C-c C-d i` | Inspect the value of the symbol under the cursor |

## REPL

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-v z` | Start the Scala REPL or switch to it |
| `C-c C-v C-r` | Send the region to the REPL |
| `C-c C-v v` | Evaluate the current buffer in the REPL |
| `C-c C-v l` | Prompt for a file and load it in the REPL |

## Miscellaneous

| Shortcut    | Description |
|-------------|-------------|
| `C-c C-b S` | Create a "stacktrace" buffer or switch to it |
| `M-x ensime-shutdown` | Shut down ENSIME |
| `M-x ensime-reload` | Reload the .ensime file and recompile the project |
| `M-x ensime-inspect-by-path` | Prompt for a type or package and inspect it |


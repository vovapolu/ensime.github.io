---
layout: section
order: 5
title: Troubleshooting
---

## Troubleshooting

Things go wrong -- we know! Here are some of the main gotchas. If these tips don't solve your problem, [ask on Gitter][gitter] and check the [issue tracker][issues] to see if others have had the same problem.

## Let's get this out of the way first

- Ensure you have created a `.ensime` file using the `ensimeConfig` command.

  If you have recently (re)generated your `.ensime` file, you may have to quit and restart Sublime Text to pick up the changes.

- Ensure the top-most item in the Side Bar (*View Menu / Side Bar / Show Side Bar*) is your project directory (the one containing the `.ensime` file).

  If not, choose *Project Menu / Add Folder to Project...* and select the project root directory. You'll be able to continue working in the same file.


## Server out of date

Nuke old versions of the ENSIME server and try again

- `rm -rf ~/.ivy2/cache/org.ensime`
- `rm -rf ~/.ivy2/local/org.ensime`


## Checking Java Visibility

Unsure whether Sublime Text can see Java on your system application path? Try pasting the following commands one at a time into the Sublime Text console (*View menu / Show Console*).

On Linux or OS X:

~~~ python
# Check the visibility of Java:
import subprocess; print(subprocess.check_output(['which', 'java'], stderr=subprocess.STDOUT).decode("utf-8"))
~~~

On Windows:

~~~ python
# Check the visibility of Java:
import subprocess; print(subprocess.check_output(['where', 'java'], stderr=subprocess.STDOUT).decode("utf-8"))
~~~

In each case you should see a path string, something like this:

~~~
b'/usr/bin/java\n'
~~~

If you see an error message like this, Sublime Text can't see the relevant executable:

~~~
Traceback (most recent call last):
  File "<string>", line 1, in <module>
  File "./subprocess.py", line 589, in check_output
subprocess.CalledProcessError: Command '['which', 'java']' returned non-zero exit status 1
~~~

## Checking Java Versions

Ideally you should be using Java 8. To check this, paste the following commands one at a time into the console (*View Menu / Show Console*):

~~~ python
# Check the Java version:
import subprocess; print(subprocess.check_output(['java', '-version'], stderr=subprocess.STDOUT).decode("utf-8"))
~~~


## None of the commands in the context menu are clickable ?

If all the commands in the context menu are greyed out, it is most likely because ENSIME is still indexing your files or encountered some error while doing so. Once the indexing is complete you a get a message in the console saying "Indexer is ready! ...". 

If it's been too long and the log files show no indexing messages or any error, deleting the `.ensime_cache` folder in your project directory and restarting ENSIME is worth a try. This will lead to a fresh start and re-index all the files. It only takes a while the first time you Startup ENSIME and is much faster in the subsequent runs.

## Line Endings

If you find that some features of Ensime are not working properly (e.g. *Go To Definition* or *Error Highlighting*), check the *Line Endings* setting in Sublime Text.

On Windows, the line endings is set to *Windows* by default. ENSIME Sublime requires it to be *Unix*. Change the setting by going to *View menu / Line Endings* and selecting *Unix*.

Also check *View menu / Console* for log information.

## Ensime and Multiple Cursors

By default, Sublime Text 3 on OSX binds the `Command + Click` or `⌘-Click` action to setting a new cursor. Having started Ensime and attempted to follow a definition with `⌘-Click`, you may inadvertently create many new cursors instead. 

You can rebind `⌘-Click` to `goto_definition` in Sublime, allowing Ensime's behavior to take precedence.

Cancel any extra cursors by pressing `Esc`. Then, go to the location on your system where Sublime user preferences are defined. On OSX, this is `~/Library/Application Support/Sublime Text 3/Packages/User/`. If it does not already exist, create a file called `Default (OSX).sublime-mousemap`.

Into the `Default (OSX).sublime-mousemap` file, paste the following setting:

```
[
  {
    "button": "button1",
    "count": 1,
    "modifiers": ["super"],
    "press_command": "drag_select",
    "command": "goto_definition"
  }
]
```

See [Stack Overflow][so-goto-definition] for additional tips. Instructions on Linux and Windows are similar, but you should use the proper `mousemap` filename for your system. The `super` modifier means `⌘` on OSX. On Windows, `super` is the "Windows" key. You can also experiment with `ctrl` and `alt`.

[gitter]: https://gitter.im/ensime/ensime-sublime
[issues]: https://github.com/ensime/ensime-sublime/issues
[so-goto-definition]: http://stackoverflow.com/questions/16235706/sublime-3-set-key-map-for-function-goto-definition

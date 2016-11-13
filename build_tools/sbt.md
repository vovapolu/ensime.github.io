---
layout: section
order: 2
title: SBT
---

- TOC
{:toc}

This [sbt](http://github.com/sbt/sbt) plugin generates a `.ensime` file and provides various convenience commands for interacting with [ENSIME](http://github.com/ensime/ensime-server).

## Install

Add these lines to `~/.sbt/0.13/plugins/plugins.sbt` as opposed to `project/plugins.sbt` (the decision to use ENSIME is per-user, rather than per-project):

```scala
addSbtPlugin("org.ensime" % "sbt-ensime" % "1.11.3")
```

**Check that again**, if you incorrectly used `~/.sbt/0.13/plugins.sbt` you'll get an sbt resolution error, it really has to be in the `plugins` folder.

**One more check** we've undergone a few artefact name changes - make sure you copied the full line.

Create the `.ensime` file by starting `sbt` (in the terminal or your editor's `sbt` mode) and run the `ensimeConfig` command.

If you are unable to install the plugin due to your firewall restrictions, copy the `EnsimePlugin.scala` into your `project` directory and make sure you have `scalariform` and `scalap` on your project definition's classpath.


## Learn to use SBT

If you've come from an IDE you might not be aware of the power of `sbt`. Please take the time to read the [sbt Getting Started Guide](http://www.scala-sbt.org/0.13/docs/Getting-Started.html) before proceeding and appreciate that `sbt` is responsible for building your project, not ENSIME.

## Core Commands

The core `sbt-ensime` plugin allows you to generate `.ensime` files:

* `ensimeConfig` --- Generate a `.ensime` for the project (takes space-separated parameters to restrict to subprojects).
* `ensimeConfigProject` --- Generate a `project/.ensime` for the project definition.

Note that downloading and resolving the sources and javadocs can take some time on first use, so we recommend that you use [coursier](http://get-coursier.io).

## Extra Tasks and Commands

Also bundled are extra workflow tasks, which are used by ensime clients:

* `ensimeRunMain` --- alternative to `runMain` allowing environment variables and jvm arguments to be used, e.g. `a/ensimeRunMain FOO=BAR -Xmx2g foo.Bar baz`
* `c/ensimeLaunch MyApp` --- a launch manager that lets you define pre-canned `ensimeRunMain` applications (analogous to IntelliJ's "Run Configurations")
* `b/ensimeCompileOnly` --- Compile a single fully qualified `.scala` file using `b`'s classpath. Takes custom flags, e.g. `scalacOptions in (Test, ensimeCompileOnly) ++= Seq("-Xshow-phases")`
* `b/ensimeScalariformOnly` --- Format a single fully qualified `.scala` file using `b`'s scalariform settings (compatible with, but does not require, `sbt-scalariform`).
* `ensimeRunDebug` --- like `ensimeRunMain` but adds debugging flags automatically
* `debugging` / `debuggingOff` --- mutates the default `javaOptions` to include debugging flags (see below)


### Debugging Example

Debugging an application is the easiest:

```
> ensimeRunDebug foo.Bar
```

but debugging tests are trickier.

If you do not `fork` your tests from `sbt` you may be able to attach a remote debugger to the entire session by starting like `sbt -jvm-debug 1337` (check the docs of your `sbt` script). However, if you have `fork in Test := true` then you can use our `debugging` task to mutate the java options to include the necessary flags:

```
crossbuild ~/Projects/ensime-server sbt
> debugging
[warn] Enabling debugging for all forked processes
[info] Only one JVM can use the port and it will await a connection before proceeding.
> jerk/test-only *JerkFormatsSpec
Listening for transport dt_socket at address: 5005
```

at which point, the test will hang until you connect a remote debugger to port 5005. When you are finished debugging, cancel the test or let it run to completion, and then type `debuggingOff`.

## Customise

For project-specific tailorings, you do not need to commit anything to your project. Simply create an `ensime.sbt` in your project's base directory (beside `build.sbt`). Don't forget to add it to your `~/.gitignore`. Here is an example that sets a specific memory size for the ensime server:

```scala
ensimeJavaFlags in ThisBuild := Seq("-Xss2m", "-Xms1024m", "-Xmx2048m", "-XX:ReservedCodeCacheSize=256m", "-XX:MaxMetaspaceSize=512m")
```

another, to use ENSIME on a Java 6 or 7 project (the server needs JDK 8). This one is so common you might want to put it in your `~/.sbt/0.13/global.sbt`:

```scala
ensimeJavaHome in ThisBuild := file("/usr/lib/jvm/java-8-openjdk")
```

another, for Android projects:

```scala
ensimeJavacOptions ++= (javacOptions in (core, Compile)).value,
ensimeScalacOptions ++= (scalacOptions in (core, Compile)).value
```

and another, for hacking on [scala](https://github.com/scala/scala) itself:

```scala
// NOTE: because of https://github.com/ensime/ensime-sbt/issues/240
//       you cannot use the ensime assembly jars or start the REPL

// WORKAROUND: https://github.com/scala/scala/pull/5387
ensimeScalaVersion in ThisBuild := "2.11.8"
```

After adding this file, run `sbt ensimeConfig` and the new settings will be included in the `.ensime` file.

## Troubleshooting

Always check the [tickets flagged as FAQ](https://github.com/ensime/ensime-sbt/issues?q=label%3AFAQ) before reporting a new issue.

Tickets are extremely hard to reproduce unless you create a minimal example project and share with us the steps to reproduce the problem.

Bug reports in the form of a pull request into the `src/sbt-test/ensime-sbt` directory are well received, which is our suite of integration tests using the [sbt scripted](http://eed3si9n.com/testing-sbt-plugins) framework (its very simple to use). Pull requests with tests and fixes are living the dream.

You can follow snapshot releases by using the following instead of the stable release

```scala
// or clone this repo and type `sbt publishLocal`
resolvers += Resolver.sonatypeRepo("snapshots")

// update to the latest development version, see project/EnsimeSbtBuild.scala
addSbtPlugin("org.ensime" % "sbt-ensime" % "<WHATEVER IS LATEST>")
```

### Cancel Processes

By default, `sbt` will not cancel a running subprocess if you type `C-c`. You are recommended to add the following to your `~/.sbt/0.13/global.sbt` so that it will do so:

```scala
cancelable in Global := true
```

Emacs users should recall that in order to send a control sequence to the `sbt-mode` subprocess, first run `sbt-clear` (bound to `C-c C-v` by default) then `C-c`. i.e. to send `C-c` to `sbt`, type `C-c C-v C-c C-c` (you probably want to bind this to something easier).


### SBT Version

Your `project/build.properties` needs to use a version newer than 0.13.5 of sbt due to a [breaking AutoPlugin change](https://github.com/ensime/ensime-server/issues/672), e.g.

```
sbt.version=0.13.12
```


## Contributing

You can check what runs in the CI by investigating the `.drone.yml`, `appveyor.yml` and `.travis.yml` files. These should give you a good feel for what to run locally.

When submitting a PR, we expect an accompanying test in the `sbt-test` folder. These use the [sbt scripted](http://eed3si9n.com/testing-sbt-plugins) plugin and you can start by copying one of the existing tests (use symbolic links instead of copying files).

To try your build locally, use `sbt publishLocal` (which will also happen as part of running `sbt scripted`) and make your required `sbt-ensime` version match that of the snapshot you are building. Remember to nuke your `~/.ivy2/local` once the fix is merged and published upstream.

Feel free to ask questions on the github issue tracker or [gitter.im/ensime/ensime-server](https://gitter.im/ensime/ensime-server) (there is no dedicated chat room for `sbt-ensime`).

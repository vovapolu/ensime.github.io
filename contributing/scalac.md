---
layout: page
order: 2
title: scalac from ENSIME
---

The following is information on how to use ENSIME to make changes to the Scala compiler and/or standard library.

## 2.11.x or 2.12.x?

Below we assume you are hacking Scala 2.11.x, which is built using `ant`.

A volunteer is required to [add support for hacking Scala 2.12.x](https://github.com/ensime/ensime-sbt/issues/180), which is built using `sbt`.

## Sample configuration

ENSIME does not compile sources to `.class` files: running `ant` is still required to produce output.

Included here is a sample `.ensime` file which can be used as the basis of a configuration for working on scala itself, and a reminder of some workflow aspects that must be kept in mind. In particular the use of the custom `:source-mode` feature.

Paths must be absolute, so you will need to customise this sample for your environment: after running `ant init` (sources will only be downloaded only if [commit `0de051`](https://github.com/typelevel/scala/commit/0de051d825111ee090be5314fc80da32e17ad6a4) has been applied) this should be as simple as performing a search and replace on `BASE`, `M2_REPO` and `IVY_HOME` with your paths.

To speed things up and reduce memory/CPU overhead, delete the downstream modules that you're not interested in.

## Binary Compatibility

ENSIME uses the same version of the presentation compiler as is used by the project, therefore a build of ENSIME for the specified `:scala-version` must exist.

When working on maintenance branches of scala, it should be as simple as using the last stable release of scala (on that branch) as the version number. In this mode, ENSIME will expect `.class` files to exist in the `build/quick` (produced by a quick build).

However, when working on development branches it is unlikely that a version of ENSIME will be available: so use the most recent stable release. In this case, ENSIME will fail horribly when attempting to read the `.class` files (e.g. the pickle format may have changed), so delete all the `:targets` settings and type `C-c C-c a` (`ensime-typecheck-all`) when starting your session to use "source only" mode. It may take several minutes for typechecking to complete, and there will be many false negative warnings. Warnings that are a result of new language features cannot be fixed. For what remains, open up the `interactive` module and fix some bugs in the presentation compiler :-P

## `.ensime`

```elisp
(:root-dir "BASE"
 :cache-dir "BASE/.ensime_cache"
 :name "scala"
 :java-home "/opt/jdk1.6.0_45"
 :reference-source-roots ("/opt/jdk1.6.0_45/src.zip")
 :scala-version "2.11.8"
 :scala-compiler-jars ("IVY_HOME/cache/org.scala-lang/scala-compiler/jars/scala-compiler-2.11.7.jar" "IVY_HOME/cache/org.scala-lang/scala-library/jars/scala-library-2.11.7.jar" "IVY_HOME/cache/org.scala-lang/scala-reflect/jars/scala-reflect-2.11.7.jar" "IVY_HOME/cache/org.scala-lang/scalap/jars/scalap-2.11.7.jar")
 :java-flags ("-XX:MaxPermSize=256m" "-Xss2m" "-Xmx2g")
 :compiler-args ("-encoding" "UTF-8" "-feature" "-deprecation" "-Ymacro-expand:discard")
 :formatting-prefs nil
 :disable-source-monitoring nil
 :disable-class-monitoring nil
 :source-mode t
 :subprojects (
               (:name "asm"
                      :depends-on-modules nil
                      :source-roots ("BASE/src/asm")
                      :targets ("BASE/build/asm/classes"))
               (:name "forkjoin"
                      :depends-on-modules nil
                      :source-roots ("BASE/src/forkjoin")
                      :targets ("BASE/build/libs/classes/forkjoin"))
               (:name "library"
                      :depends-on-modules ("asm" "forkjoin")
                      :source-roots ("BASE/src/library"
                                     "BASE/test/junit")
                      :targets ("BASE/build/quick/classes/library")
                      :test-targets ("BASE/build/junit/classes")
                      :compile-deps ("M2_REPO/junit/junit/4.10/junit-4.10.jar"
                                     "M2_REPO/org/hamcrest/hamcrest-core/1.1/hamcrest-core-1.1.jar")
                      :reference-source-roots ("M2_REPO/junit/junit/4.10/junit-4.10-sources.jar"
                                               "M2_REPO/org/hamcrest/hamcrest-core/1.1/hamcrest-core-1.1-sources.jar"))
               (:name "reflect"
                      :depends-on-modules ("library")
                      :source-roots ("BASE/src/reflect")
                      :targets ("BASE/build/quick/classes/reflect"))
               (:name "compiler"
                      :depends-on-modules ("reflect")
                      :source-roots ("BASE/src/compiler")
                      :targets ("BASE/build/classes")
                      :compile-deps ("M2_REPO/org/apache/ant/ant/1.8.4/ant-1.8.4.jar")
                      :reference-source-roots ("M2_REPO/org/apache/ant/ant/1.8.4/ant-1.8.4-sources.jar"))
               (:name "repl"
                      :depends-on-modules ("compiler")
                      :source-roots ("BASE/src/repl")
                      :targets ("BASE/build/quick/classes/repl")
                      :compile-deps ("M2_REPO/jline/jline/2.12/jline-2.12.jar")
                      :reference-source-roots ("M2_REPO/jline/jline/2.12/jline-2.12-sources.jar"))
               (:name "scalap"
                      :depends-on-modules ("compiler")
                      :source-roots ("BASE/src/scalap")
                      :targets ("BASE/build/scalap/classes"))
               (:name "actors"
                      :depends-on-modules ("library")
                      :source-roots ("BASE/src/actors")
                      :targets ("BASE/build/actors/classes"))
               (:name "partest"
                      :depends-on-modules ("repl")
                      :source-roots ("BASE/src/partest-extras"
                                     "BASE/src/partest-javaagent")
                      :targets ("BASE/build/quick/classes/partest-extras"
                                "BASE/build/quick/classes/partest-javaagent")
                      :compile-deps ("M2_REPO/com/googlecode/java-diff-utils/diffutils/1.3.0/diffutils-1.3.0.jar"
                                     "M2_REPO/org/scala-sbt/test-interface/1.0/test-interface-1.0.jar"
                                     "M2_REPO/org/apache/ant/ant-launcher/1.8.4/ant-launcher-1.8.4.jar")
                      :reference-source-roots ("M2_REPO/com/googlecode/java-diff-utils/diffutils/1.3.0/diffutils-1.3.0-sources.jar"
                                               "M2_REPO/org/scala-sbt/test-interface/1.0/test-interface-1.0-sources.jar"
                                               "M2_REPO/org/apache/ant/ant-launcher/1.8.4/ant-launcher-1.8.4-sources.jar"))
               (:name "scaladoc"
                      :depends-on-modules ("partest")
                      :source-roots ("BASE/src/scaladoc")
                      :targets ("BASE/build/scaladoc/classes")
                      :compile-deps ("M2_REPO/org/scala-lang/plugins/scala-continuations-library_2.11/1.0.2/scala-continuations-library_2.11-1.0.2.jar"
                                     "M2_REPO/org/scala-lang/plugins/scala-continuations-plugin_2.11.8/1.0.2/scala-continuations-plugin_2.11.8-1.0.2.jar"
                                     "M2_REPO/org/scala-lang/modules/scala-parser-combinators_2.11/1.0.2/scala-parser-combinators_2.11-1.0.2.jar"
                                     "M2_REPO/org/scala-lang/modules/scala-swing_2.11/1.0.1/scala-swing_2.11-1.0.1.jar"
                                     "M2_REPO/org/scala-lang/modules/scala-xml_2.11/1.0.2/scala-xml_2.11-1.0.2.jar"
                                     )
                      :reference-source-roots ("M2_REPO/org/scala-lang/plugins/scala-continuations-library_2.11/1.0.2/scala-continuations-library_2.11-1.0.2-sources.jar"
                                               "M2_REPO/org/scala-lang/plugins/scala-continuations-plugin_2.11.8/1.0.2/scala-continuations-plugin_2.11.8-1.0.2-sources.jar"
                                               "M2_REPO/org/scala-lang/modules/scala-parser-combinators_2.11/1.0.2/scala-parser-combinators_2.11-1.0.2-sources.jar"
                                               "M2_REPO/org/scala-lang/modules/scala-swing_2.11/1.0.1/scala-swing_2.11-1.0.1-sources.jar"
                                               "M2_REPO/org/scala-lang/modules/scala-xml_2.11/1.0.2/scala-xml_2.11-1.0.2-sources.jar"))
               (:name "interactive"
                      :depends-on-modules ("scaladoc")
                      :source-roots ("BASE/src/interactive")
                      :targets ("BASE/build/interactive/classes"))
               ))
```

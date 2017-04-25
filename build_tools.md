---
layout: page
order: 7
title: Supported Build Tools
site_nav_entry: true # this is an entry in the main site nav
---

[sbt]: http://www.scala-sbt.org
[sbtI]: http://www.scala-sbt.org/assets/typesafe_sbt_svg.svg
[cbt]: https://github.com/cvogt/cbt
[pants]: https://pantsbuild.github.io/
[pantsI]: https://pantsbuild.github.io/logo.ico
[lein]: http://leiningen.org/
[leinI]: public/ensime-leiningen-logo.png
[mvn]: https://maven.apache.org/
[mvnI]: https://maven.apache.org/images/maven-logo-black-on-white.png
[gradle]: http://gradle.org/
[gradleI]: public/ensime-gradle-logo.png

- [sbt](sbt) ([homepage][sbt])
- [CBT](cbt) ([homepage][cbt])
- [Pants](pants) ([homepage][pants])
- [Leiningen](lein) ([homepage][lein])
- [Maven](maven) ([homepage][mvn])
- [Gradle](gradle) ([homepage][gradle])
- [Manual](manual)

## Feature Matrix

The following chart describes how well ENSIME supports each build tool:

| Learn more →           | [sbt](sbt)          | [CBT](cbt) | [Pants](pants)            | [Leiningen](lein)           | [Maven](maven)        | [Gradle](gradle)             | [Manual](manual) |
| ---------------------- | ------------------- | ---------- | ------------------------- | --------------------------- | --------------------- | ---------------------------- | ---------------- |
| Homepage               | [![sbt][sbtI]][sbt] | [CBT][cbt] | [![Pants][pantsI]][pants] | [![Leiningen][leinI]][lein] | [![Maven][mvnI]][mvn] | [![Gradle][gradleI]][gradle] | -                |
| Upstream Licence       | BSD-3               | Apache 2.0 | Apache 2.0                | EPL                         | Apache 2.0            | Apache 2.0                   | -                |
| Recommended            | ✔                   |            |                           |                             |                       |                              |                  |
| `.ensime` project file | ✔                   |            |                           |                             | ✔                     | ✔                            | ✔                |
| source fetching        | ✔                   |            |                           |                             | ✔                     | ✔                            |                  |
| docs fetching          | ✔                   |            |                           |                             | ✔                     | ✔                            |                  |
| launch manager         | ✔                   |            |                           |                             |                       |                              |                  |
| debug launcher         | ✔                   |            |                           |                             |                       |                              |                  |
| single file compile    | ✔                   |            |                           |                             |                       |                              |                  |
| formatting             | ✔                   |            |                           |                             |                       | ✔                            |                  |

---
layout: section
order: 10
title: Manual
---

Not recommended except in dire circumstances or if you're implementing support in a new build tool.

You can create an `.ensime` manually.

The schema of the `.ensime` file is defined in [`org.ensime.api.EnsimeConfig`](https://github.com/ensime/ensime-server/blob/2.0/api/src/main/scala/org/ensime/api/config.scala) and examples are available in [`EnsimeConfigSpec.scala`](https://github.com/ensime/ensime-server/blob/2.0/core/src/test/scala/org/ensime/config/EnsimeConfigSpec.scala) (you can also get substantial examples by running `sbt ensimeConfig` against a supported project, such as `ensime-server` itself).

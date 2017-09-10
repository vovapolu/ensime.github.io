---
layout: page
order: 10
title: Server
site_nav_entry: true # this is an entry in the main site nav
---

As of version 2.0.0, the `ensime-server` process can be customised, both at a user and a project level via `.ensime-server.conf` HOCON files in your project's directory or your home directory. Project configuration takes priority over user settings, which take priority over [the defaults](https://github.com/ensime/ensime-server/blob/2.0/core/src/main/resources/application.conf).

For example, to customise organise imports to have specific orderings and wildcard rules, use

```
ensime {
  imports {
    locals = true
    groups = ["java", "scala", "scalaz,simulacrum,stalactite", "*", "org.ensime"]
    wildcards = ["scalaz", "scalaz.Scalaz"]
    collapseExclude = ["scala"]
    maxIndividualImports = 4
  }
  index {
    batchSize = 100
  }
}
```

and if you have lots of heap to burn, try increasing the batch size of the indexer

```
ensime {
  index {
    batchSize = 100
  }
}
```

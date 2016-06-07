---
layout: section
order: 4
title: Maven
---

This maven plugin generates a `.ensime` file and provides various convenience commands for interacting with [ENSIME](http://github.com/ensime/ensime-server). The source code can be found at in it's own project: [ensime-maven](https://github.com/ensime/ensime-maven/).

# ENSIME Maven Plugin

This [maven](https://maven.apache.org/) plugin generates a `.ensime` file for use with an [ENSIME server](http://github.com/ensime/ensime-server).

## Installation

Configure your `~/.m2/settings.xml` file so that maven is aware of the plugin group `org.ensime.maven.plugins`:

```xml
  <pluginGroups>
    <pluginGroup>org.ensime.maven.plugins</pluginGroup>
  </pluginGroups>
```

## Generate `.ensime` file

### (Optional) Download project sources and javadocs

The ensime-maven plugin will tell ensime about the location of source and javadoc jars, but won't automatically download them for you. You can get maven to do this by running:

```
mvn dependency:sources dependency:resolve -Dclassifier=javadoc
```

### Generate the `.ensime` file

To actually generate the `.ensime` file from your pom, run:

```
mvn ensime:generate
```

### (Optional) Initial project compilation

To prevent some surprises when working with a new project in ensime, do a full compile before starting up ensime for the first time:

```
mvn compile test-compile
```

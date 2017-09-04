---
layout: section
order: 4
title: Maven
---

This maven plugin generates a `.ensime` file and provides various convenience commands for interacting with [ENSIME](http://github.com/ensime/ensime-server). The source code can be found at in it's own project: [ensime-maven](https://github.com/ensime/ensime-maven/).

If you wish to use the Developer Version of ENSIME, you may need to run an unreleased version of the plugin.  See [Contributing](#contributing) for details.

# ENSIME Maven Plugin

This [maven](https://maven.apache.org/) plugin generates a `.ensime` file for use with an [ENSIME server](http://github.com/ensime/ensime-server).

## Installation

Configure your `~/.m2/settings.xml` file so that maven is aware of the plugin group `org.ensime.maven.plugins`:

```xml
<build>
  <pluginGroups>
    <pluginGroup>org.ensime.maven.plugins</pluginGroup>
  </pluginGroups>
</build>
```

Or you can add the following to your `pom` file:

```xml
<distributionManagement>
  <snapshotRepository>
    <id>sonatype-nexus-snapshots</id>
    <url>https://oss.sonatype.org/content/repositories/snapshots</url>
  </snapshotRepository>
  <repository>
    <id>sonatype-nexus</id>
    <url>https://oss.sonatype.org/service/local/staging/deploy/maven2/</url>
  </repository>
</distributionManagement>

<build>
<plugins>
  <plugin>
    <groupId>org.ensime.maven.plugins</groupId>
    <artifactId>ensime-maven</artifactId>
    <version>1.2.0</version>
  </plugin>
</plugins>
</build>
```
Note usually you don't need to add **DistributionManagement** part.

The default ensime server version is 2.0.0-M4, but you can customize it like:

```
<configuration>
    <ensimeServerVersion>2.0.0-M4</ensimeServerVersion>
<configuration>
```

## Generate `.ensime` file

To actually generate the `.ensime` file from your pom, run:

```
mvn ensime:generate
```


## Format the Scala sources

Format `.scala` files using Scalariform settings (compatible with, but does not require, `maven-scalariform` plugin).

```
mvn ensime:scalariform
```

You can customize it by passing the `salariform` settings to this plugin's `configuration`:

```xml
<plugin>
  <groupId>org.ensime.maven.plugins</groupId>
  <artifactId>ensime-maven</artifactId>
  <version>1.2.0</version>
  <configuration>
    <indentSpaces>2</indentSpaces>
  </configuration>
</plugin>
```
For the list of options and the default settings, please refer to the `maven-scalariorm` [plugin](https://github.com/mdr/scalariform-maven-plugin).

## Contributing

The source code is available at https://github.com/ensime/ensime-maven.  To use a locally built version of the plugin, first build and install it:

```
mvn -Dgpg.skip install
```

Then run it with:

```
mvn org.ensime.maven.plugins:ensime-maven:1.3.0-SNAPSHOT:generate
```

(substituting the latest version number if necessary)

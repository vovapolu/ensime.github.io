---
layout: section
order: 2
title: Installation
---

## Prerequisites

Before you start make sure you have:

- [installed sbt][sbt];
- [generated a `.ensime` file][ensimeConfig] for your project;
- [installed Sublime Text][sublime].

## Installing via Package Control

The recommended way to install *ENSIME Sublime* is via [Package Control][package-control] (which is a must-have tool anyway):

1. [install Package Control][package-control-install];

2. open the Command Palette in Sublime Text (`Ctrl+Shift_P`);

3. type/select *"Package Control: Install Package"* and press *Enter*;

4. After a few seconds a second command palette will appear, asking you which package you'd like to install. Type/select *"Ensime"* and press *Enter*.

Sublime Text and ENSIME Sublime should now be correctly configured. The next step is to install ENSIME sbt.

## Launching ENSIME

Once you have [a `.ensime` file][ensimeConfig] for your project, start an ENSIME session from within Sublime Text as follows:

1. Open the root folder of your project (the one containing the `.ensime` file) in Sublime Text. If you are already viewing a project file in Sublime, you can open the root folder by selecting *Project Menu / Add Folder to Project...* and selecting the project root directory.

2. Next you need to add sbt to your Sublime path, within Sublime Text, go to the Preferences > Package Settings > Settings > Ensime and select Settings - User to open the Ensime.sublime-settings file. Now add the following to this file.

~~~json
{
  "sbt_binary": "/path/to/sbt"
}
~~~

3. [Optional] You may find it helpful to open the console view to see the output and when dependencies are downloaded upon starting Ensime. You do this in the Sublime View menu and selecting Show Console.

4. Choose *"Ensime: Startup"* from the Sublime Text command palette (*Tools Menu / Command Palette...*).

   If this menu item doesn't appear, check *No Commands in the Command Palette?* in the [Troubleshooting][troubleshooting] section.

5. The first time you start ENSIME it will take a few minutes to download dependencies and get set up (it'll be much faster on subsequent runs).

   If you get an error message saying Ensime can't find sbt on your PATH, you can manually specify the location in your preferences. Check the [Troubleshooting][troubleshooting] section for details.

   How do you tell when it's initialised?
   Open one of your scala source files and break the code by simply adding a whitespace to a function or class name and then save the file, you will then see the error highlighted within Sublime Text.

   Open a Scala file and [verify that ENSIME is working][features].

## Trouble Getting It Working?

See the [troubleshooting page][troubleshooting] and [chat to us on Gitter][gitter]!



[features]: ../features
[ensimeConfig]: /build_tools/sbt/
[gitter]: https://gitter.im/ensime/ensime-sublime
[sbt]: http://www.scala-sbt.org/download.html
[sublime]: http://sublimetext.com
[troubleshooting]: ../troubleshooting
[package-control]: https://packagecontrol.io/packages/Ensime
[package-control-install]: https://packagecontrol.io/installation

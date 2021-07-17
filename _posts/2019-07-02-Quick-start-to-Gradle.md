---
layout: post
title: Quick start to Gradle
---

![](/images/migrated/1__Y__THGNMyaMSRwQ8KIeg4Xg__2x.png)

We recently migrated the ballerina build system to Gradle due to the performance issues we had with maven. Building with Gradle is significantly faster than [maven](https://gradle.org/gradle-vs-maven-performance/). We found it much more flexible to write build scripts with groovy.

### Gradle wrapper — No installation hassle

It is the recommended way to do a Gradle build. Gradle wrapper script makes sure the build is invoked in the preconfigured Gradle version. It will download Gradle in the initial run.

### Gdub is your friend — No more ‘../../../gradlew build’

Thanks to Gradle wrapper we do not need to install Gradle, but we have to point out to `gradlew` whenever we do a build. If we want to build only a project submodule [gdub](http://www.gdub.rocks/) is a very helpful tool to have.

### Build lifecycle

There are 3 phases in a Gradle build.

1.  Initialization

Gradle determines which projects are going to take part in the build.

2\. Configuration

The build scripts of **all** projects which are part of the build are executed in this phase.

3\. Execution

Gradle determines the subset of the tasks, created and configured during the configuration phase, to be executed. Gradle then executes each of the selected tasks.

### Gradle tasks tree

You can declare tasks that depend on other tasks. For example, a simple java project gradle tasks hierarchy will look like this.

```
:build+--- :assemble|    \--- :jar|         \--- :classes|              +--- :compileJava|              \--- :processResources\--- :check     \--- :test          +--- :classes          |    +--- :compileJava          |    \--- :processResources          \--- :testClasses               +--- :compileTestJava               |    \--- :classes               |         +--- :compileJava               |         \--- :processResources               \--- :processTestResources
```

### Skipping tasks

Add -x and pass the task name. You can skip multiple tasks as well.

gw build -x test -x npmBuild

### Build with no task optimizations/caching

gw build --rerun-tasks

### Build with no-cache

gw build --no-build-cache

### Build scans

Build scans are helpful to optimize your Gradle build. It is a shareable record of a build that provides insights into what happened and why.

gw build --scan

### Verbose builds

gw build --info
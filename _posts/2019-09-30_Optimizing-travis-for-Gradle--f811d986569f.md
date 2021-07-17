---
title: Optimizing travis for Gradle.
---

![](/images/migrated/1__KYfO6ZWA9uc9J4ynkTxKug.png)

In this guide I will describe how to integrate and optimize travis CI to your gradle project. Before we begin, we need to enable and caching and parallel for our gradle project.

In order to enable those, simply put

org.gradle.caching=true  
org.gradle.parallel=true

in your gradle.properties file.

Let’s begin configuring travis with a simple example.

The following configuration file tells Travis CI to build a Java project with JDK 8.

language: java  
install: true  
os: linux  
dist: trusty  
jdk: oraclejdk8  
script:  
 - ./gradlew build --scan

### Enable travis Cache

You can cache your gradle build with travis by using following configurations.

before\_cache:  
  - rm -f  $HOME/.gradle/caches/modules-2/modules-2.lock  
  - rm -fr $HOME/.gradle/caches/\*/plugin-resolution/  
  
cache:  
  directories:  
    - $HOME/.gradle/caches/  
    - $HOME/.gradle/wrapper/

### Disable gradle daemon

Having gradle daemon makes faster builds for subsequent builds. But this has no benefit in CI/CD environments.

\- ./gradlew build --scan --no-daemon

### Create Build stages

Build stages is a way to group jobs, and run jobs in each stage in parallel, but run one stage after another sequentially.

The gradle cache from one stage will be used as cache for next stage. In this example we can run two tests gradle tasks on top of `assemble` build stage.

```
jobs:  include:    - stage: assemble      script: 
```

### Conclusion

Integrating Travis with Gradle is fairly straightforward. We can use caching and build stages to optimize Gradle build in Travis.

As further optimizations, you can use Gradle features like build scans and follow suggestions guide in the report.
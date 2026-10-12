---
name: skill-jvm
description: Best practices for working with JVM-based applications, such as choosing the Java version for builds and runtimes. Use when creating, configuring, upgrading, or reviewing Java or Spring Boot projects.
---

# JVM best practices

Apply these conventions as defaults. Follow explicit user requirements and
established target-repository conventions when they conflict. Do not migrate an
existing project solely to enforce a default without approval.

## Java Version

Read [ADR 01](docs/adr/01-use-jdk-in-lts-version.md) when choosing or upgrading
the JDK version. Use only LTS releases of the JDK. Do not adopt non-LTS releases,
even when they offer new features.

Read [ADR 02](docs/adr/02-use-java-25-as-default.md) when creating a new project
or configuring build toolchains. Use Java 25 as the default version.

For Gradle, declare the toolchain:

```kotlin
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(25)
    }
}
```

For Maven, set the release version:

```xml
<properties>
    <maven.compiler.release>25</maven.compiler.release>
</properties>
```

If a project targets an older Java version, identify the version and suggest
upgrading to the default. Do not perform the upgrade without approval.

## Validate the Result

Verify the active JDK with `java -version` before building. Run the project's
existing build and test commands, such as `./gradlew build` or `./mvnw verify`,
and report failures instead of reporting a successful change.

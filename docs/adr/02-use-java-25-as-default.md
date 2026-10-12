# Use Java 25 as Default

## Context

Without an explicit default Java version, JVM projects tend to drift across different versions, which complicates tooling, upgrades, and shared guidance.

We use only Long Term Support (LTS) JDK versions, as described in
[Use JDK in LTS Version](01-use-jdk-in-lts-version.md).

Java 25 is the latest LTS release. It includes language and runtime improvements
delivered since Java 21, such as scoped values, flexible constructor bodies,
module import declarations, compact source files, and compact object headers.

Many of our JVM projects use Spring Boot. Current Spring Boot releases support
Java 25, and the Spring ecosystem actively adopts features of recent Java
releases, such as virtual threads.

## Decision

We will use Java 25 as the default Java version for new projects and for
guidance in this repository.

We will always target the latest LTS Java release. When the next LTS release
becomes available and is supported by our key frameworks, we will revisit this
decision and move the default forward.

For example, a Gradle build declares the toolchain like this:

```kotlin
java {
    toolchain {
        languageVersion = JavaLanguageVersion.of(25)
    }
}
```

A Maven build sets the release version like this:

```xml
<properties>
    <maven.compiler.release>25</maven.compiler.release>
</properties>
```

## Consequences

Positive consequences:

- Projects get long-term updates and security fixes without upgrading every six
  months.
- Developers can use modern language features and runtime improvements
  delivered up to Java 25.
- Spring Boot projects run on a Java version that the framework supports and
  actively optimizes for.
- A single default version simplifies build configuration, CI setup, container
  images, and shared documentation.

Negative consequences:

- Some third-party libraries, tools, or plugins may lag behind Java 25 support,
  which can block or delay adoption in specific projects.
- Existing projects on older Java versions need migration work to align with
  the default.
- Environments with older Java runtimes cannot run Java 25 bytecode, so
  deployment targets must be upgraded as well.
- Features introduced in non-LTS releases after Java 25 are unavailable until
  the next LTS release becomes the default.

## Alternatives Considered

**Java 21**. Java 21 is the previous LTS release and has broad ecosystem
support. It was not selected because it lacks the improvements delivered in
Java 25 and has a shorter remaining support window.

**Latest non-LTS release**. Using the newest feature release gives access to the
newest features. It was not selected because each non-LTS release is supported
only for six months, which forces frequent upgrades across all projects.

**No default version**. Letting each project choose its own Java version gives
maximum flexibility. It was not selected because it leads to inconsistent
tooling and guidance, and makes shared skills harder to maintain.

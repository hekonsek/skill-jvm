# Use JDK in LTS Version

## Context

Projects built with this repository's skills need a clear policy for which JDK
versions they use. The JDK version affects source code, build toolchains, CI
pipelines, container images, and production runtimes.

Java ships a new feature release every six months. Every two years, one of
these releases is a Long Term Support (LTS) release. LTS releases receive
security patches and bug fixes for several years. Non-LTS releases receive
updates only until the next feature release, which is about six months.

Running an unsupported JDK exposes projects to unpatched security
vulnerabilities. Staying on supported non-LTS releases requires upgrading every
six months, which is a significant ongoing cost across many projects.

The wider ecosystem is centered on LTS releases. Frameworks such as Spring
Boot, build tools, IDEs, libraries, cloud providers, and base container images
test against and support LTS releases first, and keep supporting them longest.

## Decision

We will use only LTS versions of the JDK for building and running projects.

We will not adopt non-LTS releases for projects, even when they offer new
features. Upgrades happen from one LTS release to the next, on a schedule we
can plan ahead of time.

The specific default LTS version is recorded in a separate ADR.

## Consequences

Positive consequences:

- Projects receive security patches and bug fixes for years without frequent
  upgrades.
- Upgrades become predictable, because a new LTS release arrives every two
  years.
- Projects benefit from the broadest support across frameworks, tools,
  libraries, and cloud platforms.
- Documentation, tutorials, and developer experience most commonly target LTS
  releases, which eases onboarding.
- Preview features from non-LTS releases are often finalized by the next LTS
  release, so projects rely only on stable features.

Negative consequences:

- Features introduced in non-LTS releases are unavailable until the next LTS
  release, which can mean waiting up to two years.
- Each LTS upgrade covers two years of changes at once, which can make
  migrations larger than incremental upgrades would be.
- Performance and runtime improvements from non-LTS releases arrive later.
- Long support windows can tempt teams to postpone upgrades until an LTS release
  approaches its end of support.

## Alternatives Considered

**Always use the latest feature release**. This gives immediate access to new
language features and runtime improvements. It was not selected because each
release is supported only for about six months, forcing frequent upgrades
across all projects.

**Let each project choose its JDK version**. This gives teams maximum
flexibility. It was not selected because it leads to inconsistent tooling, mixed
support windows, and guidance that is harder to share and maintain.

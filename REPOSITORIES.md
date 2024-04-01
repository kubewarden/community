# REPOSITORIES.md

This document outlines the criteria, scope, and status of the repositories
within the [Kubewarden GitHub organization](https://github.com/kubewarden).

## Criteria

Repositories in the Kubewarden organization are dedicated to various aspects of
the project, including its core codebase, documentation, tools, libraries, and
subprojects. Each repository is expected to strictly pertain to Kubewarden's
ecosystem or its operational needs.

### Code Ownership

Each repository must include a CODEOWNERS file in the root directory, following
[GitHub's format
specification](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners).
This file identifies individuals responsible for different parts of the
repository to streamline the review process.

### License

All content within the repositories must be licensed under the [Apache License,
Version 2.0](https://www.apache.org/licenses/LICENSE-2.0). A LICENSE file must
be present in the root of each repository to comply with this requirement.

## Scope

The scope of a repository delineates its role and responsibilities within the
Kubewarden project, as determined and potentially revised by Core Maintainers.
Below, each scope is expanded upon to offer a clearer picture of its
significance and purpose. 

### Core Scope
[![Kubewarden Core Repository](./badges/kubewarden-core.svg)](#core-scope)

Repositories within the Core Scope are the essential building blocks of the
Kubewarden project. They include the project's fundamental codebase, such as
the APIs, primary libraries, and the core components required for Kubewarden's
operation. These repositories are crucial for the development, deployment, and
running of Kubewarden, serving as the primary resources that adopters interact
with. Core Scope repositories must exhibit high standards of reliability,
security, and performance to ensure the stability of Kubewarden as a whole.

### Infra Scope
[![Kubewarden Infra Repository](./badges/kubewarden-infra.svg)](#infra-scope)

Infra Scope repositories are dedicated to supporting the project's underlying
infrastructure. This scope includes tools and services for continuous
integration and delivery (CI/CD), monitoring, logging, and any other
operational tools that facilitate the development and maintenance of
Kubewarden. While these repositories might not directly contribute to the
project's functionality from an end-user perspective, they are indispensable
for the project's health, efficiency, and scalability.


### Policy Scope
[![Kubewarden Policy Repository](./badges/kubewarden-policies.svg)](#policy-scope)

The Policies Scope encompasses repositories that contain specific policies
designed for execution within the Kubewarden framework. These policies can
cover a wide range of security, compliance, and governance checks applicable to
Kubernetes clusters. Repositories in the Policies Scope are critical for
enabling users to enforce best practices, regulatory requirements, and
organizational policies within their Kubernetes environments. They represent
the actionable components of Kubewarden, allowing for the customization and
extension of Kubernetes security and management.

### Special Scope

Special Scope repositories include those that do not fit neatly into the other
defined scopes. This category can cover a broad range of repositories,
including but not limited to, community engagement tools, documentation
websites, experimental projects, and any forks or mirrors of external projects
that are relevant to Kubewarden. These repositories might serve niche purposes
or support the project's ecosystem in unique and valuable ways. While they may
not directly contribute to the core functionality of Kubewarden, they play a
role in the project's overall health, growth, and community engagement.

## Status

The status of each repository within the Kubewarden project signifies its
current maturity and development phase, as periodically assessed by Core
Maintainers. This classification aids users in understanding the expected
stability, support level, and usage recommendations for each repository.

### Stable
[![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)

Stable status is assigned to repositories that have reached a peak level of
maturity, making them dependable for production environments. These
repositories benefit from regular maintenance, updates, and rigorous testing
processes to guarantee their reliability and performance. Stable repositories
are the cornerstone of Kubewarden, providing well-documented, thoroughly tested
components.

### Incubating
[![Incubating](https://img.shields.io/badge/status-incubating-orange?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#incubating)

Incubating repositories are actively being developed and may experience
significant modifications as they evolve. They represent the middle ground in
the maturity spectrum, where the foundational ideas and functionalities are
being refined and expanded. While incubating repositories hold the potential to
graduate to stable status, they are currently in a state where their use in
critical production environments should be approached with caution, as features
and APIs may change.

### Sandbox
[![Sandbox](https://img.shields.io/badge/status-sandbox-red?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#sandbox)

Sandbox repositories are at the forefront of innovation within the Kubewarden
project, embodying the initial stages of development. They serve as a breeding
ground for new ideas and experimental features, offering a space to experiment,
provide feedback, and shape the project's future directions. While promising,
these repositories are not yet mature or stable enough for production use and
are best explored in testing or development environments.

### Deprecated

Deprecated repositories have been phased out of active development and
maintenance, effectively serving as archives. They may have been superseded by
more advanced technologies or concepts within the project or no longer align
with the project's direction. While they remain accessible for historical
interest, their contents are outdated, and they are not recommended for any
practical application.

## Core Maintainers' Responsibilities

Core Maintainers are pivotal to the governance of the Kubewarden organization,
holding responsibilities that include:

- Assigning or revoking the _core_ status of repositories.
- Maintaining _special_ repositories.
- Managing non-functioning or abandoned repositories.
- Resolving disputes within the organization.

Maintainers are expected to act in the best interest of the entire Kubewarden
community and organization.

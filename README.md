[![CLOMonitor](https://img.shields.io/endpoint?url=https://clomonitor.io/api/projects/cncf/kubewarden/badge)](https://clomonitor.io/projects/cncf/kubewarden)
[![CNCF Landscape](https://img.shields.io/badge/CNCF%20Landscape-5699C6)](https://landscape.cncf.io/?item=provisioning--security-compliance--kubewarden)

Kubewarden is an open source security project, hosted by the CNCF. As a
[vendor neutral](https://contribute.cncf.io/maintainers/community/vendor-neutrality/)
project, we welcome a broad range of contributions.

This repository aims to document the evolution process of The Kubewarden
Project.

It provides a space for the community to work together, discuss ideas, and
document processes. It is also a place to make decisions that regard the whole
[Kubewarden](https://github.com/kubewarden) organization and define rules and
structures that span beyond the extent of a single repository.

**Table of Contents**

- [Quickstart](#quickstart)
- [Code Of Conduct](#code-of-conduct)
- [Maintainers](#maintainers)
- [Roadmap](#roadmap)
- [Community](#community)
- [Contributing](#contributing)
- [Repositories](#repositories)
  - [Repositories Guidelines](./REPOSITORIES.md)
  - [Core](#core)
  - [Infra](#infra)
  - [Policies](#policies)
  - [Special](#special)
  - [Archived](#archived)

## Quickstart

We recommend you read our Quickstart page at [docs.kubewarden.io](https://docs.kubewarden.io/quick-start)
to get familiarized with Kubewarden and what it aims to achieve. From then,
feel free explore the full documentation to understand all its features.

## Code Of Conduct

We follow the [CNCF Code of
Conduct](https://github.com/cncf/foundation/blob/main/code-of-conduct.md).

To report an issue, please contact
[cncf-kubewarden-maintainers@lists.cncf.io](mailto:cncf-kubewarden-maintainers@lists.cncf.io)
or any of the individual members of the [CNCF Code of Conduct
Committee](https://www.cncf.io/conduct/committee/) to submit your report. For
more detailed instructions on how to submit a report, including how to submit a
report anonymously, please see our [Incident Resolution
Procedures](https://github.com/cncf/foundation/blob/main/code-of-conduct/coc-incident-resolution-procedures.md).
You can expect a response within three business days.

## Maintainers

You can find the list of current maintainers in the
[MAINTAINERS.md](./MAINTAINERS.md) file.

## Roadmap

Information about our roadmap process is available in the [ROADMAP.md](./ROADMAP.md) file.

## Community

Get in contact with us:

- Slack: [#kubewarden](https://kubernetes.slack.com/archives/kubewarden) and [#kubewarden-dev](https://kubernetes.slack.com/archives/kubewarden-dev).
- GitHub discussions in this repository.
- Maintainers mailing list: `cncf-kubewarden-maintainers`, followed by `@`, followed by `lists.cncf.io`

### Community meeting

We host regular online meetings for contributors, adopters, maintainers, and
anyone else interested. These meetings usually take place on the second Thursday
of the month at 4 PM UTC.

- [Zoom link](https://zoom.us/j/92928111886)
- [Minutes from earlier meetings](https://docs.google.com/document/d/1TgPIFKygkR2_vViCSfBEzwDDactfTcedc9fc4AeVJ9w/edit#)

We're a friendly group, so please feel free to join us!

## Contributing

See the [contributing
guide](https://github.com/kubewarden/community/blob/main/CONTRIBUTING.md) and
the [code of conduct](./CODE_OF_CONDUCT.md).

## Security policy

See the [security policy](./SECURITY.md) for more information about how to report
any security issues.

## Repositories

The Kubewarden Project applies a straightforward **adoption model** for its
repositories. Each repository is given a _[scope](./REPOSITORIES.md#scope)_,
which outlines its purpose, and a _[status](./REPOSITORIES.md#status)_ that
indicates its maturity level.

For more detailed information, please refer to the
[REPOSITORIES.md](./REPOSITORIES.md) file.

In the sections that follow, we present the repositories, grouped by their
_scope_.

Furthermore, some of the roles of the components listed below are described in the
[components.md](./components.md) file.

### Core

[![Kubewarden Core
Repository](./badges/kubewarden-core.svg)](./REPOSITORIES.md#core-scope)

Core repositories, are critically important as they are essential for building,
installing, running and using Kubewarden.

| NAME                                                                                    | STATUS                                                                                                                                                            | DESCRIPTION                                                                                                |
| --------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| [kubewarden/kubewarden-controller](https://github.com/kubewarden/kubewarden-controller) | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Manage admission policies in your Kubernetes cluster with ease                                             |
| [kubewarden/policy-server](https://github.com/kubewarden/policy-server)                 | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Webhook server that evaluates WebAssembly policies to validate Kubernetes requests                         |
| [kubewarden/audit-scanner](https://github.com/kubewarden/audit-scanner)                 | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Reports evaluation of existing Kubernetes resources with your already deployed Kubewarden policies         |
| [kubewarden/kwctl](https://github.com/kubewarden/kwctl/)                                | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Go-to CLI tool for Kubewarden users                                                                        |
| [kubewarden/helm-charts](https://github.com/kubewarden/helm-charts)                     | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Helm charts for the Kubewarden project                                                                     |
| [kubewarden/policy-evaluator](https://github.com/kubewarden/policy-evaluator)           | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Rust library used by Kubewarden to evaluate policies with a given input, request to evaluate and settings. |
| [kubewarden/policy-fetcher](https://github.com/kubewarden/policy-fetcher/)              | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Rust library used by Kubewarden to pull policies from OCI registries and HTTP servers.                     |

### Infra

[![Kubewarden Infra Repository](./badges/kubewarden-infra.svg)](./REPOSITORIES.md#infra-scope)

| NAME                                                                                                | STATUS                                                                                                                                                            | DESCRIPTION                                                                    |
| --------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| [kubewarden/automation](https://github.com/kubewarden/automation)                                   | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Automation scripts for the management of the Kubewarden organization on GitHub |
| [kubewarden/load-testing](https://github.com/kubewarden/load-testing)                               | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | HTTP load to stress policy-server                                              |
| [kubewarden/rancher-kubectl-builder](https://github.com/kubewarden/rancher-kubectl-builder)         | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Workflow to rebuild and sign rancher/kubectl image                             |
| [kubewarden/github-actions](https://github.com/kubewarden/github-actions)                           | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | GitHub actions used by the Kubewarden project                                  |
| [kubewarden/kubewarden-end-to-end-tests](https://github.com/kubewarden/kubewarden-end-to-end-tests) | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable) | Files used to run Kubewarden end-to-end tests                                  |

### Policies

[![Kubewarden Policy Repository](./badges/kubewarden-policies.svg)](./REPOSITORIES.md#policy-scope)

All the policies maintained by the Kubewarden team are stored in the
[policies](https://github.com/kubewarden/policies) repository.

For policies across **all** of GitHub, see the
[`kubewarden-policy`](https://github.com/topics/kubewarden-policy) topic tag.

#### Policies templates

The following repositories are the template the policy authors can use to write
their own policies. Checkout the Kubewarden [documentation](https://docs.kubewarden.io/)
for more information about how to write policies.

| NAME                                                                                              | STATUS                                                                                                                                                                   | DESCRIPTION                                                                                                                        |
| ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------- |
| [kubewarden/dotnet-policy-template](https://github.com/kubewarden/dotnet-policy-template)         | [![Incubating](https://img.shields.io/badge/status-incubating-orange?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#incubating) | A template repository to quickly scaffold a Kubewarden policy written with C#                                                      |
| [kubewarden/gatekeeper-policy-template](https://github.com/kubewarden/gatekeeper-policy-template) | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | A template repository to quickly port a [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/) policy to Kubewarden |
| [kubewarden/go-policy-template](https://github.com/kubewarden/go-policy-template)                 | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | A template repository to quickly scaffold a Kubewarden policy written with Go language                                             |
| [kubewarden/go-wasi-policy-template](https://github.com/kubewarden/go-wasi-policy-template)       | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Template of a plain WASI policy written using Go                                                                                   |
| [kubewarden/opa-policy-template](https://github.com/kubewarden/opa-policy-template)               | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | A template repository to quickly port a Open Policy Agent policy to Kubewarden                                                     |
| [kubewarden/rust-policy-template](https://github.com/kubewarden/rust-policy-template)             | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | A Kubewarden Rust policy template to be used with cargo-generate                                                                   |
| [kubewarden/swift-policy-template](https://github.com/kubewarden/swift-policy-template)           | [![Sandbox](https://img.shields.io/badge/status-sandbox-red?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#sandbox)             | A template repository to quickly scaffold a Kubewarden policy written with Swift language                                          |
| [kubewarden/js-policy-template](https://github.com/kubewarden/js-policy-template)                 | [![Sandbox](https://img.shields.io/badge/status-sandbox-red?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#sandbox)             | A template repository to quickly scaffold a Kubewarden policy written with TypeScript/JavaScript                                   |

For policy templates across **all** of GitHub, see the [`kubewarden-policy-template`](https://github.com/topics/kubewarden-policy-template) topic tag.

#### Policies SDKs

The following repositories are the SDKs the policy authors can use to write
their own policies. Checkout the Kubewarden [documentation](https://docs.kubewarden.io/)

| NAME                                                                            | STATUS                                                                                                                                                                   | DESCRIPTION                                                              |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------ |
| [kubewarden/policy-sdk-dotnet](https://github.com/kubewarden/policy-sdk-dotnet) | [![Incubating](https://img.shields.io/badge/status-incubating-orange?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#incubating) | Kubewarden Policy SDK for the .NET platform                              |
| [kubewarden/policy-sdk-go](https://github.com/kubewarden/policy-sdk-go)         | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Kubewarden Policy SDK for the Go programming language                    |
| [kubewarden/policy-sdk-rust](https://github.com/kubewarden/policy-sdk-rust)     | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Kubewarden Policy SDK for the Rust programming language                  |
| [kubewarden/policy-sdk-swift](https://github.com/kubewarden/policy-sdk-swift)   | [![Sandbox](https://img.shields.io/badge/status-sandbox-red?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#sandbox)             | Kubewarden Policy SDK for the Swift programming language                 |
| [kubewarden/policy-sdk-js](https://github.com/kubewarden/policy-sdk-js)         | [![Sandbox](https://img.shields.io/badge/status-sandbox-red?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#sandbox)             | Kubewarden Policy SDK for the JavaScript/TypeScript programming language |

For policy SDKs across **all** of GitHub, see the [`kubewarden-policy-sdk`](https://github.com/topics/kubewarden-policy-sdk) topic tag.

### Special

Finally, some repositories have a special meaning and do not fit the above
scopes. They serve a particular purpose or function in the
[Kubewarden](https://github.com/kubewarden) organization and are curated
by [maintainers](./GOVERNANCE.md#maintainers).

See [REPOSITORIES.md](./REPOSITORIES.md#special-scope) for more information.

| NAME                                                                                    | STATUS                                                                                                                                                                   | DESCRIPTION                                                                                                      |
| --------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| [kubewarden/fleet-example](https://github.com/kubewarden/fleet-example)                 | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Example of Rancher Fleet bundle for Kubewarden                                                                   |
| [kubewarden/docs](https://github.com/kubewarden/docs)                                   | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Kubewarden's documentation                                                                                       |
| [kubewarden/rfc](https://github.com/kubewarden/rfc)                                     | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Kubewarden's RFCs                                                                                                |
| [kubewarden/.github](https://github.com/kubewarden/.github)                             | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Special GitHub repository                                                                                        |
| [kubewarden/kubewarden.io](https://github.com/kubewarden/kubewarden.io)                 | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Kubewarden website                                                                                               |
| [kubewarden/gostubpkg](https://github.com/kubewarden/gostubpkg)                         | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | gostubpkg is a tool for generating stubs of Go packages                                                          |
| [kubewarden/k8s-objects-generator](https://github.com/kubewarden/k8s-objects-generator) | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | CLI tool that generates Kubernetes Go types that can be used with TinyGo starting from the official OpenAPI spec |
| [kubewarden/strfmt](https://github.com/kubewarden/strfmt)                               | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | A stripped down version of go-openapi/strfrm that works with TinyGo                                              |
| [kubewarden/k8s-objects](https://github.com/kubewarden/k8s-objects)                     | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Kubernetes Go types that can be used with TinyGo                                                                 |
| [kubewarden/utils](https://github.com/kubewarden/utils)                                 | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | Utils scripts used by the Kubewarden team and users.                                                             |
| [kubewarden/gtmpl-rust](https://github.com/kubewarden/gtmpl-rust)                       | [![Stable](https://img.shields.io/badge/status-stable-brightgreen?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#stable)        | golang text/template for rust                                                                                    |
| [kubewarden/policy-charts](https://github.com/kubewarden/policy-charts)                 | [![Incubating](https://img.shields.io/badge/status-incubating-orange?style=for-the-badge)](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#incubating) | Poliy Helm charts for Rancher UI                                                                                 |

### Archived

In general, a repository can be archived at the discretion of Kubewarden
community. Usually, maintainers can decide to archive a project that has not
been maintained for a long time or does not fit the guidelines for the projects
under the [Kubewarden](https://github.com/kubewarden) GitHub's
organization anymore. In other cases, a repository is archived to reserve its
name for future use.

The list of archived repositories can be found
[here](https://github.com/kubewarden?q=&type=archived&language=&sort=name).

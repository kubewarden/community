# Security self-assessment

## Self-assessment outline

### Table of contents

- [Metadata](#metadata)
  - [Security links](#security-links)
- [Overview](#overview)
  - [Actors](#actors)
  - [Actions](#actions)
  - [Background](#background)
  - [Goals](#goals)
  - [Non-goals](#non-goals)
- [Self-assessment use](#self-assessment-use)
- [Security functions and features](#security-functions-and-features)
- [Project compliance](#project-compliance)
- [Secure development practices](#secure-development-practices)
- [Security issue resolution](#security-issue-resolution)
- [Appendix](#appendix)

### Metadata

|                   |                                                                                                                                                                                                                   |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Assessment Stage  | Complete                                                                                                                                                                                                          |
| Software          | Many repositories under https://github.com/kubewarden. See breakdown [here](https://github.com/kubewarden/community?tab=readme-ov-file#repositories).                                                             |
| Security Provider | Yes                                                                                                                                                                                                               |
| Languages         | Rust, Go for main actors. Rust, Go, Rego, CEL, any language that compiles to Wasm for policies.                                                                                                                   |
| SBOM              | All Kubewarden [deliverables](https://docs.kubewarden.io/reference/artifacts) are accompanied with SBOM artifacts, shipped in their GitHub release and included in their OCI artifacts as layers when applicable. |

#### Security links

| Doc                          | URL                                                                                                                                           |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| Security overview            | [SECURITY.md](./SECURITY.md)                                                                                                                  |
| Security disclosure          | [SECURITY.md](https://github.com/kubewarden/community/blob/main/SECURITY.md#reporting-a-vulnerability), https://docs.kubewarden.io/disclosure |
| Threat model                 | https://docs.kubewarden.io/reference/threat-model                                                                                             |
| Security file                | [SECURITY.md](./SECURITY.md)                                                                                                                  |
| Default and optional configs | https://docs.kubewarden.io/howtos/security-hardening                                                                                          |

### Overview

Kubewarden is a Kubernetes Policy Engine. It aims to be the Universal Policy
Engine for Kubernetes, by allowing to write its policies in languages that can
be compiled to WebAssembly, and being modular. Kubewarden offers flexibility
for policy admission and enforcement in a Kubernetes environment.

#### Background

Kubewarden is a universal policy engine for Kubernetes, designed to simplify
the adoption of policy-as-code in cloud-native environments. It allows users
to write and enforce policies that govern the behavior and security of
Kubernetes clusters. Kubewarden's diferentiator is the use of WebAssembly
(Wasm) as the language of choice for the policies.

Using WebAssembly allows policy authors to write policies in their preferred
programming language (as long as it compiled into Wasm), keeping their
tools and workflows. Kubewarden Policies are shipped in OCI repositories, since
WebAssembly modules have first-class support as OCI artifacts. In addition,
policies enjoy the sandboxing features of WebAssembly, providing an additional
layer of security.

This means that policy users don't need to learn a new domain-specific
language; they are free to reuse existing ones such as Rego, or use policies
written in general-purpose languages.

The project aims to cater to various personas involved in Kubernetes
management, from policy authors and cluster operators to integrators, providing
a comprehensive solution for policy enforcement, security hardening, compliance
auditing, and resource optimization in Kubernetes environments. Thanks to that,
Kubewarden strives to be the universal policy engine of Kubernetes.

#### Actors

From a security perspective, the key technical actors are:

1. **Kubewarden Controller**: manages Kubewarden Custom Resources, sets up secure
   communication via TLS between components, and translates Kubewarden's
   configuration into Kubernetes resources.

2. **PolicyServer** (several): receives and validates Kubernetes admission
   requests by executing Kubewarden policies. It runs as a separate Deployment
   and communicates with the Kubernetes API server via webhooks.

3. **Policies** in WebAssembly: isolated Wasm modules containing validation or
   mutation logic, performing context-aware calls of the cluster, executed in a
   sandboxed environment within the PolicyServer.

4. **Audit Scanner**: cronjob that independently inspects cluster resources to
   identify policy violations, operating separately from the admission control
   flow. It achieves this by creating synthetic requests that are evaluated by
   the PolicyServers. The results get saved into PolicyReports CRs.

5. **Kubernetes API Server**: interacts with the PolicyServer through
   ValidatingWebhookConfiguration and MutatingWebhookConfiguration
   objects.

6. **OCI Registry**: stores and distributes Kubewarden policies as OCI artifacts,
   separate from the cluster environment.
7. **kwctl** CLI utility: command-line utility to interact with policies
   outside of the cluster. It uses the same libraries as the policy-server
   binary. It:

   - Pulls, pushes policies from and to OCI registries.
   - Verifies policy integrity and authenticity using Sigstore when downloading
     those policies.
   - Inspects the policy metadata (policies binaries are annotated with
     metadata). Annotates policy binaries with metadata. Metadata includes the
     types of the Kubernetes resources the policy targets, and the policy
     capabilities (mutating, context-aware, etc).
   - Runs policies outside of the cluster. Useful for developing, benchmarking
     and testing policies in CI for example.
   - Generates YAML manifests for the policy CRs of Kubewarden from the policy
     metadata. This simplifies policy deployment.

8. **Certificate Authority and TLS Certificates**: generated and managed by the
   Kubewarden Controller to secure communication between components.

9. **Policy Reporter & its UI**: provides a separate interface for
   visualizing the PolicyReports, which provides insight on compliance status
   and policy violations.

10. **OpenTelemetry stack** (optional): Kubewarden exposes metrics and tracing
    from the controller and its policy-servers into OpenTelemetry.

Each of the in-cluster actors run in their own Deployments with a degree of
isolation with compartmentalized functions, contributing to the security
posture.

#### Actions

Here are the key actions and interactions between Kubewarden actors, focusing
on security checks and sensitive data handling:

1. Deploying the Kubewarden stack:
   Installing its Helm charts, `kubewarden-crds`, `kubewarden-controller`. The
   `kubewarden-defaults` chart is optional and provides a default PolicyServer and
   recommended policies. Configuration can be used for production deployments (the
   controller can create PodDisruptionBudgets, affinity, limits, set the
   recommended policies in enforce mode, mutual TLS with the API server and within
   components, etc).
2. Access Control:
   Kubewarden controller and PolicyServers come by default with sane RBAC.
   PolicyServers by default have a ServiceAccount with readonly access for the
   context-aware feature. The Kubewarden operator controls what [a policy can
   access](https://deploy-preview-562--docs-kubewarden-io.netlify.app/next/explanations/context-aware-policies)
   via said ServiceAccount. The Audit Scanner feature can also be fine-tuned.

3. Handling of Certificate Authorities and certificates:
   - Upon first install `kubewarden-controller` Helm chart will create the
     Certificate Authority used by the controller to register the Webhooks against
     the API server for reconciling Kubewarden CRs.
   - The controller generates and manages the TLS certificates for secure
     communication between components. They have an expiry of 1 year, configurable.
   - Certificate Authority and certificates are renewed and propagated
     automatically by the controller.
   - The project supports custom CAs. PolicyServers can be configured via its
     spec, and the use of sources.yaml for `kwctl` and the PolicyServers.
4. The kubewarden-controller reconciles the desired PolicyServers.
   This entails:

   1. Instatiate a policy-server Deployment.
   2. Create/Update ConfigMap associated with the PolicyServer that contains a
      list of all policies currently bound to the PolicyServer.
   3. The policy-server binary downloads all policies from the OCI registry
      (optionally verifying its signatures).
   4. The policy-server binary validates each of the configured policy settings
      by invoking the `validate_setting` of each policy. This ensures the
      policy is working as intended.
   5. The policy-server binary spawns a pool of worker threads to evaluate
      requests for the policies.
   6. The policy-server binary starts an HTTPS server and reports it's ready
      via the readiness probe.
   7. Once the policy-server is ready, the controller changes the PolicyServer Status, and creates/updates
      ValidatingWebhookConfiguration and MutatingWebhookConfiguration against
      the Kubernetes API server that point to the Service that corresponds to the PolicyServer.

   Updates to the PolicyServer Deployments happen via a Rollout, where the
   Webhooks point to the old Deployment until the new Deployment is ready.

   While this has served well so far, we plan to revise the lifecycle of
   policies and policy servers to allow users to better monitor the status of
   policies, and perform rollbacks to previous policy versions. This is
   explained in
   [RFC-22](https://github.com/kubewarden/rfc/blob/main/rfc/0022-policy-lifecycle.md).

5. Generating a YAML manifest from a Wasm policy:
   Using `kwctl`, one pulls the Wasm module from the OCI registry. Then one
   verifies the policy Sigstore signature with `kwctl`, and uses `kwctl` to
   scaffold a YAML manifest from the desired policy. Then `kubectl apply`ies
   the YAML manifest.

6. The kubewarden-controller reconciles a Policy:
   The controller updates the ConfigMap associated to the PolicyServer where
   the policy is scheduled, and performs a Rollout of the Deployments associated
   with that PolicyServer.

7. Policy execution for usual Admission Control:

   1. Kubernetes API Server sends admission requests to the policy-server
      binary via webhooks.
   2. policy-server validates the request format and authenticity.
   3. policy-server executes relevant WebAssembly policies in a sandboxed
      environment. if the policy is a mutating one, the end result is a changed
      admission request.
   4. policy-server returns admission decision to the API Server, with the
      decision to accept or reject the request.

8. Policy execution for context-aware calls:

   It is the same process as a normal execution, with the difference that the
   policy-server performs queries to the API server to learn about the state of
   the cluster. This queries are done with a Kubernetes client, and via the
   ServiceAccount that the PolicyServer was configured with. By default,
   readonly access is provided.
   In addition, each policy has a `spec.contextAwareResources` field that lists
   which resources from the cluster the policy is allowed to query about. In
   case that a policy Wasm module tries to access resources that the Policy CR
   didn't declare in its `spec.contextAwareResources`, said query is blocked
   and reported to the administrators.

9. Audit Scanning:

   1. The Audit Scanner CronJob triggers, creating a Pod with the audit-scanner
      binary.
   2. The audit-scanner binary queries the cluster and creates tuples of
      resources and the policies that apply to those resources.
   3. It queries the cluster via its default ServiceAccount, which by
      default is bound to the ClusterRoles `view` (read-only of most objects
      besides Secres, Roles, or RoleBindings) and `audit-scanner-cluster-role`
      (read-write access to Kubewarden resources and PolicyReports). The SA is
      configurable.
   4. The audit-scanner binary creates [synthetic
      requests](https://docs.kubewarden.io/explanations/audit-scanner), and
      sends them to the policy servers.
      Some [limitations
      apply](https://docs.kubewarden.io/explanations/audit-scanner/limitations)
      (e.g: policies relaying on external data, or user and user group info).
   5. The audit-scanner collects all the results and saves them in
      PolicyReports from the openreports.io project, deleting old PolicyReports
      on each run first.
      This ensures that PolicyReports results are as up-to-date as possible.

10. Secure Communication:

    - Kubewarden Controller generates and manages TLS certificates.
    - Components use these certificates for encrypted communication.
    - If desired, one can enable mutual TLS or use NetworkPolicies and a CNI to
      ensure authentication and encrypted communication.

11. Monitoring and Reporting:

    - Policy Reporter UI collects data from PolicyReports.
    - UI presents compliance status and policy violations in a secure,
      read-only interface.

#### Goals

Kubewarden intends to:

- Be the Universal Policy Engine for Kubernetes by simplifying adoption of
  Policy As Code in cloud-native environments. Provide security hardening,
  continous compliance auditing, and resource optimization for Kubernetes
  clusters.
- Enable writing policies in any programming language that generates
  WebAssembly binaries.
  - Allow reuse of policies from other policy engines without rewriting them.
    For example reusing Rego policies from OPA & Gatekeeper, or using our
    experimental `kyverno-dsl-policy` policy.
  - Distribute policies using OCI compliant registries.
  - Provide a stable API for policy development, and SDKs for popular languages.
- Enhance security by verifying policies using SLSA, as well as Kubernetes
  resources.
- Cater to various personas in an organization, including Policy Users, Policy
  Developers, Policy Distributors, Cluster Operators, and Kubewarden Integrators.
- Foster transparency, collaboration, and improvement through CNCF membership
  and an open-source community.
- Maintain a corpus of useful policies, shipped via ArtifactHub.
- Be able to run policies and the policy-server binary outside of the cluster
  (see ["raw policies"](https://docs.kubewarden.io/howtos/raw-policies)).

#### Non-goals

Kubewarden doesn't intend to:

- Replace Kubernetes built-in security features, but complement them:
  - We provide migration from PSPs.
  - One can re-use ValidatingAdmissionPolicies and CEL policies with our
    `cel-policy`.
  - Kubewarden policies can be mutating, while Pod Security Admission cannot.
  - Kubewarden policies benefit from the Kubewarden stack features (audit
    scanner, telemetry, CRD management).
- Provide runtime security like intrusion detection or runtime container
  isolation.
- Provide host system protection of clusters.
- Provide infinite policy execution flexibility. To prevent DoS attacks,
  policies' processing times are limited.

### Self-assessment use

This self-assessment is created by the Kubewarden team to perform an internal
analysis of the project's security. It is not intended to provide a security
audit of Kubewarden, or function as an independent assessment or attestation of
Kubewarden's security health.

This document serves to provide Kubewarden users with an initial understanding
of Kubewarden's security, where to find existing security documentation,
Kubewarden plans for security, and general overview of Kubewarden security
practices, both for development of Kubewarden as well as security of
Kubewarden.

This document provides the CNCF TAG-Security with an initial understanding of
Kubewarden to assist in a joint-assessment, necessary for projects under
incubation. Taken together, this document and the joint-assessment serve as a
cornerstone for if and when Kubewarden seeks graduation and is preparing for a
security audit.

### Security functions and features

Depending on the role, we differentiate our components between "core" "infra",
"policies", "SDKs", etc. See the
[README.md](https://github.com/kubewarden/community/blob/main/README.md#repositories)
on this repository.

We also define different
[statuses](https://github.com/kubewarden/community/blob/main/REPOSITORIES.md#status)
to signify maturity for our components and repositories in the
[README.md](./README.md) of this repository.

Critical ["core"
components](https://github.com/kubewarden/community/blob/main/README.md#core)
comprise the Kubewarden stack. They have been used for threat modeling.

The rest are of components listed there are security relevant, for example
policies maintained by the Kubewarden team. They are part of the threat
modeling with lowered expectations (as they are sandboxed, for example all
policies given they are WebAssembly modules).

On "policies" components, one should make a special mention to those
implementing DSLs whose attack surface is greater. To date these are the
cel-policy and the kyverno-dsl-policy.

Other components such as "policies SDKs", "policy templates" and "special"
helpers are not consumed when deploying Kubewarden.

Nevertheless, all components ("core", "policies", "policies SDKs", "policy
templates", "special", and others) receive maintenance according to their status.

### Project compliance

To date, we haven't formally certified Kubewarden to meet any security
standards (such as PCI-DSS, COBIT, ISO, GDPR, etc.).

However, policies from our catalog can be used for providing certification of
other workloads in Kubernetes clusters. Some policies ship with metadata
annotations in the form of `io.kubewarden.policy.standards.*` (example,
[`io.kubewarden.policy.standards.soc2-type-i:
soc2-type-i.2.1.1`](https://github.com/kubewarden/rego-policies-library/blob/main/policies/ControllerAffinityNodeSelector/metadata.yml#L29)).
These annotations are used by `kwctl` when scaffolding the custom resource as
Kubernetes annotations.

### Secure development practices

#### Development Pipeline

For our "core" stable components, our "policy" stable components (see previous
"security functions and features" subsection), plus others (on a best-effort
basis), we ensure the following.

Our development pipeline is [SLSA v1.0 L3](https://slsa.dev/spec/v1.0/levels#build-l3) ready:

- Build platform and pipelines run on dedicated infrastructure, where the runs
  don't influence one another and are tamper-proof.
- We provide digitally signed build immutable artifacts and provenance.

In addition, we provide Software Bill of Materials for our deliverables.

Committers require cryptographically signed commits, and Developer Certificate
of Origin. We require Pull Requests to be reviewed and merged by at least 1
maintainer. We strive to have [~70% of code
test](https://app.codecov.io/github/kubewarden/) coverage for our main
repositories. We adhere by OpenSSF practices. We create ["tech-debt"
issues](https://github.com/orgs/kubewarden/projects/6/views/9) and work on at
least 1 of them per sprint. We have automated checks for vulnerabilities via
using Dependabot.

### Communication Channels.

Our channels are linked in docs.kubewarden.io, kubewarden.io, and in the
[./README.md] under this repository:

- Slack: [#kubewarden](https://kubernetes.slack.com/archives/kubewarden) and [#kubewarden-dev](https://kubernetes.slack.com/archives/kubewarden-dev).
- GitHub discussions in this repository.
- Maintainers mailing list: `cncf-kubewarden-maintainers`, followed by `@`, followed by `lists.cncf.io`

Communication:

- Internal. By default and when possible, team members strive to communicate
  in the open channels.
- Inbound. Users and prospective users get in contact with us via the slack
  channels and our monthly Kubewarden Office calls.
- Outbound. We post announcements on the `#kubewarden` Slack channel, and we have
  several blog posts per month under https://kubewarden.io/blog.

### Ecosystem

#### Kubernetes integration

Provided by Kubewarden's Helm charts, which install `kubewarden-controller` and CRD definitions.

#### OpenTelemetry integration

Kubewarden components expose metris and tracing via OpenTelemetry endpoints.

#### GitOps

Kubewarden documentation lists ArgoCD and Fleet how-tos.

### Security issue resolution

- Responsible Disclosures Process. This is specified both in the
  [SECURITY.md](./SECURITY.md) file in this repository and in
  https://docs.kubewarden.io/disclosure.

- Vulnerability Response Process. Specified in the
  [SECURITY.md](./SECURITY.md) file in this repository under "Reporting a vulnerability".

- Incident Response. Specified in the
  [SECURITY.md](./SECURITY.md) file in this repository under "Security Patch
  Policy, Dependency Policy".

### Appendix

#### Known Issues Over Time

We publish our security advisories via the "security advisory" feature of GitHub.
We also explain them in our release blog posts ([example](https://www.kubewarden.io/blog/2025/01/kubewarden-1-21-release/)).
List of issues to this date:

- [GHSA-5877-g4h3-mf3c](https://github.com/kubewarden/helm-charts/security/advisories/GHSA-5877-g4h3-mf3c)
- [CVE-2025-24376](https://github.com/kubewarden/kubewarden-controller/security/advisories/GHSA-fc89-jghx-8pvg)
- [CVE-2025-24784](https://github.com/kubewarden/kubewarden-controller/security/advisories/GHSA-756x-m4mj-q96c)

#### OpenSSF Best Practices

Kubewarden passes the [Open SSF Best Practices](https://www.bestpractices.dev/en):
https://www.bestpractices.dev/en/users/23101

Kubewarden is also in
[CLOMonitor](https://clomonitor.io/projects/cncf/kubewarden), and we strive to
have 100% coverage.

#### Adopters and Case Studies

We maintain a list of adopters in the [ADOPTERS.md](./ADOPTERS.md) file of this
repository.

Example case studies:

- Case A: as a Kubernetes operator, I want to ensure my cluster is safe and
  compliant.

  I deploy Kubewarden and its default configuration with its
  `kubewarden-defaults` Helm chart, in the `kubewarden` Namespace. This deploys a
  default PolicyServer and recommended ClusterAdmissionPolicies in the
  `kubewarden` namespace, solely under the control of the Kubernetes operator.

  As an operator, I can add more PolicyServers under a managed Namespace
  (such as `kubewarden`) to distribute load and fault tolerance.

  The operator can deploy more ClusterAdmissionPolicies and ClusterAdmissionPolicyGroups
  that check the totality of the Kubernetes resources, for any type of
  operation (CREATE, UPDATE, DELETE, etc). This ensures operations into the
  cluster are safe and compliant. This includes security, compliance (to
  industry standards or company regulations), resource optimization (via
  mutating policies), governance of Kubernetes environments (via labels and
  naming conventions), best practices, image verification, etc.

  The security expectations change in the future, and that was ok to have
  deployed in the cluster isn't anymore. Yet Kubewarden already accepted those
  operations in the cluster. What the operator can do is to deploy the Audit
  Scanner feature, a CronJob that runs periodically and evaluates the existing
  resources in the cluster. This ensures the cluster is safe and compliant even
  with the pass of time.

  The operator can configure some or all the policies in `monitor` mode instead
  of `protect` mode, to learn from the state of the cluster without blocking operations.

  As usual, the operator can receive information from policies and the Kubewarden stack
  by consuming logs and OpenTelemetry information for metrics and tracing.

- Case B: As a Kubernetes operator, I want to provide a framework to my
  Kubernetes users so they can self-service in their Namespaces.

  As an operator, I deploy Kubewarden as in Case A for a set of policies of my choosing.
  This provides me with safe baseline in the cluster, that other users cannot evade.

  In addition to Case A, I have different personas per Namespaces: perhaps
  teams, team administrators, test deployments, etc.
  I allow each Namespace administrator to self-service by letting them deploy
  PolicyServers in their Namespace, along with namespaced AdmissionPolicies and
  AdmissionPolicyGroups. These arquitecture means that they are in control of
  their PolicyServer and policies, the policies only apply to their Namespace,
  and the resource usage is contained also to their Namespace.

  This also allows the operator to segregate noisy tenants, reserving
  performant PolicyServers for those tenants and tasks that need high
  throughput and low latency for example.

- Case C: As a policy author, I want to use the tools and languages that I know
  to write new policies.

  Kubewarden achieves this by supporting any language that compiles to
  WebAssembly as possible target languages for policies. This means that policy authors
  can reuse their workflows (`git`, CI, editors, peer reviews, etc), and tools:
  languages, language libraries, testing harnesses and frameworks, etc.

  This allows re-using Domain Specific Languages (like Rego, CEL, Kyverno's
  YAML+macros) or general-purpose languages (like Go, Rust, C#, Javascript, any
  that compiles to Wasm). Kubewarden provides [SDKs](https://docs.kubewarden.io/tutorials/writing-policies) for some languages as
  first-class support.

  Kubewarden policies can be as simple as desired, or complex
  [context-aware](https://docs.kubewarden.io/explanations/context-aware-policies)
  policies. Context-aware policies can also be used to interface with separate
  workloads (for example, to obtain information from an image scanner
  long-running service).

- Case D: As a system integrator, I want to re-use Kubewarden as part of my
  security and compliante solution, and re-use other solutions by including
  them in Kubewarden.

  As a system integrator, I can reuse parts of Kubewarden, such as the
  `policy-server`, to police resources inside of the Kubernetes cluster, or
  outside of the cluster via the ["raw
  policies"](https://docs.kubewarden.io/howtos/raw-policies) feature.

  The system integrator can chose to deploy the `kubewarden-controller` or
  manage the CRDs on their own, and can chose to deploy or scale the Audit
  Scanner as needed.

  I can create new components, for example an image scanner, and interface with
  it via a context-aware policy, without having a monolithic implementation in
  a Kubernetes controller.

#### Related Projects / Vendors

We maintain a comparison documentation page with comparisons. Currently,
it contains a [comparison with OPA Gatekeeper](https://docs.kubewarden.io/explanations/comparisons/opa-comparison).

For Vendors, See the [enterprise](https://docs.kubewarden.io/enterprise) page.

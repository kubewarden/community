# General Technical Review questions

v1.0

## Introduction

The General Technical Review questions can be completed by a project in lieu of a presentation to a Technical Advisory Group (TAG) as well as to satisfy the Engineering Principle requirements of a Sandbox application or Due Diligence for moving levels.

The questions are designed to prompt **_design thinking_** for projects that would like to one day be a graduated project.

The intent is to understand how the project has adopted and aligned with the CNCF maturation levels as well as encourage good design & security best practices.

<!--
The General Technical Review questions can be completed by a project team in lieu of a presentation to a Technical Advisory Group (TAG) as well as to satisfy several of the Engineering Principle requirements for applying to CNCF Sandbox as well as applying to move to Incubation and Graduation.

For the purposes of the general technical review and further domain reviews, the questions are designed to prompt design thinking for ready-for-production projects and architecture. The intent is to understand and validate the cloud native software lifecycle of the project and whether it is in line with the CNCF Maturation process and levels.

Project maintainers are expected to have designed the project for cloud native use cases and workloads, as well as taking a ‘secure by design and secure by default’ approach that enables adopters and consumers of the project the ability to ‘loosen’ the defaults in a manner that suits their environment, requirements and risk tolerance.

These questions are to gather knowledge about the project. Project maintainers are expected to answer to the best of their ability. **_Not every question will be addressable by every project._**

**Suggestion:** A recorded demo or diagram(s) may be easier to convey some of the concepts in the questions below. The project maintainers may provide a link to a recorded demo or add architectural diagrams along with your GTR questionnaire.

-->

### General Technical Review questions

The questions follow the cloud native software lifecycle day schemas:

**Day 0 - Planning Phase. (Sandbox)** - This phase covers design and architecture of the cloud native project.

**Day 1 - Installation and Deployment Phase (Incubation)** - This phase covers initial installation and deployment of the design developed during Day 0 - Planning Phase.

**Day 2 - Day-to-Day Operations Phase (Graduated)** - This phase covers post-deployment operations in production-ready environments to include monitoring, maintenance, auditing and troubleshooting.

### How to use this template

Make a copy of the template below and answer questions related to your project level to the best of your ability.
_**Not every question will be addressable or relevant to every project.**_
If this is the case for your project, please mark it as not-applicable (N/A) and provide a brief explanation.

**NOTE:** The questions are cumulative e.g. if you are applying for incubation or graduation, you should answer both day 0 and day 1 questions etc.

#### Tips

- Treat the GTR questionnaire as a living document and keep a copy of it in your project's own repo. The GTR questions are helpful to both contributors and users and will make updating it in the future less work when you want to apply to move levels.
- Answer more questions than the requirement for your level if it _makes sense for your project_. e.g. if you have documentation covering the different forms of observability in the Day-2 requirements.
- You **CAN** link out to your own project's documentation, but be sure to link to it in a _versioned_ form. e.g. link to it at a specific commit instead of the `main` branch, or versioned website.
- A recorded demo or diagram(s) may be easier to convey some of the concepts in the questions below. You may provide a link to a recorded demo or add architectural diagrams along with your GTR questionnaire.
- If you are unsure or have a question about any section below, **please ask**. Chances are you're not the only one with a question and the template should be updated with additional guidance.

---

# General Technical Review - Kubewarden / Sandbox

- **Project:** Kubewarden
- **Project Version:** mixed (see below)
- **Website:** https://kubewarden.io
- **Date Updated:** 2026-10-13
- **Template Version:** v1.0
- **Description:**
  Kubewarden is a Kubernetes security platform. It contains four components.
  Each component addresses one need.

  - Admission Controller: the first component of the project. It is a
    Kubernetes Admission Controller. Its policies are written using
    any language that can compile to WebAssembly. The goal of Kubewarden
    Admission Controller is to be the universal policy engine
    for Kubernetes.
    - Simplifies the adoption of policy as code.
    - Uses WebAssembly so policies run on any CPU architecture and can
      be written in any language that compiles to WebAssembly.
    - Distributes policies as OCI artifacts.
    - Reuses policies from other policy engines (Gatekeeper, Kubernetes VAP, Kyverno) without
      a rewrite.
    - Verifies policies with Sigstore signatures.
    - Provides one approach to admission policy management.
  - Network Enforcer: discovers network activity inside of a Kubernetes
    cluster and creates network policies that protect workloads.
    - Works in three phases:
      - Learn: discovers network traffic patterns.
      - Monitor: does not block traffic that violates the network policy.
        It notifies the administrator about the violations.
      - Protect: blocks traffic that violates the network policy and
        notifies the administrator.
    - Runs on top of Cilium, Calico or Istio ambient mode.
    - Integrates with OpenTelemetry for logs, metrics and violations.
  - Runtime Enforcer: prevents unwanted processes from running inside of
    containers.
    - Uses eBPF.
    - Works in three phases:
      - Learn: discovers the binaries that start inside of a Pod, at the
        container level.
      - Monitor: lets any process start inside of a container. It reports
        violations to the administrator.
      - Protect: blocks binaries that are not in the allow list. It reports
        violations to the administrator.
    - Integrates with OpenTelemetry for logs, metrics and violations.
  - SBOM Scanner: a vulnerability scanner for Kubernetes clusters, based on
    Software Bills of Materials (SBOMs).
    - Scans container images in registries, running workloads and cluster
      nodes.
    - Generates an SBOM for each image and node. Then it scans the SBOM for
      operating-system and application-library vulnerabilities.
    - Uses the SBOM as the source of truth. When the vulnerability database
      changes, it scans the stored SBOM again without pulling the image again.
    - Supports VEX (Vulnerability Exploitability eXchange), KEV and EPSS to
      reduce false positives and help with vulnerability prioritization.
    - Stores reports as Kubernetes resources through an extension API server to
      prevent clogging Kubernetes' etcd.
    - Integrates with OpenTelemetry to export traces and metrics.

## Day 0 - Planning Phase

### Scope

- Describe the roadmap process, how scope is determined for mid to long term features, as well as how the roadmap maps back to current contributions and maintainer ladder?

  Information about Kubewarden's roadmap process is available in the [ROADMAP.md](https://github.com/kubewarden/community/blob/main/ROADMAP.md) document in the community repository.

  The maintainer ladder is at [MAINTAINERS.md](https://github.com/kubewarden/community/blob/main/MAINTAINERS.md).

- Describe the target persona or user(s) for the project?

  Each component documents its target personas:

  - [Admission Controller personas](https://docs.kubewarden.io/admission-controller/latest/en/personas.html)
  - [Network Enforcer personas](https://docs.kubewarden.io/network-enforcer/latest/en/personas.html)
  - [Runtime Enforcer personas](https://docs.kubewarden.io/runtime-enforcer/latest/en/personas.html)
  - [SBOM Scanner personas](https://docs.kubewarden.io/sbom-scanner/latest/en/personas.html)

- Explain the primary use case for the project. What additional use cases are supported by the project?

  Each component documents its use cases:

  - [Admission Controller use cases](https://docs.kubewarden.io/admission-controller/latest/en/use-cases.html)
  - [Network Enforcer use cases](https://docs.kubewarden.io/network-enforcer/latest/en/use-cases.html)
  - [Runtime Enforcer use cases](https://docs.kubewarden.io/runtime-enforcer/latest/en/use-cases.html)
  - [SBOM Scanner use cases](https://docs.kubewarden.io/sbom-scanner/latest/en/use-cases.html)

- Explain which use cases have been identified as unsupported by the project.

  Each use cases page ends with a Non-goals section:

  - [Admission Controller non-goals](https://docs.kubewarden.io/admission-controller/latest/en/use-cases.html#_non_goals)
  - [Network Enforcer non-goals](https://docs.kubewarden.io/network-enforcer/latest/en/use-cases.html#_non_goals)
  - [Runtime Enforcer non-goals](https://docs.kubewarden.io/runtime-enforcer/latest/en/use-cases.html#_non_goals)
  - [SBOM Scanner non-goals](https://docs.kubewarden.io/sbom-scanner/latest/en/use-cases.html#_non_goals)

- Describe the intended types of organizations who would benefit from adopting this project. (i.e. financial services, any software manufacturer, organizations providing platform engineering services)?

  Enterprise organizations, startups, SaaS providers, regulated industries, financial services and any organization running Kubernetes at scale.

- Please describe any completed end user research and link to any reports.

  We are working on a report to be published in the future.

### Usability

- How should the target personas interact with your project?

  - CLI:
    - Admission controller: [kwctl](https://docs.kubewarden.io/admission-controller/latest/en/reference/kwctl-cli.html) helps with publishing, managing and testing policies.
    - Runtime enforcer: [kubectl plugin](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/kubectl_plugin.html):
      helps manage the life-cycle of a policy.
    - Runtime enforcer: [wpgen](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/wpgen/index.html):
      drafts a `WorkloadPolicy` from container images, before the workload runs.
  - Helm: [Charts](https://github.com/kubewarden/helm-charts) are available for installing Kubewarden in Kubernetes clusters. Charts are also discoverable over ArtifactHUB.
  - Kubernetes CRDs:
    - [Admission Controller CRDs reference](https://docs.kubewarden.io/admission-controller/latest/en/reference/CRDs.html)
    - [Network Enforcer CRDs reference](https://docs.kubewarden.io/network-enforcer/latest/en/reference/crd.html)
    - [Runtime Enforcer CRDs reference](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/crd.html)
    - [SBOM Scanner CRDs reference](https://docs.kubewarden.io/sbom-scanner/latest/en/reference/crd-reference.html)

- Describe the user experience (UX) and user interface (UI) of the project.

  Kubewarden components' user experience centers around a collection of Kubernetes CRDs.
  The project has no web UI. You can integrate external tools that offer
  graphical interfaces for policy management, reporting and observability.
  See the following question for more details.

  Some components also offer a CLI (dedicated ones or `kubectl` plugins) to simplify
  certain operations.

- Describe how this project integrates with other projects in a production environment.

  Kubewarden integrates with the following projects in the Cloud Native ecosystem:

  #### Integrations

  | Project                                                       | Purpose                                                         | Documentation                                                                                                                  |
  | ------------------------------------------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
  | [OpenTelemetry](https://github.com/open-telemetry)            | Provide unified observability.                                  | https://docs.kubewarden.io/admission-controller/latest/en/howtos/telemetry/10-opentelemetry-qs.html                            |
  | [Prometheus](https://github.com/prometheus/prometheus)        | Collect and stores time-series metrics from all the components. | https://docs.kubewarden.io/admission-controller/latest/en/howtos/telemetry/30-metrics-qs.html                                  |
  | [Grafana](https://github.com/grafana/grafana)                 | Visualize metrics through customizable dashboards.              | https://docs.kubewarden.io/admission-controller/latest/en/howtos/telemetry/30-metrics-qs.html                                  |
  | [Jaeger](https://github.com/jaegertracing/jaeger)             | Visualize fine-grained traces about security events.            | https://docs.kubewarden.io/admission-controller/latest/en/howtos/telemetry/20-tracing-qs.html                                  |
  | [Policy Reporter](https://github.com/kyverno/policy-reporter) | Visualize policy violations for auditing purposes.              | https://docs.kubewarden.io/admission-controller/latest/en/explanations/audit-scanner/policy-reports.html#_policy_reporter_ui   |
  | [Sigstore](https://github.com/sigstore/sigstore)              | Signing of policies.                                            | https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/secure-supply-chain.html#_signing_policies |
  |                                                               | Verification of OCI artifacts within policy logic.              | https://docs.kubewarden.io/admission-controller/latest/en/reference/spec/host-capabilities/02-signature-verifier-policies.html |
  | [ArgoCD](https://github.com/argoproj/argo-cd)                 | GitOps.                                                         | https://docs.kubewarden.io/admission-controller/latest/en/howtos/argocd-installation.html                                      |
  | [Flux](https://github.com/fluxcd/flux2)                       | GitOps integration.                                             |                                                                                                                                |
  | [Cilium](https://github.com/cilium/cilium)                    | Network enforcement                                             | https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html                                           |
  | [Istio](https://github.com/istio/istio)                       | Network enforcement                                             | https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html                                           |

### Design

- Explain the design principles and best practices the project is following.

  #### Design principles
  - [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/explanations/architecture.html#_design_principles)
  - [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html#_design_principles)
  - [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/explanations/architecture.html#_design_principles)
  - [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/explanations/architecture.html#_design_principles)

  #### Best practices
  1. **Stay Aligned with Upstream Kubernetes**

  Kubewarden’s CRDs live under `<component>.kubewarden.io/v1` and adhere to the Kubernetes API conventions.
  Policy semantics mirror official Kubernetes policies to avoid surprises when
  upgrading or integrating with native tooling.

  2. **Automate CI/CD Pipelines**

  All components use GitHub Actions to:
  - Test code changes: unit, integration and end-to-end tests
  - Produce SBOMs
  - Build and sign artifacts (latest, release candidates, GA releases)

  GitHub Actions are reused whenever possible between the different components.

  3. **Test for Real-World Scenarios**

  Each component repository contains an end-to-end test suite.
  The suite installs the component in a Kubernetes cluster and exercises it under realistic conditions.
  The tests run in CI before every release.

  4. **Community-Driven Roadmap & Governance**

  Track features, issues, and milestones openly in the [Kubewarden GitHub projects](https://github.com/orgs/kubewarden/projects).
  Each project has its own dedicated board.
  Information about Kubewarden's roadmap process is available in the [ROADMAP.md](https://github.com/kubewarden/community/blob/main/ROADMAP.md) document in the community repository.

  Propose and review RFCs. Each component has its own `docs/rfcs` directory.
  RFCs impacting multiple components are defined inside of [kubewarden/rfc](https://github.com/kubewarden/rfc).

  The project hosts a [monthly community meetings](https://zoom-lfx.platform.linuxfoundation.org/meetings/kubewarden?view=week).

  5. **Versioned Documentation**

  Provide quick starts, tutorials, how-tos, API references and upgrade guides pinned to specific releases
  so users can always view documentation matching their software version in [docs.kubewarden.io](https://docs.kubewarden.io).

  6. **Secure Software Supply Chain (SLSA Compliance)**

  Build pipelines generate [SPDX SBOMs](https://spdx.dev) and [SLSA](https://slsa.dev) Build Level 3 provenance for every container image, Helm chart and binary.
  Sigstore cosign signs every artifact, including the WebAssembly policies.
  The "secure software supply chain best practices" answer in the Security section lists the level of each artifact and the verification commands.

- Outline or link to the project’s architecture requirements? Describe how they differ for Proof of Concept, Development, Test and Production environments, as applicable.

  The architecture documentation of each component is available at:

  - [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/explanations/architecture.html)
  - [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html)
  - [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/explanations/architecture.html)
  - [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/explanations/architecture.html)

  See also the [actors](https://github.com/kubewarden/community/blob/main/security-self-assesment.md#actors) and
  [actions](https://github.com/kubewarden/community/blob/main/security-self-assesment.md#actions)
  sections of the [Security Self-Assessment](https://github.com/kubewarden/community/blob/main/security-self-assesment.md) document.

- Define any specific service dependencies the project relies on in the cluster.

  The Admission Controller has no required service dependencies in the cluster. It manages its own TLS certificates.
  The optional integrations and their tested version ranges are in the [Dependency matrix](https://docs.kubewarden.io/admission-controller/latest/en/reference/dependency-matrix.html).
  The three newer components depend on other services in the cluster.

  **Network Enforcer**

  - cert-manager and cert-manager-csi-driver: required for the default chart install.
  - One network provider: Istio ambient mode (1.30.3 or later), Calico (v3.32.1 or later) or Cilium (1.20.0 or later).
    The provider enforces the generated policies and reports the network flows.
    A [flow](https://docs.kubewarden.io/network-enforcer/latest/en/glossary.html#_flow) is one observed connection between two workloads: source, destination, protocol and port.
  - The service of the provider that reports the flows: ztunnel access logs (Istio), Goldmane (Calico) or Hubble Relay (Cilium).

  See [Compatibility](https://docs.kubewarden.io/network-enforcer/latest/en/reference/compatibility.html).

  **Runtime Enforcer**

  - cert-manager and cert-manager-csi-driver.
  - A container runtime with NRI (Node Resource Interface) enabled: containerd or CRI-O.

  See [Compatibility](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/compatibility.html) and
  [Quick Start](https://docs.kubewarden.io/runtime-enforcer/latest/en/quickstart.html).

  **SBOM Scanner**

  - cert-manager.
  - A PostgreSQL database. By default, the chart creates it with the CloudNativePG operator, which you must install first.
    Alternatively, you can use an external PostgreSQL database instead.
  - A default StorageClass.

  The chart deploys NATS as a subchart, so NATS is not an external dependency.

  See [Quickstart](https://docs.kubewarden.io/sbom-scanner/latest/en/quickstart.html) and
  [Helm values](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/helm-values.html).

  **Optional integrations**

  All components can integrate with external services for observability, audit visualization and policy management.
  See [Integrations](#integrations) for the full list.

- Describe how the project implements Identity and Access Management.

  Kubewarden does not implement its own identity system.
  Users and automation interact with each component through Kubernetes custom resources.
  As a result, Kubernetes RBAC controls who can read and change these resources.

  Each workload runs under its own Service Account. The RBAC rules of each Service Account grant only the permissions that the workload needs.
  Components do not share credentials.

  **Admission Controller**

- Management of namespaced `AdmissionPolicy` and `AdmissionPolicyGroup` resources can be delegated to
  namespace owners. Cluster administrators manage the cluster-wide `ClusterAdmissionPolicy` and
  `ClusterAdmissionPolicyGroup` resources.
- Each Policy Server uses its own `ServiceAccount`.
  [Context-aware policies](https://docs.kubewarden.io/admission-controller/latest/en/explanations/context-aware-policies.html)
  must declare which resources they read. Access to undeclared resources is blocked.
- Each Policy Server can define which host capabilities are available to namespaced policies. See
  [Namespaced policy host capabilities](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html#_namespaced_policy_host_capabilities)
  in the hardening guide.
- Access to OCI registries uses Kubernetes Secrets scoped to the Policy Server that needs them.

See [Security hardening: RBAC](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html#_rbac).

  **Network Enforcer**

  - `WorkloadNetworkPolicy` and `WorkloadNetworkPolicyProposal` resources are namespaced. Namespace owners
    can review proposals and promote them by setting a label, without cluster-wide permissions.
  - Two `ValidatingAdmissionPolicy` objects enforce rules for proposals. One restricts the promote label
    to `monitor` or `protect`; the other blocks changes to a proposal's owner reference.
  - The controller has cluster-wide write permissions on `NetworkPolicy` and Istio's `AuthorizationPolicy`
    objects as it creates them in every namespace.
  - The controller reads the network provider's Transport Layer Security (TLS) credentials from a Secret.
    The provider can be Hubble Relay or Goldmane. The chart grants read access to that specific Secret.

  **Runtime Enforcer**

  - `WorkloadPolicy` and `WorkloadPolicyProposal` resources are namespaced. A platform engineer selects
    the namespaces where learning runs. Application teams review proposals and promote them by setting a label.
  - A `ValidatingAdmissionPolicy` makes the `runtimeenforcer.kubewarden.io/policy` label on a Pod immutable.
    Users with Pod update permissions cannot change which policy a running Pod references.
  - The agent and controller communicate over gRPC with mutual TLS, using certificates from cert-manager.
  - To load extended Berkeley Packet Filter (eBPF) programs, the agent needs node-level privileges:
     the `BPF`, `PERFMON`, `SYS_RESOURCE`, and `SYS_PTRACE` capabilities, plus `hostPID`. 
    It does not run as a privileged container.

  **SBOM Scanner**

  - `Registry` and `ScanJob` resources are namespaced. A platform engineer manages the cluster-scoped
    configuration resources: `WorkloadScanConfiguration`, `NodeScanConfiguration`, `VEXHub`, and `NodeScanJob`.
  - A `Registry` reads its credentials from a Secret in the same namespace. Cross-namespace Secret
    references are not permitted.
  - Secret read access is restricted to the worker's `ServiceAccount`. It has cluster-wide `get`
    permission on Secrets to retrieve `Registry` credentials in any namespace. The controller cannot read Secrets.
  - Permission to change managed `Registry` and `WorkloadScanReport` resources is restricted to the
    controller's `ServiceAccount`.
  - The storage component is an aggregated application programming interface (API) server. It delegates
    request authentication and authorization to the Kubernetes API server.
  - All components authenticate to NATS with mutual TLS. The Model Context Protocol (MCP) server uses
    Basic Auth and TLS.
  - The node scanner runs as root with the `DAC_READ_SEARCH` capability and a read-only mount of the
    host root. It is not compatible with the `restricted` [Pod Security Standard](https://kubernetes.io/docs/concepts/security/pod-security-standards/).

  See [Multi-tenancy setup](https://docs.kubewarden.io/sbom-scanner/latest/en/tutorials/scanning-workloads.html) and
  [Private registries](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/private-registries.html).

- Describe how the project has addressed sovereignty.

  The project has no data-sovereignty requirements of its own.
  Policies can block traffic from the cluster to external services, and they can restrict access to namespaces or resources.

- Describe any compliance requirements addressed by the project.

  Kubewarden holds no certification against security standards such as PCI-DSS, COBIT, ISO or GDPR.
  Policies from the Kubewarden catalog help certify other workloads in Kubernetes clusters.
  See https://github.com/kubewarden/community/blob/main/security-self-assesment.md#project-compliance for more information.

- Describe the project’s High Availability requirements.

  Kubewarden does not include its own High Availability (HA) mechanism.
  Each component runs as standard Kubernetes workloads: Deployments, DaemonSets and StatefulSets.
  As a result, HA comes from the Kubernetes features that you apply to these workloads.

  **Admission Controller**

  The controller and the Policy Servers run as Deployments.
  To keep the admission webhooks available, run these Deployments with more than one replica.
  The documentation explains how to use `PodDisruptionBudgets`, Affinity and Anti-Affinity rules, resource requests and limits, and Priority Classes.

  See [Configuring Kubewarden stack for production](https://docs.kubewarden.io/admission-controller/latest/en/howtos/production-deployments.html) and
  [Configuring Policy Server for production](https://docs.kubewarden.io/admission-controller/latest/en/howtos/production-deployments.html#_policyserver_production_configuration).

  **Network Enforcer**

  The controller runs as a Kubernetes Deployment. Leader election is on by default, so you can run more than one replica for HA.
  Only the leader reconciles and writes resources. The other replicas stand by and take over if the leader fails.

  The controller is stateless. All durable state lives in the Kubernetes API server:
  observed flows become `WorkloadNetworkPolicyProposal` resources, and violations are written to the `WorkloadNetworkPolicy` status.
  The controller holds only short-lived queues in memory. It drains violation observations into the status every 30 seconds (`controller.wnpStatusUpdateInterval`).
  A restart or a crash results in the loss of the queued observations that have not been yet written.

  Enforcement does not depend on the controller.
  The controller writes native `NetworkPolicy` or Istio `AuthorizationPolicy` objects. Cilium, Calico or Istio enforce them.
  Existing policies stay in effect if the controller is down.
  The Learn and Monitor phases stop until the controller is back. The controller does not learn network flows that occur during the outage.
  The controller does not use admission webhooks. It uses `ValidatingAdmissionPolicy` objects, which the API server evaluates on its own.

  The Learn and Monitor phases depend on the service that reports the flows: Hubble Relay (Cilium), Goldmane (Calico) or ztunnel logs through a fluent-bit DaemonSet (Istio).
  The optional OpenTelemetry collector is a stateless pass-through, fronted by a Kubernetes Service, so you can scale it the same way. It is not on the enforcement path.

  **Runtime Enforcer**

  The controller runs as a Kubernetes Deployment. Leader election is on by default, so you can run more than one replica for HA.
  Only the leader reconciles and writes resources. The other replicas stand by and take over if the leader fails.

  The agent runs as a DaemonSet, one pod per node. The agent loads the eBPF programs and enforces policies on that node.
  The OpenTelemetry collector is a stateless pass-through, run as a Kubernetes Service. You can scale it directly via Kubernetes.

  The webhooks reject new policy proposals promotions and policy deletions (`failurePolicy: Fail`), if the controller is down. No learning can occur at that time.

  The default values of the Helm chart protects the agent during upgrades.
  The DaemonSet uses `maxSurge: 100%` and `maxUnavailable: 0`.
  The new agent becomes ready before the old agent stops.
  The controller and the agent use a Priority Class. Their resource requests equal their limits, so Kubernetes evicts them last.
  The chart includes a `PodDisruptionBudget` for the controller. It is off by default.

  By default, the agent blocks pods that reference a missing policy. You can set `agent.nriFailopen=true` to change this.
  To block container start when the agent is absent on a node, configure the "required plugins" feature of the container runtime.
  See [Phases](https://docs.kubewarden.io/runtime-enforcer/latest/en/explanations/phases.html) and
  [Troubleshooting](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/troubleshooting.html#_required-plugins).

  **SBOM Scanner**

  SBOM Scanner is highly available by default. The Helm chart deploys:

  - Controller: Deployment, 3 replicas, leader election on. All replicas serve the admission webhooks.
  - Storage (extension API server): Deployment, 3 replicas.
  - Worker: Deployment, 3 replicas. Workers pull jobs from a queue, so you can add replicas.
  - PostgreSQL: 3 instances managed by CloudNativePG. You can use an external PostgreSQL if you want.
  - NATS: StatefulSet with 3 pods in cluster mode, with JetStream.
  - Node worker: DaemonSet, deployed when node scanning is on.

  SBOM Scanner is the only Kubewarden component which requires persistent storage. NATS uses a  PersistentVolumeClaim (PVC). If PostresSQL is deployed via CloudNativePG then the operator handles failover and requests a PVC too.
  The webhooks (`failurePolicy: Fail`) only cover the SBOM Scanner resources. A controller outage does not block ordinary workloads.
  You cannot read scan results as long as storage or PostgreSQL are down.
  If the workers or NATS are down, scanning pauses but existing reports stay readable.

  For development, you can set each replica count to 1.
  See [Quickstart](https://docs.kubewarden.io/sbom-scanner/latest/en/quickstart.html) and
  [Helm values](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/helm-values.html).

- Describe the project’s resource requirements, including CPU, Network and Memory.

  Each Helm chart sets default CPU and memory requests and limits for its workloads.
  The defaults fit a small cluster. Adjust them via Helm values for your cluster.
  No component needs persistent network bandwidth. The components talk to the Kubernetes API server, and SBOM Scanner pulls images from OCI registries.

  **Admission Controller** ([defaults](https://github.com/kubewarden/helm-charts/blob/main/charts/admission-controller/values.yaml))

  - The chart sets requests and limits for the controller and the audit scanner.
  - The Policy Server has no default. Usage depends on the number and complexity of the policies. Set `spec.limits` and `spec.requests` on the `PolicyServer` resource accordingly.

  See [Limits and requests](https://docs.kubewarden.io/admission-controller/latest/en/howtos/production-deployments.html#_limits_and_requests).

  **Network Enforcer** ([defaults](https://github.com/kubewarden/helm-charts/blob/main/charts/network-enforcer/values.yaml))

  - The controller runs with requests equal to limits, so the Pod has the `Guaranteed` QoS class and therefore Kubernetes evicts it last under node pressure.
  - The chart also sets requests and limits for the OpenTelemetry collector and with Istio for the fluent-bit DaemonSet.
  - The controller receives a stream of network flows from the provider. The volume depends on the traffic in the cluster.

  **Runtime Enforcer** ([defaults](https://github.com/kubewarden/helm-charts/blob/main/charts/runtime-enforcer/values.yaml))

  - The controller and the agent run with requests equal to limits, so the Pods have the `Guaranteed` QoS class.
  - The agent runs on every node.
  - The documentation gives sizing recommendations by cluster size, based on benchmarks.

  See [Resource consumption](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/resource-consumption.html).

  **SBOM Scanner** ([defaults](https://github.com/kubewarden/helm-charts/blob/main/charts/sbomscanner/values.yaml))

  - The chart sets requests and limits for the controller, the storage and the workers. The storage component needs more memory because it processes SBOMs.
  - Each component runs with three replicas by default. PostgreSQL and NATS are handled separately.
  - The main network cost of the project are the workers pulling container images and the vulnerability databases from registries.

  See [Resource limits and requests](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/helm-values.html#_resource_limits_and_requests).

- Describe the project’s storage requirements, including its use of ephemeral and/or persistent storage.

  Three components are stateless: the Admission Controller, the Network Enforcer and the Runtime Enforcer.
  SBOM Scanner is the only component that needs persistent storage.

  **Stateless components**

  On startup, each component loads its configuration and secrets from Kubernetes ConfigMaps and Secrets, mounted as files in the pod.
  During runtime, the component keeps processed data in memory or in `emptyDir` volumes. Pod termination discards this data.

  The Admission Controller policies are distributed as [OCI artifacts via container registries](https://docs.kubewarden.io/admission-controller/latest/en/reference/oci-registries-support.html).
  The Network Enforcer and the Runtime Enforcer store all policy state in the Kubernetes API server, as custom resources.

  **SBOM Scanner**

  SBOM Scanner stores SBOMs and vulnerability reports in a PostgreSQL database.

  - PostgreSQL: by default, the Helm chart deploys a PostgreSQL cluster with CloudNativePG. Each instance uses a PersistentVolumeClaim of 1Gi.
    You can increase the size later, but you cannot decrease it. You can also connect SBOM Scanner to an external PostgreSQL instance.
  - NATS: the message broker runs with JetStream. Each NATS pod uses a PersistentVolumeClaim for the JetStream file store (10Gi by default).
  - Workers: the workers use `emptyDir` volumes as scratch space while they scan images.

  Deleting the SBOM Scanner namespace deletes the PersistentVolumeClaims of PostgreSQL and NATS.
  Whether the PersistentVolumes and the data behind them are also destroyed depends on the `reclaimPolicy` of the StorageClass (`Delete` removes the data, `Retain` keeps the volume).
  The chart does not configure backups. If you need to keep past reports, see [Backups](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/helm-values.html#backups).

  See [Quickstart](https://docs.kubewarden.io/sbom-scanner/latest/en/quickstart.html),
  [Helm values](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/helm-values.html) and
  [Uninstall](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/uninstall.html).

- Please outline the project’s API Design:

  - Describe the project’s API topology and conventions

    Kubewarden integrates with Kubernetes by providing a set of CRDs.
    CRDs documentation here:

    - [Admission Controller CRDs reference](https://docs.kubewarden.io/admission-controller/latest/en/reference/CRDs.html)
    - [Network Enforcer CRDs reference](https://docs.kubewarden.io/network-enforcer/latest/en/reference/crd.html)
    - [Runtime Enforcer CRDs reference](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/crd.html)
    - [SBOM Scanner CRDs reference](https://docs.kubewarden.io/sbom-scanner/latest/en/reference/crd-reference.html)

    The API follows standard Kubernetes extension patterns and is organized in groups and versions.

  - Describe the project defaults

    Each component ships one Helm chart in the [helm-charts](https://github.com/kubewarden/helm-charts) repository.
    The default values give a secure deployment configuration. The links below point to the `values.yaml` file of each chart.

    **Admission Controller** ([values.yaml](https://github.com/kubewarden/helm-charts/blob/main/charts/admission-controller/values.yaml))

    The `admission-controller` chart replaces the three previous charts: `kubewarden-crds`, `kubewarden-controller` and `kubewarden-defaults`.

    - The chart deploys a default Policy Server. Policies without `spec.policyServer` run on it.
    - The chart can deploy six recommended policies. They are off by default. When on, they run in `monitor` mode.
    - Policy mode: `protect`. A policy in `monitor` mode can move to `protect`. The opposite move is not permitted.
    - Failure policy: `Fail`. If the Policy Server does not answer, the API server rejects the request.
    - Background audit: on. The audit scanner runs every hour and checks existing resources against the policies.
    - Policy evaluation timeout: 10 seconds.
    - Metrics and tracing: off.

    **Network Enforcer** ([values.yaml](https://github.com/kubewarden/helm-charts/blob/main/charts/network-enforcer/values.yaml))

    - Network provider: Istio ambient mode.
    - A new workload starts in the Learn phase.
    - A promoted `WorkloadNetworkPolicy` starts in `monitor` mode.

    **Runtime Enforcer** ([values.yaml](https://github.com/kubewarden/helm-charts/blob/main/charts/runtime-enforcer/values.yaml))

    - Learning: on in all namespaces.
    - A promoted `WorkloadPolicy` starts in `monitor` mode.
    - Fail closed: a Pod that references a missing policy does not start. Set `agent.nriFailopen=true` to change this.

    **SBOM Scanner** ([values.yaml](https://github.com/kubewarden/helm-charts/blob/main/charts/sbomscanner/values.yaml))

    - Three replicas for the controller, the storage and the workers. PostgreSQL runs with three instances through CloudNativePG.
    - Workload scanning and node scanning: on.
    - The chart does not create `Registry` or scan configuration resources. You create them, and you set the scan interval on each one.
    - The chart seeds two `VEXHub` resources, for the Rancher and Aqua Security VEX repositories.
    - MCP server: off. 
    - Telemetry export: off.

  - Outline any additional configurations from default to make reasonable use of the project

    Each component documents how to configure it for production:

    - [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/howtos/production-deployments.html)
    - [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/production-deployments.html)
    - [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/production-deployments.html)
    - [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/production-deployments.html)

    The Admission Controller also has a [Security Hardening](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html) guide, covering RBAC, Pod Security Admission, security contexts and the capabilities exposed to namespaced policies.

  - Describe any new or changed API types and calls \- including to cloud providers \- that will result from this project being enabled and used

    Not applicable.

  - Describe compatibility of any new or changed APIs with API servers, including the Kubernetes API server

    All components extend the Kubernetes API with custom resources. They do not change existing Kubernetes APIs.
    Each component declares the Kubernetes versions that it supports in its Helm chart (`kubeVersion`) and in its documentation.

    **Admission Controller**

    The chart supports Kubernetes 1.19 or later.
    Features that depend on a newer Kubernetes version are turned off at runtime if the cluster does not meet the required version.
    Policies that depend on a specific Kubernetes API version, for example the [deprecated-api-versions-policy](https://github.com/kubewarden/deprecated-api-versions-policy), declare it.

    **Network Enforcer**

    Kubernetes 1.31 or later. The component installs two `ValidatingAdmissionPolicy` resources in `admissionregistration.k8s.io/v1`.
    This API went GA in Kubernetes 1.30, but 1.31 is the oldest version that the project tests against.
    The component also depends on the network provider APIs: Kubernetes `NetworkPolicy` for Calico and Cilium, and Istio `AuthorizationPolicy` for Istio ambient mode.
    See [Compatibility](https://docs.kubewarden.io/network-enforcer/latest/en/reference/compatibility.html).

    **Runtime Enforcer**

    Kubernetes 1.31 or later, because the component uses a CEL-based `ValidatingAdmissionPolicy`.
    The component also depends on the node: a kernel of 5.8 or later on x86_64 and 6.4 or later on aarch64, and a container runtime with NRI (containerd or CRI-O).
    See [Compatibility](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/compatibility.html).

    **SBOM Scanner**

    The storage component is an extension API server, registered with an `APIService`.
    It depends on the API aggregation layer of the Kubernetes API server, and it delegates authentication and authorization to that server.

  - Describe versioning of any new or changed APIs, including how breaking changes are handled

    The project follows [semantic versioning](https://semver.org/) for its releases. Additional details are in the answer to the next question.
    For CRDs, the stable version in use is `v1`. In line with Kubernetes conventions, breaking changes to the API trigger a new version. Non-breaking enhancements are introduced within the existing version.
    CRDs release can be as alpha or beta versions before reaching stability.
    Alpha versions (`v1alphaX`) are experimental and can change or disappear between releases.
    Beta versions (`v1betaX`) are more stable, with fewer breaking changes expected, but are still subject to refinement before becoming stable.

  - Describe the project’s release processes, including major, minor, and patch releases.

    All components follow [semantic versioning](https://semver.org/).

    Each component is released as one unit.
    All the binaries, container images and CRDs of a component share one `MAJOR.MINOR.PATCH` version.
    The maintainers tag every piece together, even the ones that did not change since the last release.
    For example, the Admission Controller tags the controller, the Policy Server, the audit scanner, `kwctl` and the CRDs together.
    This gives each component one version number. A user reports that number, and the maintainers know the exact version of every piece.

    For each release, the maintainers decide if the changes call for a major, minor or patch bump:

    - A breaking change (for example a removed CRD field) bumps the major version, or the minor version while the component is below 1.0.
    - New features bump the minor version.
    - Bug fixes bump the patch version.

    The Helm chart of each component carries two version fields. The `appVersion` field always matches the component version.
    The chart `version` field follows its own SemVer. The chart can change, for example with a new default value, without a change to the component.
    A new minor version of a component also bumps the chart `version`.

    Each component documents its supported upgrade path:

    - [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/reference/upgrade-path.html)
    - [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/reference/upgrade-path.html)
    - [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/upgrade-path.html)
    - [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/reference/upgrade-path.html)

    The [helm-charts CONTRIBUTING.md](https://github.com/kubewarden/helm-charts/blob/main/CONTRIBUTING.md) describes how a tagged release becomes a published chart.

    Kubewarden policies and their SDKs follow their own independent lifecycle.
    Each policy is versioned on its own, at its own pace, because the runtime components stay backward compatible with policies built against older SDKs.

### Installation

- Describe how the project is installed and initialized, e.g. a minimal install with a few lines of code or does it require more complex integration and configuration?

  Each component installs with one Helm chart from the `https://charts.kubewarden.io` repository.
  The charts are also listed on ArtifactHUB. A minimal install is one `helm install` command per component.
  The components do not depend on each other. You install only the components that you need.

  - Admission Controller: no prerequisites. The chart installs the CRDs, the controller, the audit scanner and a default Policy Server.
    See [Quick start](https://docs.kubewarden.io/admission-controller/latest/en/quick-start.html#_installation).
  - Network Enforcer: requires cert-manager, cert-manager-csi-driver and one configured network provider (Istio ambient mode, Calico or Cilium).
    You select the provider with a Helm value.
    See [Quick start](https://docs.kubewarden.io/network-enforcer/latest/en/quickstart.html).
  - Runtime Enforcer: requires cert-manager, cert-manager-csi-driver and a container runtime with NRI enabled.
    See [Quick start](https://docs.kubewarden.io/runtime-enforcer/latest/en/quickstart.html).
  - SBOM Scanner: requires cert-manager, CloudNativePG and a default Storage Class.
    See [Quickstart](https://docs.kubewarden.io/sbom-scanner/latest/en/quickstart.html).

- How does an adopter test and validate the installation?

  Each quick start has a "Verify the deployment" step. It lists the expected Pods and their status.
  Then the quick start walks through a first end-to-end use of the component:

  - Admission Controller: deploy a policy and send a request that the policy rejects.
    See [Enforce your first policy](https://docs.kubewarden.io/admission-controller/latest/en/quick-start.html#_example_enforce_your_first_policy).
  - Network Enforcer: deploy a sample application, generate traffic, and inspect the generated `WorkloadNetworkPolicyProposal`. Then promote it and observe a violation.
    See [Verify the deployment](https://docs.kubewarden.io/network-enforcer/latest/en/quickstart.html#_verify-the-deployment).
  - Runtime Enforcer: deploy a sample application and inspect the generated `WorkloadPolicyProposal`. Then promote it and observe a violation.
    See [Verify the deployment](https://docs.kubewarden.io/runtime-enforcer/latest/en/quickstart.html#_verify-the-deployment).
  - SBOM Scanner: create a `Registry` and a `ScanJob`, then wait for the SBOM and the vulnerability report.
    See [Verify the deployment](https://docs.kubewarden.io/sbom-scanner/latest/en/quickstart.html#_verify_the_deployment).

### Security

- Please provide a link to the project’s cloud native [security self assessment](https://tag-security.cncf.io/community/assessments/).

  Security self-assessment: https://github.com/kubewarden/community/blob/main/security-self-assesment.md

- Please review the [Cloud Native Security Tenets](https://github.com/cncf/tag-security/blob/main/community/resources/security-whitepaper/secure-defaults-cloud-native-8.md) from TAG Security.

  - How are you satisfying the tenets of cloud native security projects?

    1. **Make security a design requirement**

       Each architecture page lists the design principles of the component and a "Trust boundaries" section.
       The trust boundaries name who can write each resource, which component holds which credential, and how the components authenticate to each other.

       **Admission Controller**

       - **Threat model**: the team evaluates the controller and the Policy Server against the Kubernetes SIG Security Admission Control Threat Model.
         See the [Threat Model](https://docs.kubewarden.io/admission-controller/latest/en/reference/threat-model.html) reference.
       - **WebAssembly sandboxing**: policies run inside isolated WebAssembly sandboxes. A policy cannot interfere with other policies or with the host.
       - **Context-aware policies**: a policy declares the resources it reads, in read-only mode. The Policy Server blocks all other resources.

       **Network Enforcer** ([design principles](https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html#_design_principles), [trust boundaries](https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html#_trust_boundaries))

       - **Observe before you enforce**: observation has no side effect. Nothing blocks traffic until you promote a proposal.
       - **Promotion is a label, not a side effect**: the controller never turns a proposal into a policy on its own. A reviewer approves it and can keep the approval in Git.
       - **Learn from the data plane, do not add one**: the component installs no probe, sidecar or node agent of its own.
       - The controller is the only writer of proposals, policies and native policy objects. No component writes a Pod.
       - Two `ValidatingAdmissionPolicy` objects guard the promote label and the owner reference of a proposal. Both fail closed.

       **Runtime Enforcer** ([design principles](https://docs.kubewarden.io/runtime-enforcer/latest/en/explanations/architecture.html#_design_principles), [trust boundaries](https://docs.kubewarden.io/runtime-enforcer/latest/en/explanations/architecture.html#_trust_boundaries))

       - **Enforce in the kernel, before the process starts**: a process that is not allowed never starts. There is no agent in the container to bypass.
       - **Bind before the entrypoint**: the entrypoint is subject to the policy, and so is a Pod that lives for one second.
       - **Fail closed**: a Pod that names a policy the agent does not know does not start. A mistake in a label does not leave a workload without protection.
       - The controller owns the policy, the agent owns the node. Only the agent loads a policy into the kernel. No component writes a Pod.
       - The agent is an NRI plugin with a read-only socket. It can stop a container from starting, and nothing else.

       **SBOM Scanner** ([design principles](https://docs.kubewarden.io/sbom-scanner/latest/en/explanations/architecture.html#_design_principles), [trust boundaries](https://docs.kubewarden.io/sbom-scanner/latest/en/explanations/architecture.html#_trust_boundaries))

       - **Namespaces give multi-tenancy**: a `Registry` and its results live in one namespace. A team reads its own reports with its own RBAC.
       - **A job runs on a frozen input**: a change to a `Registry` during a scan does not change the running scan.
       - Only the worker Service Account can read Secrets, and only to get registry credentials. The controller cannot.
       - Only the controller Service Account can write a `WorkloadScanReport` or a managed `Registry`. A webhook and a storage admission plugin enforce this.
       - The node worker is the only component with access to the host. Its mount is read-only.

    2. **Applying secure configuration has the best user experience**

       - **Helm charts with secure defaults**: the Helm chart of each component ships secure defaults. A plain `helm install` gives a secure deployment.
         TLS is on by default for all components, and each workload runs under its own Service Account with limited permissions.

         The `admission-controller` chart creates a default Policy Server and can install a set of recommended security policies (`recommendedPolicies.enabled=true`).

       - **One production guide per component**: each component has a production deployments page. The page lists the few settings that a production cluster needs on top of the defaults, with the reason for each one.
         The pages are linked in the answer to "Outline any additional configurations from default" above.
       - **Admission Controller hardening guide**: the Admission Controller also has a [Security Hardening](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html)
         guide and a [Webhooks hardening](https://docs.kubewarden.io/admission-controller/latest/en/reference/security-hardening/webhooks-hardening.html) reference.
         They cover RBAC, Pod Security Admission, security contexts, the capabilities exposed to namespaced policies, and optional mutual TLS between the API server and the Policy Servers.

    3. **Selecting insecure configuration is a conscious decision**

       Every component ships with secure defaults. To loosen a default, the user must set a named value on purpose.
       No insecure setting is on by default, and no insecure setting is hidden inside a broader option.
       The documentation names the risk next to each setting.

       - **Admission Controller**: the Policy Server pulls policies only over HTTPS with trusted certificates. To accept an untrusted or plain-text registry, the user lists it under `insecureSources`.
       - **Network Enforcer**: the controller connects to the network provider over TLS. To use plain text, the user sets `tls.mode=insecure` for that provider.
       - **Runtime Enforcer**: the agent fails closed. A Pod that names a policy the agent does not know does not start. To let such a Pod start, the user sets `agent.nriFailopen=true`.
       - **SBOM Scanner**: the workers verify the TLS certificate of every registry. To skip the check for one registry, the user sets `spec.insecure: true` on that `Registry`.

       `monitor` mode is the other explicit choice. The three enforcement components support it, and in that mode a policy reports violations and blocks nothing.
       The Admission Controller creates a policy in `protect` mode unless the user asks for `monitor`. The two enforcers promote a proposal to `monitor` first, and the user moves it to `protect` as a second step.

       The answer to "How do you recommend users alter security defaults" below lists every loosening setting, with links.

    4. **Transition from insecure to secure state is possible**

       - **Hardening guide**: the Admission Controller [Security Hardening](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html) guide moves a default install to a hardened one.
       - **Admission Controller, monitor to protect only**: a policy in `monitor` mode can move to `protect`. The opposite move is not permitted. This is a deliberate choice: a user cannot downgrade a policy by accident.
       - **Network Enforcer and Runtime Enforcer, three phases**: a workload starts in Learn, where nothing is blocked. You promote it to Monitor, where violations are reported. Then you move it to Protect.
         Both enforcers permit the move back from Protect to Monitor, so you can respond to a false positive without a redeploy.
       - **Gradual rollout**: Admission Controller policies apply to selected namespaces and resources through `namespaceSelector`, `matchConditions` and `rules`.
         The Runtime Enforcer limits learning to selected namespaces with `learning.namespaceSelector`. The Network Enforcer creates one proposal per workload, so you promote one workload at a time.

    5. **Secure defaults are inherited**

       - **Admission Controller**: integrates through admission webhooks and inherits the authentication and authorization of the Kubernetes API server. Policies inherit the memory isolation of WebAssembly.
       - **Network Enforcer**: writes native `NetworkPolicy` and Istio `AuthorizationPolicy` objects. The CNI or the mesh enforces them. If the controller stops, the policies stay in place.
         The admission guards are `ValidatingAdmissionPolicy` objects that the API server evaluates on its own, with no webhook to keep up.
       - **Runtime Enforcer**: enforces in the kernel with eBPF, so the check happens before the process starts. The agent plugs into the container runtime through NRI.
       - **SBOM Scanner**: the storage component is an aggregated API server. It delegates authentication and authorization to the Kubernetes API server, so a report follows the same RBAC as any other Kubernetes resource.
       - **All components**: TLS on every connection. The three newer components get their certificates from cert-manager. The Admission Controller rotates its own.

    6. **Exception lists have first class support**

       - **Admission Controller**: `namespaceSelector` and `matchConditions` exclude resources or namespaces from a policy. The audit scanner can skip namespaces. Multiple Policy Servers isolate tenants.
       - **Network Enforcer**: you add a rule to the `WorkloadNetworkPolicy` to allow expected traffic. You acknowledge a violation with the `networkenforcer.kubewarden.io/acknowledge-<id>` annotation to mark it as reviewed noise.
       - **Runtime Enforcer**: you add a binary to the allow list (`kubectl runtime-enforcer policy allow`). You acknowledge a violation. Containers not listed in a policy are not enforced. `learning.namespaceSelector` excludes namespaces from learning.
       - **SBOM Scanner**: VEX documents from a `VEXHub` mark vulnerabilities as not exploitable; the report shows them as `suppressed`. A `Registry` filters by platform, repository and CEL `matchConditions`. Node scans accept `skipPatterns`.

    7. **Secure defaults protect against pervasive vulnerability exploits**

       The controllers, workers, storage and collector Pods of all components run as a non-root user, with `allowPrivilegeEscalation: false`, all Linux capabilities dropped and the `RuntimeDefault` seccomp profile.
       The Pods that process untrusted or external input use a read-only root file system: the Admission Controller Policy Servers, which run policy code, and every SBOM Scanner Pod, which processes images and SBOMs.
       Each workload runs under its own Service Account with minimal RBAC.
       Container images use a `scratch` or distroless base and contain only the component binary.

       Three workloads need more than this, because of what they do. Each one is documented, and each one is scoped to the minimum:

       - **Runtime Enforcer agent**: loads eBPF programs, so it holds the `BPF`, `PERFMON`, `SYS_RESOURCE` and `SYS_PTRACE` capabilities and `hostPID`. It is not a privileged container.
         The documentation lists which Admission Controller policies reject it and why. See [Agent security context](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/production-deployments.html#_agent_security_context).
       - **SBOM Scanner node worker**: reads the host file system, so it runs as root with `DAC_READ_SEARCH` and a read-only mount of `/`. It has no host network and no host PID namespace.
         It is not compatible with the `restricted` or `baseline` Pod Security Standard. See [Node scan worker](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/production-deployments.html#_node_scan_worker).
       - **Network Enforcer fluent-bit** (Istio only): reads the ztunnel log files on each node, so it runs as root with a read-only mount of `/var/log`.
         See [fluent-bit security context](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/production-deployments.html#_fluent_bit_security_context).

    8. **Security limitations of a system are explainable**

       - **Architecture and trust boundaries**: each component has an architecture page that names its trust boundaries. Links are in tenet 1 above.
       - **Known limitations**: the [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/reference/known_limitations.html) and the [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/known_limitations.html) each publish a Known limitations page. The pages separate design decisions from constraints inherited from the data plane, the kernel or the container runtime.
       - **Stated caveats**: the Network Enforcer documents that Monitor evaluation is best-effort, and that an attacker active during learning becomes a rule. The Runtime Enforcer documents that a node without an agent Pod gives no protection, and how to use the "required plugins" feature of the container runtime to close that gap.
       - **Threat model**: the Admission Controller maintains a public [threat model](https://docs.kubewarden.io/admission-controller/latest/en/reference/threat-model.html).
       - **Non-goals**: each component lists its non-goals on its use-cases page. Links are in the Scope section above.

- How do you recommend users alter security defaults in order to "loosen" the security of the project? Please link to any documentation the project has written concerning these use cases.

  Each loosening is an explicit setting. The defaults stay secure, and the documentation names the risk next to the setting.
  The three enforcement components (Admission Controller, Network Enforcer and Runtime Enforcer) support a `monitor` mode. In this mode, a policy reports violations and blocks nothing.

  **Admission Controller**

  - Pull policies from registries with untrusted certificates or without TLS: [Insecure sources](https://docs.kubewarden.io/admission-controller/latest/en/howtos/policy-servers/01-custom-cas.html#_insecure_sources).

  **Network Enforcer**

  - Connect to the network provider in plain text: `controller.provider.cilium.tls.mode=insecure` or `controller.provider.istio.tls.mode=insecure`. See [Compatibility](https://docs.kubewarden.io/network-enforcer/latest/en/reference/compatibility.html).
  - Turn off the OpenTelemetry export with `telemetry.collectorStrategy=none`. Learning, monitor and protect keep working. Violations stay in the policy status.

  **Runtime Enforcer**

  - Fail open: `agent.nriFailopen=true`. A Pod that references a missing policy starts without protection. See [Fail-open](https://docs.kubewarden.io/runtime-enforcer/latest/en/glossary.html#_fail-open).

  **SBOM Scanner**

  - Connect to a registry without TLS verification: `spec.insecure: true` on a `Registry` or on the `WorkloadScanConfiguration`. See [Scanning workloads](https://docs.kubewarden.io/sbom-scanner/latest/en/tutorials/scanning-workloads.html).
  - Serve the MCP server over plain HTTP: `mcp.disableTLS=true`. See [MCP server](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/mcp-server.html).

- Security Hygiene

  - Please describe the frameworks, practices, and procedures the project uses to maintain the basic health and security of the project.

    **Dependency management**

    Kubewarden has a [Security and dependency policy](https://github.com/kubewarden/.github/blob/main/SECURITY.md#supported-versions). We use automation tools such as Renovatebot and Updatecli to keep dependencies up to date in all the repositories.

    **Vulnerability scanning**

    Kubewarden's container images are scanned in ArtifactHub.
    The repositories use GitHub's security features to scan for vulnerabilities in dependencies, alongside language-specific tools like `cargo-audit` for Rust projects and `govulncheck` for Go projects.

    **Supply chain**

    The container images, the Helm charts and the binaries reach SLSA Build Level 3.
    The "secure software supply chain best practices" answer below lists the level of each artifact.

  - Describe how the project has evaluated which features will be a security risk to users if they are not maintained by the project?

    The project checks each component for features that become a security risk
    without maintenance. Two patterns repeat: stale data, and a dependency on an
    external system that can change without notice.

    **Admission Controller**

    - The policy catalog is the main risk. A policy that does not track new Kubernetes API fields can stop matching a request.
      The request then passes. This is a silent failure, not a crash.
    - The WebAssembly sandbox limits a different risk. It stops a buggy or malicious policy from reaching outside its own process.

    **SBOM Scanner**

    - The vulnerability database is an external dependency. SBOM Scanner pulls Trivy databases from Aqua Security. A stale feed can miss a new CVE.
    - VEX hubs carry the same risk. A stale VEX document can keep hiding a vulnerability that is now exploitable.
    - Mitigation: the stored SBOM is the source of truth. A database refresh rescans every stored SBOM without a new image pull, so a fix reaches
      every report fast.

    **Runtime Enforcer**

    - The agent loads eBPF programs into the kernel. A kernel upgrade can break program loading on a node.
      The failure is visible, not silent. A Pod that names a missing or broken policy does not start. This is the fail-closed default.

    **Network Enforcer**

    - The controller depends on provider adapters: Hubble, Goldmane, and ztunnel logs. A broken adapter stops the Learn and the Monitor phases.
    - Protect mode does not depend on the controller. The CNI or the mesh keeps enforcing the native `NetworkPolicy` or `AuthorizationPolicy`
      objects on its own.

    All four components use Renovate and Updatecli to track dependencies (see Security Hygiene above). Every container image and binary carries an SBOM and SLSA
    Build Level 3 provenance, so a stale dependency stays visible in the supply chain record.

- Cloud Native Threat Modeling

  - Explain the least minimal privileges required by the project and reasons for additional privileges.

    Every workload runs under its own Service Account. Each Service Account holds the
    smallest set of RBAC rules that its workload needs. No chart grants a wildcard.
    Most Pods run as a non-root user, with all Linux capabilities dropped. The ones
    that need more are listed below, each with its reason.

    **Admission Controller**

    - The controller and each Policy Server have separate Service Accounts.
    - A context-aware policy declares the resources it reads. The Policy Server grants
      read access to those resources only.
    - The audit scanner Service Account is bound to the `view` ClusterRole, because it
      must read the resources it audits in every namespace.
    - All Pods pass the `restricted` Pod Security Standard.
      See [Security Hardening: RBAC](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html#_rbac)
      and [Pod Security Admission](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html#_pod_security_admission).

    **Network Enforcer**

    - The controller holds cluster-wide write on `NetworkPolicy` and Istio
      `AuthorizationPolicy`. It creates those objects in every namespace that has a
      promoted policy.
    - The controller reads one Secret: the TLS client certificate of the network
      provider. The chart grants that through a Role scoped to that one Secret.
    - With the Istio provider, a fluent-bit DaemonSet runs as root with a read-only
      mount of `/var/log`, to read the ztunnel log files on each node. It does not
      pass `restricted`.
      See [fluent-bit security context](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/production-deployments.html#_fluent_bit_security_context).

    **Runtime Enforcer**

    - The controller runs as non-root and passes `restricted`.
    - The agent needs node-level access to do its job. It holds the `BPF`, `PERFMON`,
      `SYS_RESOURCE` and `SYS_PTRACE` capabilities, `hostPID`, and a read-only mount of
      the NRI socket. It runs unconfined under AppArmor. It is not a privileged
      container. It does not pass `restricted` or `baseline`.
      The documentation lists which Admission Controller policies reject the agent
      and why. See [Agent security context](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/production-deployments.html#_agent_security_context).

    **SBOM Scanner**

    - The worker is the only Service Account that can read Secrets. It needs
      `get` on Secrets cluster-wide, to read the registry credentials that a
      `Registry` names in its own namespace. The controller cannot read Secrets.
    - Only the controller Service Account can write a `WorkloadScanReport` or a
      managed `Registry`. A webhook and a storage admission plugin enforce this.
    - The node worker runs as root with the `DAC_READ_SEARCH` capability and a
      read-only mount of `/`, to read the host file system. It has no host network
      and no host PID namespace. It does not pass `restricted` or `baseline`.
      See [Node scan worker](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/production-deployments.html#_node_scan_worker).

    The "Trust boundaries" section of each architecture page states who can write each
    resource and which component holds which credential. Links are in tenet 1 above.

  - Describe how the project is handling certificate rotation and mitigates any issues with certificates.

    **Admission Controller**

    The controller manages all certificates of the stack without cert-manager.
    The Helm chart generates a root CA and the webhook certificates at install time.
    A reconciliation loop renews the leaf certificates and the root CA before they expire. The rotation causes no downtime.
    See [Certificate rotation](https://docs.kubewarden.io/admission-controller/latest/en/explanations/certificates.html).

    **Network Enforcer, Runtime Enforcer and SBOM Scanner**

    These components delegate certificate management to cert-manager, which is a prerequisite.
    Each chart creates a self-signed CA `Issuer` and the `Certificate` resources for its components. cert-manager renews them before they expire.
    The Network Enforcer and the Runtime Enforcer mount the certificates through the cert-manager CSI driver.
    SBOM Scanner uses cert-manager for the storage API server, the controller webhook, NATS mutual TLS and the MCP server.
    See the "Trust boundaries" section of each architecture page:
    [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/explanations/architecture.html#_trust_boundaries),
    [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/explanations/architecture.html#_trust_boundaries),
    [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/explanations/architecture.html#_trust_boundaries).

  - Describe how the project is following and implementing [secure software supply chain best practices](https://project.linuxfoundation.org/hubfs/CNCF_SSCP_v1.pdf)

    The project follows the five areas of the CNCF paper: source code, materials,
    build pipelines, artifacts and deployments.

    **Source code.** Every change lands through a reviewed pull request. Release tags
    are immutable. The component repositories and `helm-charts` require signed
    commits. CodeQL scans the Admission Controller and SBOM Scanner code. `zizmor`
    lints the GitHub Actions workflows of all components. OpenSSF Scorecard runs on
    the Admission Controller repository.

    **Materials.** The Security Hygiene answer above describes dependency tracking.
    Every container image and binary ships with an SPDX SBOM. A Wasm policy
    ships one when its release enables it.

    **Build pipelines.** All builds run in GitHub Actions on GitHub-hosted runners,
    and every action is pinned to a commit SHA. One reusable workflow,
    [`container-release.yml`](https://github.com/kubewarden/github-actions/blob/main/.github/workflows/container-release.yml)
    in `kubewarden/github-actions`, builds the container images of all four
    components. The Helm charts and the binaries (`kwctl`, the Runtime Enforcer
    kubectl plugin and `wpgen`) are built by reusable workflows in their own
    repositories. The build, the signature and the provenance attestation run under
    the identity of the reusable workflow, and no step of the calling workflow can
    alter them. The job that compiles has no permission to sign, and the job that
    signs runs no code from the repository. This is what gives SLSA Build Level 3.

    **Artifacts.** Container images, Helm charts, binaries and Wasm policies
    are signed with Sigstore cosign, keyless, with the GitHub Actions OIDC identity.
    The provenance level differs by artifact:

    - Container images of all four components: SLSA Build Level 3 provenance,
      published with `actions/attest`. Verify it with `gh attestation verify` or
      `cosign`.
    - Helm charts and binaries: SLSA Build Level 3 provenance.
    - Wasm policies: signature only, no provenance attestation yet.

    Each component documents the verification commands:
    [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/tutorials/verifying-kubewarden.html),
    [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/tutorials/verifying-network-enforcer.html),
    [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/tutorials/verifying-runtime-enforcer.html),
    [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/tutorials/verifying-sbom-scanner.html).

    **Deployments.** The verification pages above give the commands to check an
    image or a chart before it is deployed. The Admission Controller has one more
    moving part. Its policies are Wasm modules that the Policy Server pulls from an
    OCI registry at run time, so a policy is code that enters the cluster after the
    install. Because of that, the Policy Server verifies policies before it loads
    them: when an operator sets a
    [verification config](https://docs.kubewarden.io/admission-controller/latest/en/reference/verification-config.html),
    the Policy Server checks the signature of every policy against it and refuses to
    start when a policy fails the check. See
    [Secure supply chain](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/secure-supply-chain.html)
    in the Admission Controller documentation.

## Day 1 \- Installation and Deployment Phase

### Project Installation and Configuration

- Describe what project installation and configuration look like.

  Each component installs with one Helm chart from `https://charts.kubewarden.io`.
  Configuration is Helm values at install time, plus Kubernetes custom resources at
  run time. The charts are also listed on ArtifactHUB.

  Every component documents the same five steps: a quick start, a production
  deployment guide, the supported upgrade path, the compatibility requirements and
  the uninstall procedure. The quick start installs the prerequisites, installs the
  chart, verifies the Pods, and runs one end-to-end example.

  **Admission Controller**

  - [Quick start](https://docs.kubewarden.io/admission-controller/latest/en/quick-start.html)
  - [Production deployments](https://docs.kubewarden.io/admission-controller/latest/en/howtos/production-deployments.html)
  - [Upgrade path](https://docs.kubewarden.io/admission-controller/latest/en/reference/upgrade-path.html)
  - [Dependency matrix](https://docs.kubewarden.io/admission-controller/latest/en/reference/dependency-matrix.html)
  - [Uninstall](https://docs.kubewarden.io/admission-controller/latest/en/quick-start.html#_uninstall)
  - Also: [Security hardening](https://docs.kubewarden.io/admission-controller/latest/en/howtos/security-hardening/security-hardening.html),
    [Air-gapped installation](https://docs.kubewarden.io/admission-controller/latest/en/howtos/airgap/01-requirements.html),
    [Large-scale environments](https://docs.kubewarden.io/admission-controller/latest/en/howtos/deploy-at-scale.html),
    [ArgoCD](https://docs.kubewarden.io/admission-controller/latest/en/howtos/argocd-installation.html)
    and [Rancher Fleet](https://docs.kubewarden.io/admission-controller/latest/en/howtos/Rancher-Fleet.html) installation.

  **Network Enforcer**

  - [Quick start](https://docs.kubewarden.io/network-enforcer/latest/en/quickstart.html).
    It covers the setup of the network provider: Istio ambient mode, Calico or Cilium.
  - [Production deployments](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/production-deployments.html)
  - [Upgrade path](https://docs.kubewarden.io/network-enforcer/latest/en/reference/upgrade-path.html)
  - [Compatibility](https://docs.kubewarden.io/network-enforcer/latest/en/reference/compatibility.html)
  - [Uninstall](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/uninstall.html)

  **Runtime Enforcer**

  - [Quick start](https://docs.kubewarden.io/runtime-enforcer/latest/en/quickstart.html)
  - [Production deployments](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/production-deployments.html)
  - [Upgrade path](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/upgrade-path.html)
  - [Compatibility](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/compatibility.html).
    It lists the kernel options that eBPF needs.
  - [Uninstall](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/uninstall.html)
  - Also: [Learning mode configuration](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/learning_mode_configuration.html)
    and [Resource consumption](https://docs.kubewarden.io/runtime-enforcer/latest/en/reference/resource-consumption.html).

  **SBOM Scanner**

  - [Quick start](https://docs.kubewarden.io/sbom-scanner/latest/en/quickstart.html)
  - [Production deployments](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/production-deployments.html)
  - [Upgrade path](https://docs.kubewarden.io/sbom-scanner/latest/en/reference/upgrade-path.html)
  - [Compatibility](https://docs.kubewarden.io/sbom-scanner/latest/en/reference/compatibility.html)
  - [Uninstall](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/uninstall.html)
  - Also: [Helm values](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/helm-values.html),
    [Air gap support](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/airgap-support.html)
    and [Private registries](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/private-registries.html).

### Project Enablement and Rollback

- How can this project be enabled or disabled in a live cluster? Please describe any downtime required of the control plane or nodes.

  You enable a component with `helm install` and remove it with `helm uninstall`.
  Neither step restarts the control plane or reboots a node. The CRDs and the
  user-created custom resources stay in place after `helm uninstall`; the next
  questions cover the cleanup.

  For an incident, each enforcing component documents an emergency disable
  procedure. It stops the blocking without an uninstall, and it has a restore
  step that brings protection back:

  - [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/howtos/emergency-disable.html)
  - [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/emergency-disable.html)
  - [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/emergency-disable.html)

  The SBOM Scanner enforces nothing, so it has no emergency procedure. A removal
  has no effect on running workloads.

- Describe how enabling the project changes any default behavior of the cluster or running workloads.

  A default install of any component enforces nothing. Each enforcement path needs
  a second step by the operator: create a policy, promote a proposal, or create a
  scan configuration. The changes that happen at install time are listed below.

  All four components register admission webhooks with `failurePolicy: Fail`. Every
  one of those webhooks matches only the component's own custom resources. None
  matches Pods or any other Kubernetes resource.

  **Admission Controller**

  - Deploys one Policy Server named `default` with no policies. No admission request
    is evaluated until the operator creates a policy.
  - The recommended policies are off by default. When turned on, they start in
    `monitor` mode. A policy in `monitor` mode reports a rejection instead of
    enforcing it. It blocks nothing.
  - The audit scanner runs every hour. It reads existing resources and writes reports.
    It changes nothing.

  **Network Enforcer**

  - Starts in the Learn phase in every namespace. On Calico and Cilium it learns every
    flow the CNI reports. On Istio it learns the namespaces labelled
    `istio.io/dataplane-mode=ambient`.
  - Writes `WorkloadNetworkPolicyProposal` objects into the workload namespaces.
  - Creates no `NetworkPolicy` or `AuthorizationPolicy` until the operator promotes a
    proposal. No traffic is blocked.

  **Runtime Enforcer**

  - The agent registers as an NRI plugin on every node. The container runtime calls
    the agent on every container start. A Pod without the policy label starts as
    usual.
  - Learning is on in every namespace. The agent records which executables run and
    writes `WorkloadPolicyProposal` objects.
  - No executable is blocked until the operator promotes a proposal and a Pod
    template carries the policy label.

  **SBOM Scanner**

  - Adds one API group to the cluster, `storage.sbomscanner.kubewarden.io`, served by
    an aggregated API server. `kubectl api-resources` shows the new kinds.
  - Workload and node scanning are inactive until the operator creates a
    `WorkloadScanConfiguration` or a `NodeScanConfiguration`.
  - Seeds two `VEXHub` resources with public VEX feeds. They are reference data.

- Describe how the project tests enablement and disablement.

  The end-to-end test suite of each component installs the Helm chart in a fresh cluster, runs the tests, and uninstalls the chart.

- How does the project clean up any resources created, including CRDs?

  Each component documents the full cleanup: `helm uninstall`, then deletion of the CRDs, then deletion of the namespace.
  The CRDs carry `helm.sh/resource-policy: keep`, so a `helm uninstall` does not delete the custom resources by accident.
  Deleting a CRD deletes every custom resource of that type in the cluster.

  - [Admission Controller](https://docs.kubewarden.io/admission-controller/latest/en/quick-start.html#_uninstall)
  - [Network Enforcer](https://docs.kubewarden.io/network-enforcer/latest/en/howtos/uninstall.html). Kubernetes removes the generated `NetworkPolicy` and `AuthorizationPolicy` objects through owner references.
  - [Runtime Enforcer](https://docs.kubewarden.io/runtime-enforcer/latest/en/howtos/uninstall.html). A `WorkloadPolicy` cannot be deleted while a Pod references it.
  - [SBOM Scanner](https://docs.kubewarden.io/sbom-scanner/latest/en/howtos/uninstall.html). Deleting the namespace removes the PersistentVolumeClaims and their PersistentVolumes.

### Rollout, Upgrade and Rollback Planning

- How does the project intend to provide and maintain compatibility with infrastructure and orchestration management tools like Kubernetes and with what frequency?

  Each component declares the Kubernetes versions it supports in its Helm chart
  (`kubeVersion`) and on its compatibility page. The Admission Controller supports
  Kubernetes 1.19 or later and turns off features at run time when the cluster is
  too old for them. The Network Enforcer and the Runtime Enforcer require 1.31 or
  later, because they depend on `ValidatingAdmissionPolicy` in `admissionregistration.k8s.io/v1`.
  The SBOM Scanner depends on the API aggregation layer.

  Each component also declares the infrastructure it depends on, with a minimum
  version: the network provider for the Network Enforcer (Istio ambient, Calico or
  Cilium), the kernel and container runtime for the Runtime Enforcer, and
  PostgreSQL and cert-manager for the SBOM Scanner. The links are in the
  "service dependencies" answer above.

  The project keeps up with upstream in three ways:

  - **Dependencies.** Tools like Renovate and Dependabot open update pull requests
    on every repository, so the Kubernetes client libraries and the GitHub Actions
    pins stay current.
  - **Tests.** Each end-to-end suite runs against a pinned Kubernetes version in CI.
    The Admission Controller also tests against the oldest version it supports.
    The Runtime Enforcer tests against the current version and the next one.
  - **Support policy.** The project supports the last minor version of each
    component. Security fixes are prioritized and can trigger a release on their
    own. See the [security policy](https://github.com/kubewarden/.github/blob/main/SECURITY.md#supported-versions).

- Describe how the project handles rollback procedures.

  Kubewarden doesn't include a dedicated rollback procedure and supports forward-only upgrades.
  While technically possible, reverting to a previous version of the project isn't recommended.

- How can a rollout or rollback fail? Describe any impact to already running workloads.

  Kubewarden does not support rollback procedures. See the previous answer.

  A rollout can fail for the usual reasons: an image that does not pull, a Pod
  that does not pass its readiness probe, a change in a Helm value that the new
  version rejects, or a missing prerequisite such as cert-manager. Every component
  ships as standard Kubernetes Deployments and DaemonSets, so a rollout uses the
  Kubernetes rolling update. The old version keeps running until the new version
  is ready. If the new version never becomes ready, the rollout stalls on the old
  version. Nothing is removed before its replacement works.

  A stalled rollout does not touch running workloads. What it pauses differs per
  component:

  - **Admission Controller**: the old Policy Server pods keep answering the
    webhooks. If every Policy Server replica is down, the API server rejects the
    admission requests that the policies match, because the webhooks fail closed.
    Pods that are already running are not affected.
  - **Network Enforcer**: enforcement does not depend on the controller. The CNI or
    the mesh keeps enforcing the native policies. Learn and Monitor pause.
  - **Runtime Enforcer**: the agent DaemonSet rolls with `maxSurge: 100%` and
    `maxUnavailable: 0`, so a new agent is ready before the old one stops.
    Protection does not lapse during the roll. A stalled controller blocks policy
    promotions and deletions, not enforcement.
  - **SBOM Scanner**: enforces nothing. Scanning pauses. Reports already stored
    stay readable while the storage pods are up.

- Describe any specific metrics that should inform a rollback.

  The project does not define metrics that are specific to a rollback decision.

  Every component ships as standard Kubernetes Deployments and DaemonSets, so the
  usual rollout signals apply: `kubectl rollout status`, Pod readiness, restart
  counts, and the events of the ReplicaSet or the DaemonSet. A new version that
  does not become ready stalls the rollout on the old version. Those signals are
  the same for all four components and need no extra tooling.

  Beyond that, each component exports telemetry through OpenTelemetry. The depth
  differs today. The Admission Controller and the SBOM Scanner document their
  metrics and traces in full. The Network Enforcer and the Runtime Enforcer export
  violation events and a smaller set of metrics, and the project plans to extend
  them. See the "Observability" answer in the Day 2 section for the per-component
  detail.

- Explain how upgrades and rollbacks were tested and how the upgrade-\>downgrade-\>upgrade path was tested.

  The project does not test downgrade scenarios.
  The Admission Controller end-to-end tests cover the upgrade path: the suite installs the previous release, upgrades to the release candidate, and runs the tests again.
  The Network Enforcer, Runtime Enforcer and SBOM Scanner do not yet test the upgrade path in their end-to-end suites.

- Explain how the project informs users of deprecations and removals of features and APIs.

  Deprecations and removals reach users through five channels.

  - **Release notes.** Every component drafts its GitHub release notes with `release-drafter`.
    A change marked as breaking in its commit message lands in a "Breaking changes" section at the top of the notes.
  - **Blog.** Release posts on [kubewarden.io](https://www.kubewarden.io/blog/) announce a deprecation,
    give the steps to move off the feature, and say when the default changes.
  - **CRD versions.** A deprecated API version carries `deprecated: true` and a `deprecationWarning` in the CRD,
    as Kubernetes defines them. The API server returns the warning on every request to that version,
    and `kubectl` prints it. The Admission Controller marks `policies.kubewarden.io/v1alpha2` of
    `PolicyServer` this way and points users to `v1`. The other three
    components serve `v1alpha1` only and have not deprecated a version yet.
  - **Helm charts.** A deprecated value is marked in `values.yaml` and in `values.schema.json` with
    `"deprecated": true`. When a release enables a deprecated option, `NOTES.txt` prints a warning at
    install and upgrade time.
  - **Versioning and docs.** A removal is a breaking change, so it bumps the major version, or the minor
    version for a component below 1.0. The documentation is versioned per release, so the pages for a
    deprecated feature stay with the versions that have it. The upgrade-path pages listed above describe the
    steps between versions.

- Explain how the project permits utilization of alpha and beta capabilities as part of a rollout.

  The CRD version name states the maturity of an API, as described in the
  versioning answer above. Today the Admission Controller serves `v1`, plus a
  deprecated `v1alpha2`. The Network Enforcer, the Runtime Enforcer and the SBOM
  Scanner serve `v1alpha1` only. Their APIs are alpha and can change between
  minor releases.

  An experimental feature ships behind a Helm value that is off by default. A
  user enables it for a rollout and turns it off again with a Helm upgrade.

  The documentation page of an experimental feature says so in its title and
  carries a note that a future release can change or remove the feature.

## Day 2 \- Day-to-Day Operations Phase

### Scalability/Reliability

- Describe how the project increases the size or count of existing API objects.
- Describe how the project defines Service Level Objectives (SLOs) and Service Level Indicators (SLIs).
- Describe any operations that will increase in time covered by existing SLIs/SLOs.
- Describe the increase in resource usage in any components as a result of enabling this project, to include CPU, Memory, Storage, Throughput.
- Describe which conditions enabling / using this project would result in resource exhaustion of some node resources (PIDs, sockets, inodes, etc.)
- Describe the load testing that has been performed on the project and the results.
- Describe the recommended limits of users, requests, system resources, etc. and how they were obtained.
- Describe which resilience pattern the project uses and how, including the circuit breaker pattern.

### Observability Requirements

- Describe the signals the project is using or producing, including logs, metrics, profiles and traces. Please include supported formats, recommended configurations and data storage.
- Describe how the project captures audit logging.
- Describe any dashboards the project uses or implements as well as any dashboard requirements.
- Describe how the project surfaces project resource requirements for adopters to monitor cloud and infrastructure costs, e.g. FinOps
- Which parameters is the project covering to ensure the health of the application/service and its workloads?
- How can an operator determine if the project is in use by workloads?
- How can someone using this project know that it is working for their instance?
- Describe the SLOs (Service Level Objectives) for this project.
- What are the SLIs (Service Level Indicators) an operator can use to determine the health of the service?

### Dependencies

- Describe the specific running services the project depends on in the cluster.
- Describe the project’s dependency lifecycle policy.
- How does the project incorporate and consider source composition analysis as part of its development and security hygiene? Describe how this source composition analysis (SCA) is tracked.
- Describe how the project implements changes based on source composition analysis (SCA) and the timescale.

### Troubleshooting

- How does this project recover if a key component or feature becomes unavailable? e.g Kubernetes API server, etcd, database, leader node, etc.
- Describe the known failure modes.

### Security

- Security Hygiene
  - How is the project executing access control?
- Cloud Native Threat Modeling
  - How does the project ensure its security reporting and response team is representative of its community diversity (organizational and individual)?
  - How does the project invite and rotate security reporting team members?

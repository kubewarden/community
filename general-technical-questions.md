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
- **Project Version:** 1.24.0
- **Website:** https://kubewarden.io
- **Date Updated:** 2025-05-15
- **Template Version:** v1.0
- **Description:** Kubewarden is a Kubernetes Policy Engine. It aims to be the Universal Policy Engine for Kubernetes by:

  - simplifying the adoption of 'policy-as-code'
  - distributing policies as OCI images
  - using Wasm to be architecture independent
  - allowing policy development in any WebAssembly generating languages
  - reusing policies from other policy engines without rewriting
  - verifying policies using SLSA tools and practices
  - providing a comprehensive approach to admission policy management.
    Information about Kubewarden's roadmap process is available in the [ROADMAP.md](https://github.com/kubewarden/community/blob/main/ROADMAP.md) document in the community repository.

  The maintainer ladder is at [MAINTAINERS.md](https://github.com/kubewarden/community/blob/main/MAINTAINERS.md).

- Describe the target persona or user(s) for the project?

  The documented target personas for Kubewarden are available at: https://docs.kubewarden.io/personas.

- Explain the primary use case for the project. What additional use cases are supported by the project?

  Use cases documentation is here: https://docs.kubewarden.io/#use-cases

- Explain which use cases have been identified as unsupported by the project.

  See the project's [non-goals](https://docs.kubewarden.io/use-cases#non-goals) in the documentation.

- Describe the intended types of organizations who would benefit from adopting this project. (i.e. financial services, any software manufacturer, organizations providing platform engineering services)?

  Enterprise organizations, startups, SaaS providers, regulated industries, financial services and any organization running Kubernetes at scale.

- Please describe any completed end user research and link to any reports.

  We are working on a report to be published in the future.

### Usability

- How should the target personas interact with your project?

  - CLI: [kwctl](https://github.com/kubewarden/kwctl) helps with publishing, managing and testing policies.
  - Helm: [Charts](https://github.com/kubewarden/helm-charts) are available for installing Kubewarden in Kubernetes clusters.
  - Kubernetes CRDs: `ClusterAdmissionPolicy`, `AdmissionPolicy`, `ClusterAdmissionPolicyGroup`, `AdmissionPolicyGroup` and `PolicyServer` documented at https://docs.kubewarden.io/reference/CRDs.

- Describe the user experience (UX) and user interface (UI) of the project.

  Kubewarden's user experience centers around the `kwctl` CLI and a collection of Kubernetes CRDs.
  While the project doesn't include a web UI, you can integrate with external tools offering graphical interfaces for policy management, reporting and observability.
  See the following question for more details.

- Describe how this project integrates with other projects in a production environment.

  Kubewarden integrates with the following projects in the Cloud Native ecosystem:

  #### Integrations

  | Project                                                              | Purpose                                                                                                 | Documentation                                                                             |
  | -------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
  | [OpenTelemetry](https://github.com/open-telemetry)                   | Provide unified observability.                                                                          | https://docs.kubewarden.io/howtos/telemetry/opentelemetry-qs                              |
  | [Prometheus](https://github.com/prometheus/prometheus)               | Collect and stores time-series metrics from the Policy Server.                                          | https://docs.kubewarden.io/howtos/telemetry/metrics-qs                                    |
  | [Grafana](https://github.com/grafana/grafana)                        | Visualize policy metrics through customizable dashboards.                                               | https://docs.kubewarden.io/howtos/telemetry/metrics-qs                                    |
  | [Jaeger](https://github.com/jaegertracing/jaeger)                    | Visualize fine-grained traces about policy evaluations.                                                 | https://docs.kubewarden.io/howtos/telemetry/tracing-qs                                    |
  | [Policy Reporter](https://github.com/kyverno/policy-reporter)        | Visualize policy violations for auditing purposes.                                                      | https://docs.kubewarden.io/explanations/audit-scanner/policy-reports#policy-reporter-ui   |
  | [Sigstore](https://github.com/sigstore/sigstore)                     | Signing of policies.                                                                                    | https://docs.kubewarden.io/howtos/security-hardening/secure-supply-chain#signing-policies |
  |                                                                      | Verification of OCI artifacts within policy logic.                                                      | https://docs.kubewarden.io/reference/spec/host-capabilities/signature-verifier-policies   |
  | [ArgoCD](https://github.com/argoproj/argo-cd)                        | ArgoCD integration.                                                                                     | https://docs.kubewarden.io/howtos/argocd-installation                                     |
  | [Rancher UI Extension](https://github.com/rancher/kubewarden-ui)     | Integrate Kubewarden into Rancher Manager’s UI as a global extension for policy management.             | https://docs.kubewarden.io/howtos/ui-extension/install                                    |
  | [Rancher Fleet Example](https://github.com/kubewarden/fleet-example) | Deploy and manage Kubewarden charts across fleets of clusters using GitOps workflows via Rancher Fleet. | https://docs.kubewarden.io/howtos/Rancher-Fleet                                           |

### Design

- Explain the design principles and best practices the project is following.

  #### Design principles:

  Kubewarden's design principles are at: https://docs.kubewarden.io/explanations/architecture#design-principles.

  #### Best practices

  1. **Stay Aligned with Upstream Kubernetes**

  Kubewarden’s CRDs live under `policies.kubewarden.io/v1` and adhere to Kubernetes API conventions. Policy semantics mirror official Kubernetes policies to avoid surprises when upgrading or integrating with native tooling.

  2. **Automate CI/CD Pipelines**

  All core repositories use a shared [kubewarden/github-actions](https://github.com/kubewarden/github-actions) toolkit in GitHub Actions to build Wasm modules,
  generate SBOMs, run unit and integration tests, and publish releases, ensuring consistent quality gates and reproducible artifacts across the project.

  3. **Test for Real-World Scenarios**

  Maintain dedicated end-to-end test suites [kubewarden-end-to-end-tests](https://github.com/kubewarden/kubewarden-end-to-end-tests)
  and load-testing benchmarks ([load-tests/results](https://github.com/kubewarden/community/blob/main/load-tests/results.md)) to validate policy enforcement under realistic cluster loads and edge conditions before every release.

  4. **Community-Driven Roadmap & Governance**

  Track features, issues, and milestones openly in the [Kubewarden GitHub project](https://github.com/orgs/kubewarden/projects/6). Propose and review RFCs in [kubewarden/rfc](https://github.com/kubewarden/rfc),
  and [host monthly community meetings](https://teamup.com/ks2bj74dvw132mhjtj).

  5. **Comprehensive, Versioned Documentation**

  Provide quick starts, tutorials, howtos, API references and upgrade guides all pinned to specific releases so users always view documentation matching their software version in [docs.kubewarden.io](https://docs.kubewarden.io).

  6. **Secure Software Supply Chain (SLSA Compliance)**

  Build pipelines generate [SPDX SBOMs](https://spdx.dev) and [SLSA](https://slsa.dev) provenance attestations for every Wasm module, container image, and Helm chart.
  Sigstore’s Cosign signs all artifacts and signatures are published alongside attestations—enabling fully automated, end-to-end verification of artifact integrity and origin.
  See [Verifying Kubewarden](https://docs.kubewarden.io/tutorials/verifying-kubewarden) and [the SLSA level 3 blogpost](https://www.kubewarden.io/blog/2024/11/kubewarden-1-18-release-slsa-level-3/) for more details.

- Outline or link to the project’s architecture requirements? Describe how they differ for Proof of Concept, Development, Test and Production environments, as applicable.

  The project architecture documentation is available at: https://docs.kubewarden.io/explanations/architecture
  Additionally, refer to the [actors](https://github.com/kubewarden/community/blob/main/security-self-assesment.md#actors) and [actions](https://github.com/kubewarden/community/blob/main/security-self-assesment.md#actions) sections of the [Security Self-Assessment](https://github.com/kubewarden/community/blob/main/security-self-assesment.md) document.

  For a production environment, deploy multiple replicas of the `kubewarden-controller` and `policy-server` components to ensure high availability and fault tolerance.
  Also, deploy multiple policy server instances to handle different sets of policies, allowing for better resource allocation and isolation.
  See [Configuring Kubewarden stack for production](https://docs.kubewarden.io/howtos/production-deployments) and [Configuring Policy Server for production](https://docs.kubewarden.io/howtos/policy-servers/production-deployments) for more details.

  End-to-end and load tests run against a production-like environment.
  Development and integration test environments are typically single-node clusters, where you deploy both the `kubewarden-controller` and `policy-server` components as single replicas.

- Define any specific service dependencies the project relies on in the cluster.

  The project doesn't have any specific service dependencies in the cluster.
  Optionally, the project can integrate with external services for observability, audit visualization, and policy management.

  See [Integrations](#integrations) for the list of supported integrations.
  See [Dependency Matrix](https://docs.kubewarden.io/reference/dependency-matrix) for the list of dependencies.

- Describe how the project implements Identity and Access Management.

  The project relies on Kubernetes [RBAC](https://docs.kubewarden.io/howtos/security-hardening#rbac) features to control what each component can access.
  Kubewarden policies access resources within the [cluster](https://docs.kubewarden.io/explanations/context-aware-policies), implementing access control individually for each policy server. Policy execution takes place in Policy servers.
  Therefore, different policy servers running distinct sets of policies can have varying access permissions.

  Furthermore, policies must explicitly declare the resources they intend to access; all other resources are blocked by default. Additionally, policies have read-only access to these declared resources.

  The same principle applies to the [audit scanner](https://docs.kubewarden.io/explanations/audit-scanner), which audits the running resources in the cluster.
  Cluster operators can also define the service account used by the audit scanner to perform cluster-wide scans.

- Describe how the project has addressed sovereignty.

  The project doesn't have any specific requirements for data sovereignty.
  However, you can design the policies to ensure that sensitive data isn't sent outside the cluster or to external services.
  You can configure policies to restrict access to specific namespaces or resources within the cluster.

- Describe any compliance requirements addressed by the project.

  To date, Kubewarden isn't formally certified to meet any security standards (such as PCI-DSS, COBIT, ISO, GDPR, etc.).
  However, you can use policies from the Kubewarden catalog to provide certification of other workloads in Kubernetes clusters.
  See https://github.com/kubewarden/community/blob/main/security-self-assesment.md#project-compliance for more information.

- Describe the project’s High Availability requirements.

  Kubewarden uses the High Availability (HA) capabilities of Kubernetes by deploying its core components as standard Kubernetes Deployments.
  This design provides HA through standard Kubernetes mechanisms.

  To ensure the availability of Kubewarden, users should configure the Kubewarden deployments (for components like the controller and policy servers) with multiple replicas.
  Then, even if one or more instances fail, a minimum number of replicas remain operational, preventing service disruption.
  Kubewarden also offers documentation to help users make their setup more reliable by using common Kubernetes features such as `PodDisruptionBudgets`, Affinity and Anti-Affinity rules, resource limits and requests, Priority Classes and more.

  See [Configuring Kubewarden stack for production](https://docs.kubewarden.io/howtos/production-deployments) and
  [Configuring Policy Server for production](https://docs.kubewarden.io/howtos/policy-servers/production-deployments).

- Describe the project’s resource requirements, including CPU, Network and Memory.

  Resource requirements vary depending on the number and complexity of policies deployed.
  You set `kubewarden-controller` and `audit-scanner` limits and requests using Helm chart values. Default values are here, at [this link](https://github.com/kubewarden/helm-charts/blob/b8d8f357d3ae0b677ff7c43582413f24777834e8/charts/kubewarden-controller/values.yaml#L225).
  You can set the `policy-server` component's limits and requests by following the documentation at [Production deployments](https://docs.kubewarden.io/howtos/policy-servers/production-deployments)

- Describe the project’s storage requirements, including its use of ephemeral and/or persistent storage.

  The Kubewarden project's application components are stateless. Their storage requirements are ephemeral for runtime data processing.

  On startup, each component loads all necessary configuration and sensitive information from Kubernetes ConfigMaps and Secrets, mounted as files within the pod.
  During runtime, any processed data is temporarily stored within ephemeral volumes, such as `emptyDir` volumes or directly in memory. Pod termination discards this storage.

  The project doesn't have requirements for persistent storage for its core application components.
  All data needed for operation is either provided through configuration or is transient and managed within the pod's ephemeral storage.

  The Kubewarden policy storage is in [OCI registries as OCI artifacts](https://docs.kubewarden.io/reference/oci-registries-support).

- Please outline the project’s API Design:

  - Describe the project’s API topology and conventions

    Kubewarden integrates with Kubernetes by providing a set of CRDs.
    CRDs documentation is at https://docs.kubewarden.io/reference/CRDs.

    The API follows standard Kubernetes extension patterns and is organized in groups and versions.

  - Describe the project defaults

    The default values for a Kubewarden Helm installation are available at https://github.com/kubewarden/helm-charts/blob/main/charts/kubewarden-controller/values.yaml.
    These defaults provide a secure deployment configuration.
    Kubewarden provides the [`kubewarden-defaults`](https://docs.kubewarden.io/howtos/security-hardening#kubewarden-defaults-helm-chart) chart, which deploys a default policy server and optionally includes a set of recommended policies.

    Other key defaults include:

    - **Default Policy Server**: policies resources without a specified `spec.policyServer` are automatically assigned to the default policy server.
    - **Default Policy Mode**: `protect` (enforcing mode) is the default policy mode for all policies.
    - **Default Failure Policy**: `Fail` by default (admission failures cause rejection of the API request).
    - **Background Audit**: `enabled` by default (policy audit happens in the background to check compliance of existing resources).
    - **Default Policy Server Timeout**: 10 seconds is the default timeout for policy server requests.

  - Outline any additional configurations from default to make reasonable use of the project

    Guidance for configuring Kubewarden for production use is available in the [Production deployments](https://docs.kubewarden.io/howtos/production-deployments) and [Configuring Policy Server for production](https://docs.kubewarden.io/howtos/policy-servers/production-deployments) documentation.
    Recommendations for enhancing security are in the [Security Hardening](https://docs.kubewarden.io/howtos/security-hardening) documentation.

  - Describe any new or changed API types and calls \- including to cloud providers \- that will result from this project being enabled and used

    Not applicable.

  - Describe compatibility of any new or changed APIs with API servers, including the Kubernetes API server

    The Kubewarden API server has no specific compatibility requirements.
    Features that depend on a particular Kubernetes version are automatically disabled at runtime if the cluster does not meet the required version.
    Policies that depend on a specific Kubernetes API version (e.g: [deprecated-api-versions-policy](https://github.com/kubewarden/deprecated-api-versions-policy)) declare it as such.

  - Describe versioning of any new or changed APIs, including how breaking changes are handled

    The project follows [semantic versioning](https://semver.org/) for its releases. Additional details are in the answer to the next question.
    For CRDs, the stable version in use is `v1`. In line with Kubernetes conventions, breaking changes to the API trigger a new version. Non-breaking enhancements are introduced within the existing version.
    CRDs release can be as alpha or beta versions before reaching stability.
    Alpha versions (`v1alphaX`) are experimental and may undergo significant changes or removal.
    Beta versions (`v1betaX`) are more stable, with fewer breaking changes expected, but are still subject to refinement before becoming stable.

  - Describe the project’s release processes, including major, minor, and patch releases.

    The main components of the Kubewarden project, `kubewarden-controller`, `policy-server`, `kwctl`, and `audit-scanner`, are always released together, ensuring their major and minor versions remain synchronized.
    However, the patch version for each component can be incremented independently as needed. The combination of the major and minor version is the Kubewarden "stack" version and used for the `appVersion` field in the released Helm chart.
    For each release, the team determines whether the included features and changes are a major or minor version bump and tag the components accordingly.
    The Helm chart's `version` field doesn't follow the same numbering as the `appVersion`.
    These are independent because the Helm chart version can change due to modifications in the chart itself, without corresponding changes in the Kubewarden components.
    Whenever a major or minor version bump occurs in the `appVersion`, an equivalent version bump is also performed in the Helm chart's `version` field.
    This is documented in our docs in the [upgrade path documentation](https://docs.kubewarden.io/reference/upgrade-path).
    The release process documentation is at [this location](https://github.com/kubewarden/helm-charts/blob/main/CONTRIBUTING.md).
    The [Kubewarden versioning RFC](https://github.com/kubewarden/rfc/blob/main/rfc/0007-kubewarden-versioning.md) provides a detailed overview of the versioning strategy.

    Kubewarden policies follow their own independent lifecycle.
    Their versioning progresses at a pace specific to each policy and determined on a per-policy basis, depending on changes introduced in each release.

### Installation

- Describe how the project is installed and initialized, e.g. a minimal install with a few lines of code or does it require more complex integration and configuration?

  Installation via Helm chart: https://docs.kubewarden.io/quick-start#installation
  Webinar from CNCF about Kubewarden: https://www.kubewarden.io/blog/2025/03/cncf-webinar-chatloopbackoff/

- How does an adopter test and validate the installation?

  The project provides guidance on how to validate the installation via the creation of a policy: https://docs.kubewarden.io/quick-start#example-enforce-your-first-policy.

### Security

- Please provide a link to the project’s cloud native [security self assessment](https://tag-security.cncf.io/community/assessments/).

  Security self-assessment: https://github.com/kubewarden/community/blob/main/security-self-assesment.md

- Please review the [Cloud Native Security Tenets](https://github.com/cncf/tag-security/blob/main/community/resources/security-whitepaper/secure-defaults-cloud-native-8.md) from TAG Security.

  - How are you satisfying the tenets of cloud native security projects?

    1. **Make security a design requirement**

       - **Threat-model integration**: The Kubewarden team continuously evaluates the controller and policy server against the Kubernetes SIG Security Admission Control Threat Model to make security considerations a part of every release.

         See the ([Threat Model reference documentation](https://docs.kubewarden.io/reference/threat-model)) reference documentation.

       - **WebAssembly Sandboxing**: Kubewarden executes policies inside isolated WebAssembly sandboxes.
         This architecture means that policies are confined and can't interfere with each other, or the host system, so reducing the attack surface.
       - **Context-aware policies**: Policy design should be to only access the needed resources in read-only mode, and are limited to the permissions granted to the policy server.
         This ensures that, even if a policy is compromised, it cannot access resources outside its intended scope.

    2. **Applying secure configuration has the best user experience**

       - **Helm Charts with Secure Defaults**: Kubewarden Helm charts come with secure defaults out-of-the-box, including the `kubewarden-defaults` chart. That chart automatically creates a default policy server and installs recommended security policies.
         TLS is enabled by default for all components, and the `kubewarden-controller` is configured to use a secure service account with limited permissions.
       - **Clear docs and guides**: Step-by-step Quick Start and "Security hardening" pages mean that following secure defaults takes no more time than a typical Helm install or kubectl apply.
         This includes mTLS with the Kubernetes API server, RBAC, and Security Contexts.

       See the [Security Hardening](https://docs.kubewarden.io/howtos/security-hardening) and the [Webhooks hardening](https://docs.kubewarden.io/reference/security-hardening/webhooks-hardening) documentation for more details.

    3. **Selecting insecure configuration is a conscious decision**

       Kubewarden deploys components with secure defaults.

       For policies the user can:

       - **Allow insecure sources**: Kubewarden enforces secure connections (HTTPS with trusted certificates) when pulling policy artifacts from registries.
         However, the user can choose to allow connections to registries using untrusted certificates or even without TLS by [explicitly configuring the policy server to do so](https://docs.kubewarden.io/howtos/policy-servers/custom-cas#insecure-sources).
       - **Use the monitor mode**:
         Kubewarden policies operate in two modes: `protect` and `monitor`. By default, policies deployment is in `protect` mode, where they actively enforce rules by accepting, rejecting, or mutating requests.
         The user can choose to deploy policies in `monitor` mode, where they only log the actions they would have taken without enforcing them.

    4. **Transition from insecure to secure state is possible**

       - **Hardening**: The Kubewarden project provides a [Security Hardening](https://docs.kubewarden.io/howtos/security-hardening) guide that helps users transition from a default to a more secure state.
       - **Protect mode**: Policies in `monitor` mode can change to `protect` mode at any time. However, the opposite isn't possible.
         This is a deliberate design choice to prevent users from unintentionally downgrading the security posture of their policies.
       - **Controlled policy adoption**: As custom resources, policies are applied gradually. Starting with specific namespaces via `namespaceSelector`, `matchConditions`, and `rules`, then expanding to broader scopes when ready.

    5. **Secure defaults are inherited**

       - **Kubernetes Integration**: Kubewarden integrates seamlessly with Kubernetes through admission webhooks, inheriting Kubernetes' authentication and authorization mechanisms.
       - **TLS Inheritance**: By using TLS for all communications, Kubewarden inherits the security properties of the TLS protocol.
       - **WebAssembly Security**: Policies inherit the security features of WebAssembly, including memory isolation and sandboxing, without needing to implement these protections themselves.

    6. **Exception lists have first class support**

       - **Policy exceptions**: Users can configure Kubewarden policies to permit exceptions for specific resources or namespaces using `namespaceSelector` and `matchConditions`.
         This allows users to define exceptions without compromising the overall security posture of the cluster.
       - **Audit scanner exceptions**: Users can configure the audit scanner to ignore specific resources or namespaces, allowing users to focus on the most critical areas of their cluster.
       - **Multi-tenancy**: The architecture supports deploying multiple PolicyServers, allowing different security configurations for different workloads or tenants.

    7. **Secure defaults protect against pervasive vulnerability exploits**

       - All Kubewarden workloads run inside unprivileged containers, with processes started by a low-privileged user.
       - The Pods enforce a strict security context, including read-only file systems and no additional Linux capabilities.
       - Container images are built on distroless bases to minimize the attack surface and contain only the necessary Kubewarden binaries.
       - Each component operates under a dedicated, purpose-specific Service Account, configured with minimal privileges to limit the potential impact in the event of a compromise.

    8. **Security limitations of a system are explainable**

       - **Transparent Architecture**: [The Kubewarden architecture is documented](https://docs.kubewarden.io/explanations/architecture) here, making security boundaries and assumptions explicit.
       - **Threat Model Assessment**: The project maintains a public threat model assessment, increasing transparency about security considerations.
       - **Alternative Recommendations**: When certain security controls aren't possible, Kubewarden documentation provides alternative approaches and recommendations.

- Describe how each of the cloud native principles applies to your project.

  We are waiting for the CNCF TOC to provide guidance on this topic: https://github.com/cncf/toc/issues/1673

- How do you recommend users alter security defaults in order to "loosen" the security of the project? Please link to any documentation the project has written concerning these use cases.

  Use case [Allow insecure sources](https://docs.kubewarden.io/howtos/policy-servers/custom-cas#insecure-sources)

- Security Hygiene

  - Please describe the frameworks, practices, and procedures the project uses to maintain the basic health and security of the project.

    **Dependency management**

    Kubewarden has a [Security and dependency policy](https://github.com/kubewarden/community/blob/main/SECURITY.md#supported-versions). We use automation tools such as Renovatebot and Updatecli to keep dependencies up to date in all the repositories.

    **Vulnerability scanning**

    Kubewarden's container images are scanned in ArtifactHub.
    The repositories use GitHub's security features to scan for vulnerabilities in dependencies, alongside language-specific tools like `cargo-audit` for Rust projects and `govulncheck` for Go projects.

    **SLSA 3 compliance**
    Kubewarden is SLSA3 compliant. The project generates SBOMs and provenance attestations for every Wasm module, container image, and Helm chart.

  - Describe how the project has evaluated which features will be a security risk to users if they are not maintained by the project?

    By its architectural design, Kubewarden policies being Wasm modules run in a Wasm host. This ensures policy use is safe, even at different levels of maintenance.

- Cloud Native Threat Modeling

  - Explain the least minimal privileges required by the project and reasons for additional privileges.

  RBAC roles needed by Kubewarden components are documented at [Security Hardening - RBAC](https://docs.kubewarden.io/howtos/security-hardening#rbac).

  Kubewarden is also able to run in a Namespace where the restricted Pod Security Standards are enforced.
  Please refer to the [Security Hardening - Security Contexts](https://docs.kubewarden.io/howtos/security-hardening#pod-security-standards) for more information.

- Describe how the project is handling certificate rotation and mitigates any issues with certificates.

  Kubewarden has its own certificate rotation mechanism. The CA root and the leaf certificates are both rotated automatically.
  Management is by the `kubewarden-controller` component, and documented at [Certificate Rotation](https://docs.kubewarden.io/howtos/security-hardening#certificate-rotation).

- Describe how the project is following and implementing [secure software supply chain best practices](https://project.linuxfoundation.org/hubfs/CNCF_SSCP_v1.pdf)

  Kubewarden is SLSA Level 3 compliant. The project generates SBOMs and provenance attestations for every Wasm module, container image, and Helm chart.
  All artifacts are signed with Sigstore’s Cosign and signatures are published alongside attestations. This enables fully automated, end-to-end verification of artifact integrity and origin.
  See [Verifying Kubewarden](https://docs.kubewarden.io/tutorials/verifying-kubewarden) and [the SLSA level 3 blogpost](https://www.kubewarden.io/blog/2024/11/kubewarden-1-18-release-slsa-level-3/) for more details.

  Also, Kubewarden policies can verify the signatures of OCI artifacts via the [Signature Verifier](https://docs.kubewarden.io/reference/spec/host-capabilities/signature-verifier-policies) capability.

## Day 1 \- Installation and Deployment Phase

### Project Installation and Configuration

- Describe what project installation and configuration look like.

  Management of installation and configuration uses Helm charts.

  A [quick start guide](https://docs.kubewarden.io/quick-start) is available to help users through the initial setup.

  Additional installation and configuration resources include:

  - [Helm chart documentation](https://charts.kubewarden.io/)
  - [Guidance for production deployments](https://docs.kubewarden.io/howtos/production-deployments)
  - [Instructions for configuring Policy Server in production](https://docs.kubewarden.io/howtos/policy-servers/production-deployments)
  - [Security hardening best practices](https://docs.kubewarden.io/howtos/security-hardening)
  - [Air-gapped environment installation](https://docs.kubewarden.io/howtos/airgap-installation)

### Project Enablement and Rollback

- How can this project be enabled or disabled in a live cluster? Please describe any downtime required of the control plane or nodes.

  Kubewarden removal is done by following the [Uninstall process documentation](https://docs.kubewarden.io/howtos/uninstall) instructions.
  Kubewarden removal requires no downtime, as it doesn't require any changes to the control plane or nodes.

  In critical situations, operations teams may need to carry out actions that Kubewarden would normally block.
  To support this, Kubewarden offers an [emergency disable procedure](https://docs.kubewarden.io/howtos/emergency-disable) that allows the policy engine to be temporarily turned off.

- Describe how enabling the project changes any default behavior of the cluster or running workloads.

  Kubewarden acts as an [admission controller](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/), enforcing policies on Kubernetes resources during their creation, deletion and modification.
  As a result, it can intercept and either block or mutate requests to the Kubernetes API server according to the policies defined by the user.

- Describe how the project tests enablement and disablement.

  Installing and uninstalling Kubewarden is part of the [Kubewarden end-to-end testing suite](https://github.com/kubewarden/kubewarden-end-to-end-tests/).

- How does the project clean up any resources created, including CRDs?

  See the [Uninstall process documentation](https://docs.kubewarden.io/howtos/uninstall) instructions.

### Rollout, Upgrade and Rollback Planning

- How does the project intend to provide and maintain compatibility with infrastructure and orchestration management tools like Kubernetes and with what frequency?

  Kubewarden maintains Kubernetes compatibility by following standard Kubernetes patterns.
  It uses the Kubernetes Dynamic Admission Control mechanism, stable v1 APIs, and regular dependency updates to ensure compatibility with the latest Kubernetes versions.

- Describe how the project handles rollback procedures.

  Kubewarden doesn't include a dedicated rollback procedure and supports forward-only upgrades.
  While technically possible, reverting to a previous version of the project isn't recommended.

- How can a rollout or rollback fail? Describe any impact to already running workloads.

  Kubewarden doesn't support rollback procedures.

  During rollout, potential failure scenarios include infrastructure issues, misconfigurations in the PolicyServer, software bugs, and certificate-related problems.
  The impact on running workloads is minimal. Existing validations remain functional because Kubewarden relies on Kubernetes' built-in deployment rollout mechanism. This means
  the previous version of the application stays available until the new version is fully deployed and verified.

- Describe any specific metrics that should inform a rollback.

  The project doesn't have specific metrics to inform a rollback.
  However, the project provides a useful set of [observability metrics](https://docs.kubewarden.io/howtos/telemetry/metrics-qs) for monitoring the health of the system.

- Explain how upgrades and rollbacks were tested and how the upgrade-\>downgrade-\>upgrade path was tested.

  At the time of writing, the project hasn't been tested for downgrade scenarios.
  Upgrade path testing for each release is through our [end-to-end testing suite](https://github.com/kubewarden/kubewarden-end-to-end-tests/).

- Explain how the project informs users of deprecations and removals of features and APIs.

  Kubewarden communicates deprecations and removals through semantic versioning of specific components, release notes, blog announcements, and documentation updates.
  The project follows standard Kubernetes conventions for API lifecycle management.
  Additionally, Kubewarden provides a specialized policy that can detect the usage of deprecated Kubernetes APIs, helping users identify potential compatibility issues in their configurations.

  For deprecation handling:

  - [Deprecated API Versions Policy](https://github.com/kubewarden/deprecated-api-versions-policy)
  - [Kubernetes Deprecation Guide (For Reference)](https://kubernetes.io/docs/reference/using-api/deprecation-guide/)

- Explain how the project permits utilization of alpha and beta capabilities as part of a rollout.

  Kubewarden indicates API maturity through versioning (v1alpha, v1beta, v1).
  Experimental features typically require explicit opt-in through configuration, allowing users to test new features while being aware of potential instability.

  Documentation for experimental features, including experimental policies, has appropriate warnings and limitations, enabling users to make informed decisions based on their risk tolerance.

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

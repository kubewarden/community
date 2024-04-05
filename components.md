# Kubewarden Components

Kubewarden's architecture comprises multiple components, each serving a
distinct function in the Kubewarden stack, ensuring users' compliance and
security policies are properly enforced.

#### Kubewarden CRDs (Custom Resource Definitions)

Kubewarden CRDs define resources for admission request validations. They detail
the structure, not only for the `ClusterAdmissionPolicy` and `AdmissionPolicy`
resources, which include policy configurations and matching rules for admission
requests, but also for the `PolicyServer` resource. CRDs define the setup for
PolicyServers, with deployment specific details and parameters.

The Kubewarden CRDs are defined in the
[kubewarden-controller](https://github.com/kubewarden/kubewarden-controller)
repository.

#### Kubewarden Controller

The Kubewarden Controller is the conductor. It monitors Kubewarden CRDs and
Kubernetes resources, ensuring the all resources necessary for running 
PolicyServers and policies are correctly configured. 

The code of the Kubewarden controller can be found in the
[kubewarden-controller](https://github.com/kubewarden/kubewarden-controller)
repository.

#### Policy Server

The Policy Server processes admission requests, using the logic encapsulated
within each policy to validate, mutate, or reject requests. Deployed within
Kubernetes, these servers are capable of hosting multiple policies
in parallel.

See the Policy Server code [here](https://github.com/kubewarden/policy-server)

#### Policies

At the core of Kubewarden's operational logic lies the Policies — OCI artifacts
that contain both the WebAssembly modules and necessary metadata for execution.
These policies embody the rules for admission control, packaged for
distribution and executed within Policy Servers to ensure compliance with the
defined security and operational standards.

See all the policies maintained by the Kubewarden team
[here](https://github.com/search?q=org%3Akubewarden%20topic%3Akubewarden-policy&type=repositories)

#### ValidationWebhooks and MutatingWebhooks

Kubewarden's integration with Kubernetes is orchestrated through
ValidationWebhooks and MutatingWebhooks, mechanisms that funnel admission
requests to PolicyServers. Created by the Kubewarden Controller, these
webhooks are critical for directing traffic, ensuring that each admission
request is evaluated against the relevant policy, facilitating a dynamic and
automated policy enforcement process.

#### AuditScanner

The AuditScanner introduces a proactive layer to Kubewarden’s security
framework, periodically scanning the cluster to identify and report
non-compliant resources. This component enhances cluster security by evaluating
the cluster state against enforced policies, identifying discrepancies and
facilitating timely remediation. It integrates with Policy Servers,
using existing policy definitions to ensure consistent enforcement and
evaluation.

The AuditScanner code can be found
[here](https://github.com/kubewarden/audit-scanner)

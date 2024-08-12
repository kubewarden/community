# Security Policy

## Supported Versions

The Kubewarden project provides community support only for the last minor
version. See https://docs.kubewarden.io/reference/upgrade-path for more information.

Security fixes are given priority and might be enough to cause a new version to
be released.

### Security Patch Policy

CVEs in Kubewarden code will be patched in the newest Kubewarden releases.

### Dependency Policy

Dependencies are evaluated before being introduced to ensure they:

1. are actively maintained
2. are maintained by trustworthy maintainers
3. are licensed in a way not to impact the Kubewarden license based on [the CNCF license allowlist](https://github.com/cncf/foundation/blob/main/allowed-third-party-license-policy.md).

These evaluations vary from dependency to dependencies.

Dependencies are also scheduled for removal if the project has been deprecated
or if the project is no longer maintained. Additionally based on license
changes we replace dependencies as necessary.

CVEs in dependencies will be patched for all supported versions if the CVE is
applicable and is assessed by the image scanners to be of high or critical severity.
Automation generates a new dependabot scan daily and alerts are addressed.

## Reporting a Vulnerability

_The following is a copy of the [Security
disclosure](https://docs.kubewarden.io/disclosure) page from our website. The
website's version has precedence in case of conflicts._

The Kubewarden team greatly appreciates investigative work into security
vulnerabilities carried out by well-intentioned, ethical security researchers.
We follow the practice of [responsible
disclosure](https://en.wikipedia.org/wiki/Responsible_disclosure) in order to
best protect Kubewarden's user-base from the impact of security issues. On our
side, this means:

- We will respond to security incidents on priority.
- We will release fixes for issues as soon as is practical, keeping in mind
  that not all risks are created equal.
- We will always transparently let the community know about any incident that
  affects them.

If you have found a security vulnerability in Kubewarden, the easiest way to
report a vulnerability is through the [Security tab on
GitHub](https://github.com/kubewarden/community/security/advisories). This
mechanism allows maintainers to communicate privately with you, and you do not
need to encrypt your messages.

Alternatively, you can can disclose it responsibly by emailing
[cncf-kubewarden-maintainers@lists.cncf.io](mailto:cncf-kubewarden-maintainers@lists.cncf.io)
in an **unencrypted** message. Please do not discuss potential vulnerabilities in public without validating
with us first.

You can also come talk to us at our [slack-room] in the Kubernetes Slack server.

On receipt the security team will:

- Review the report, verify the vulnerability and respond with confirmation
  and/or further information requests.
- Once the reported security bug has been addressed we will notify the
  Researcher, who is then welcome to optionally disclose publicly.

[mailing-list]: https://lists.cncf.io/g/cncf-kubewarden-maintainers
[slack-room]: https://kubernetes.slack.com/archives/C03L52JRAFM

## Securing a Kubewarden installation

If you are looking to secure your Jaeger installation, check out our documentation on the topic: [Securing Jaeger Installation](https://www.jaegertracing.io/docs/latest/security/).

# AI Contribution Policy

Kubewarden is a Kubernetes policy engine where correctness directly affects
cluster security. This policy sets expectations for AI-assisted contributions
so contributors and maintainers can collaborate effectively.

Kubewarden maintainers and contributors use AI tools in their own workflows,
and we have no objection to contributors doing the same. AI can help you
understand unfamiliar code, draft documentation, generate test cases, or
explore implementation options. We want contributors who use AI as a
productivity aid, not as a replacement for understanding.

**AI tools are welcome in the Kubewarden contributor workflow. But the human
contributor is always accountable.**

## Contribution Guidelines

The following rules apply to every contribution, regardless of how it was produced:

- **Understand your changes.** You must be able to explain every change you
  submit. "The AI generated it" is never an acceptable answer.
- **Design first.** For non-trivial changes, open an Issue before a PR. PRs
  that don't align with our architectural patterns will be closed.
- **Quality over quantity.** One thoughtful PR is worth more than many
  AI-assisted fixes for trivial issues.
- **Legal compliance.** Kubewarden follows all CNCF and Linux Foundation
  directives on AI-generated contributions. See the Linux Foundation's
  [Generative AI guidance](https://www.linuxfoundation.org/legal/generative-ai).

## Disclosure

If AI was used to generate any part of your contribution, disclose
it in the PR description and add an `Assisted-by:` trailer to the relevant
commits:

```
Assisted-by: GitHub Copilot
Assisted-by: Claude Opus 4.5
Assisted-by: ChatGPT 5.2
```

## Engaging With Maintainers

Contributing is a collaborative process. When maintainers leave feedback, follow these rules:

- **Respond personally.** Do not feed review feedback back into an AI and
  blindly apply the output. Your responses must reflect genuine understanding.
- **No AI ping-pong.** If maintainers observe a pattern of AI-driven responses
  without real engagement, the PR will be closed.
- Maintainers reserve the right to close any low-effort AI contribution without
  a detailed technical critique.

This is not an anti-AI stance. It is a stance for quality, openness, traceability, and sustainability.

## Acknowledgement

This policy was inspired by the
[CloudNativePG AI Policy](https://github.com/cloudnative-pg/governance/blob/main/AI_POLICY.md),
the [Ghostty AI Policy](https://github.com/ghostty-org/ghostty/blob/main/AI_POLICY.md),
and the [OpenTelemetry AGENTS guidelines](https://github.com/open-telemetry/opentelemetry-collector/blob/main/AGENTS.md).
It aligns with the Linux Foundation's
[Generative AI guidance](https://www.linuxfoundation.org/legal/generative-ai).

This document was written with assistance from GitHub Copilot.

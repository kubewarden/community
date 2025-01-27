# CONTRIBUTING

Thanks for your interest in contributing to Kubewarden.

There are different ways you could help us simplify the adoption of policy as code.

## Feedback

* Starring our main repository [kubewarden/kubewarden-controller](https://github.com/kubewarden/kubewarden-controller). GitHub stars do matter !
* Joining us on our [`kubewarden` channel](https://kubernetes.slack.com/?redir=%2Fmessages%2Fkubewarden).
* Following us on [Bluesky](https://bsky.app/profile/kubewarden.io) or [Mastodon](https://hachyderm.io/@kubewarden).

## Code 

Contributing to our [policy templates](https://github.com/topics/kubewarden-policy-template), [policy SDKs](https://github.com/topics/kubewarden-policy-sdk) and [policies](https://github.com/topics/kubewarden-policy).
You could also look into the following "core" projects:

| Project | Scope | Language |
|---------|---------|--------|
| [`kubewarden-controller`](https://github.com/kubewarden/kubewarden-controller) | Kubernetes integration point| Go |
| [`policy-server`](https://github.com/kubewarden/policy-server) | Run Kubewarden policies | Rust |
| [`kwctl`](https://github.com/kubewarden/kwctl) | Kubewarden policy multi-purpose cli tool | Rust |
| [`audit-scanner`](https://github.com/kubewarden/audit-scanner) | continously report policy results | Go |

### Specific CONTRIBUTING.md guides

Once you have selected a project repository to contribute, please read the CONTRIBUTING.md on that repository for specific
directions on setting a development environment, testing, or development tools needed.

### Rust code conventions

In the Kubewarden Rust code base everyone should follow some standards. This
standards are inspired on
[buck2](https://github.com/facebook/buck2/blob/main/HACKING.md#coding-conventions).
All the code should be well-tested and easy to read. Furthermore, rustfmt,
clippy and any other automatically enforced guidelines should be used as much
as possible

Beyond that, all the code changes should try to follow these guidelines:

- Follow standard `rustfmt` conventions.
- Prefer `to_owned` to convert `&str` to `String`.
- Qualify `anyhow::Result` rather than `use anyhow::Result`.
- Bin: Most errors should be returned as `anyhow::Result`. Inspecting errors
  outside tests and the top-level error handler is strongly discouraged.
- Bin/Lib: most errors should be constructed with `thiserror` deriving `enum`
  values, not raw `anyhow!`.
- Prefer `use crate::foo::bar` over `use super::bar` or `use crate::foo::*`,
  apart from test modules which often have `use super::*` at the top.
- In production-quality code, most Rustaceans choose expect rather than unwrap
  and give more context about why the operation is expected to always succeed.
  That way, if your assumptions are ever proven wrong, you have more
  information to use in debugging.

On testing code:

- Prefer the usage of `assert_eq!` macro over `assert!(a == b)` or
  `assert!(a.eq(&b))`.
- Prefer to use tests without return values over tests that return `Result<(),
  Error>`. This to avoid the boilerplate of writing `Ok(())` in the test body
  and to avoid to import `anyhow::Result` in the test module.
- Use table testing with [rstest](https://docs.rs/rstest/latest/rstest/) for
  tests with similar cases but different inputs.
- Use [mockall](https://docs.rs/mockall/latest/mockall/) for [mocking structs,
  traits and conditional
  compilation](https://github.com/oxidecomputer/omicron/blob/aceb7444938afb60f01fdf5ddeb05fd23349674d/illumos-utils/src/fstyp.rs#L33):
- Use [mockall_double](https://docs.rs/mockall_double/latest/mockall_double/#)
- Avoid writing traits only for testing purposes.

See more Some additional guidelines on [how to test
code](https://matklad.github.io/2021/05/31/how-to-test.html)

## Mission

Help us make Kubernetes cluster a more secure place by adopting policy as code.

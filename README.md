# ego

[![CI](https://github.com/thanoslabs/ego/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/thanoslabs/ego/actions/workflows/ci.yml)
[![Release](https://img.shields.io/github/v/release/thanoslabs/ego?sort=semver&display_name=tag)](https://github.com/thanoslabs/ego/releases/latest)
[![Docs site](https://img.shields.io/badge/docs-GitHub%20Pages-blue?logo=github)](https://thanoslabs.github.io/ego/)

> *"Do you know what I'm craving? A little perspective."*
> — Anton Ego, *Ratatouille*

`ego` is that perspective for your pull requests: an outside reviewer that reads the diff before it merges. It's a GitHub Action (it also runs on Forgejo and Gitea) that sends the PR to the LLM of your choice and posts one structured review comment, updated in place on every push.

The name also borrows from Freud. In his model of the mind, the *id* acts on impulse, the *superego* holds the rules, and the *ego* weighs the two against reality before anything happens. Agentic development has the same shape: coding agents generate changes on impulse, your conventions sit above them, and `ego` is the reality check before anything reaches `main`.

**📖 Documentation: https://thanoslabs.github.io/ego/**

## What you get

- **A verdict:** ✅ Looks good, ⚠️ Needs changes or 🛑 Blocking, with a risk level and a one-line reason.
- **Code and security findings**, ranked by severity, each with file, line and a concrete fix.
- **Dependency, test and open-question sections**, shown when they apply.
- **Reviewer info:** model, versions, tokens and an estimated cost.
- **Any provider:** Anthropic, OpenAI, or any OpenAI-compatible server (Ollama, vLLM, MiniMax, OpenRouter and others).
- **No checkout and no app:** `ego` reads the PR through the API and comments with the job's own token.

## Quick start

Add `.github/workflows/pr-review.yaml` to a repository and an `ANTHROPIC_API_KEY` secret:

```yaml
name: PR Review
on:
  pull_request:

permissions:
  contents: read
  pull-requests: write

jobs:
  review:
    uses: thanoslabs/ego/.github/workflows/pr-review.yaml@main
    secrets:
      llm-api-key: ${{ secrets.ANTHROPIC_API_KEY }}
```

Open a pull request, and the review appears as a comment.

## Learn more

| Page | Covers |
|---|---|
| [Getting started](https://thanoslabs.github.io/ego/getting-started) | Setup, the composite action, other providers, Forgejo |
| [The review](https://thanoslabs.github.io/ego/review) | The sections, tuning (`concise`, `extra-prompt`, `review-prompt`), gating on the verdict, cost |
| [Configuration](https://thanoslabs.github.io/ego/configuration) | Every input and output, and `extra-body` |
| [Recipes](https://thanoslabs.github.io/ego/recipes/index) | Running after other checks, Terraform, `workflow_run`, your own bot identity ([`examples/`](examples/)) |
| [Providers and forges](https://thanoslabs.github.io/ego/providers) | Anthropic, OpenAI, MiniMax, Ollama; GitHub and Forgejo |
| [Security](https://thanoslabs.github.io/ego/security) | `pull_request` vs `pull_request_target`, secrets, untrusted input |
| [Running locally](https://thanoslabs.github.io/ego/cli) | The binary as a CLI |
| [Releases and development](https://thanoslabs.github.io/ego/development) | Versioning, release labels, the codebase, building the docs |

The site is built from [`docs/`](docs/) with [nebula-md](https://github.com/thanoslabs/nebula-md).

## Contributing

See [`CONTRIBUTING.md`](CONTRIBUTING.md) and [`AGENTS.md`](AGENTS.md). Security issues: [`SECURITY.md`](SECURITY.md).

## License

[MIT](LICENSE)

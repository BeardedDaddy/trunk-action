# ⚡️ Trunk GitHub Action (alpha)

[![](https://github.com/trunk-io/trunk-action/actions/workflows/pr.yaml/badge.svg)](https://trunk.io)

This action runs [`trunk check`](https://trunk.io), a super powerful meta linter and formatter, showing inline annotations on your PRs for any issues found. Trunk runs just as well locally as on CI, so you can always quickly see lint issues _before_ pushing your changes.

## Get Started

> :warning: Trunk (the tool, along with this GitHub action) is in private alpha, and is invite-only. You can't actually use it yet 😢. Stop by the [Trunk Community Slack](https://slack.trunk.io/) if you have any questions. Thanks!

1. Install Trunk → `curl https://get.trunk.io -fsSL | bash` ([docs](https://docs.trunk.io/getting-started))
2. Setup Trunk in your repo → `trunk init` ([docs](https://docs.trunk.io/getting-started))
3. Locally check your changes for issues → `trunk check` ([docs](https://docs.trunk.io/check))
4. Locally format your changes → `trunk fmt` ([docs](https://docs.trunk.io/using-trunk/cli-commands))
5. Make sure no lint and format issues leak onto `main` → **You're in the right place 👍**

## Usage

```yaml
steps:
  - name: Checkout
    uses: actions/checkout@v2

  # Caching is only needed when using ephemeral CI runners
  - name: Cache Linters/Formatters
    uses: actions/cache@v2
    with:
      path: ~/.cache/trunk
      key: trunk-${{ runner.os }}

  # >>> Install your own deps here (npm install, etc) <<<

  - name: Trunk Check
    uses: trunk-io/trunk-action@v0.1.0-alpha
```

(See this repo's [`pr.yaml`](https://github.com/trunk-io/trunk-action/blob/main/.github/workflows/pr.yaml) workflow for further reference)

### Installing your own deps

You do need to install your own dependencies (`npm install`, etc) as a step in your workflow before the `trunk-io/trunk-action` step. Many linters will follow imports/includes in your code to find errors in your usage and thus they need you to have your dependencies installed and available.

If you've setup basic testing on CI, you're already doing this for other CI jobs; Do it here too 😉. Here's some GitHub docs to get you going: [[nodejs](https://docs.github.com/en/actions/guides/building-and-testing-nodejs), [ruby](https://docs.github.com/en/actions/guides/building-and-testing-ruby), [python](https://docs.github.com/en/actions/guides/building-and-testing-python), [many more](https://docs.github.com/en/actions/guides/about-continuous-integration)]

### Caching via `actions/cache@v2`

- Cache: If you're using **GitHub-hosted or epemeheral CI runners** cache `~/.cache/trunk` using `actions/cache@v2` as is shown above, so you don't have to re-download every linter you're using every CI run.
- Don't Cache: If you're using **long-lived self-hosted CI runners** don't bother using `actions/cache@v2`, it'll be slower than not using it.

## Linters

We integrate new linters every release. Stop by on [slack](https://slack.trunk.io/) and let us know what you'd like next!

| Language        | Linters                                                                  |
| --------------- | ------------------------------------------------------------------------ |
| All             | `gitleaks`                                                               |
| Ansible         | `ansible-lint`                                                           |
| Bash            | `shellcheck`, `shfmt`                                                    |
| Bazel, Starlark | `buildifier`                                                             |
| C/C++           | `clang-format`, `clang-tidy`                                             |
| Cloudformation  | `cfnlint`                                                                |
| Docker          | `hadolint`                                                               |
| Go              | `gofmt`, `golangci-lint`, `semgrep`                                      |
| Java            | `semgrep`                                                                |
| JS/TS           | `eslint`, `prettier`, `semgrep`                                          |
| Markdown        | `markdownlint`                                                           |
| Protobuf        | `buf`                                                                    |
| Python          | `autopep8`, `bandit`, `black-py`, `flake8`, `isort`, `pylint`, `semgrep` |
| Ruby            | `semgrep`                                                                |
| Rust            | `clippy`, `rustfmt`                                                      |
| Terraform       | `terraform-fmt`                                                          |

## Trunk versioning

After you `trunk init`, `trunk.yaml` will contain a pinned version of Trunk to use for your repo. When you run trunk, it will automatically detect which version you should be running for a particular repo and download+run it. This means that everyone working in a repo, and CI, all get the same results and the same experience. no more "doesn't happen on my machine". When you want to upgrade to a newer verison, just run `trunk upgrade` and commit the updated `trunk.yaml`.

## Run Trunk outside of GitHub Actions

Trunk has a dead simple install, is totally self-contained, doesn't require docker, and runs on macOS and all common flavors of Linux.

1. Install Trunk → `curl https://get.trunk.io -fsSL | bash` ([docs](https://docs.trunk.io/getting-started))
2. Setup Trunk in your repo → `trunk init` ([docs](https://docs.trunk.io/getting-started))
3. Check your changes for issues → `trunk check` ([docs](https://docs.trunk.io/check))
4. Format your changes → `trunk fmt` ([docs](https://docs.trunk.io/using-trunk/cli-commands))
5. Upgrade the pinned trunk version in your repo → `trunk upgrade` ([docs](https://docs.trunk.io/using-trunk/cli-commands))

Check out our [Getting Started guide](https://docs.trunk.io/getting-started) for more info.

## Badge

Add your very own [![](https://github.com/trunk-io/trunk-action/actions/workflows/pr.yaml/badge.svg)](https://trunk.io) !

Follow [these instructions](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/adding-a-workflow-status-badge) to create a workflow status badge. For example:

```
[![Trunk Check](https://github.com/trunk-io/trunk-action/actions/workflows/pr.yaml/badge.svg)](https://trunk.io)
```

## Feedback

Join the [Trunk Community Slack](https://slack.trunk.io/). ❤️

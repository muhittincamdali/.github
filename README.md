# .github

Shared community files and reusable GitHub Actions workflows for the repositories under
[muhittincamdali](https://github.com/muhittincamdali).

## Community files

GitHub uses these for every repository that does not have its own copy:

| File                                                      | Purpose                                 |
| --------------------------------------------------------- | --------------------------------------- |
| [CONTRIBUTING.md](CONTRIBUTING.md)                        | How to set up, test and submit a change |
| [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md)                  | Contributor Covenant 2.1                |
| [SECURITY.md](SECURITY.md)                                | How to report a vulnerability privately |
| [SUPPORT.md](SUPPORT.md)                                  | Where to ask questions                  |
| [Issue forms](.github/ISSUE_TEMPLATE)                     | Bug report and feature request          |
| [Pull request template](.github/PULL_REQUEST_TEMPLATE.md) | What a pull request description covers  |

## Reusable workflows

Call them from a repository workflow. Pin the reference to a commit SHA and keep the tag as a
comment; Dependabot then proposes updates.

| Workflow                                                       | What it does                                                                                                         | Permissions the caller grants                       |
| -------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- |
| [swift-ci.yml](.github/workflows/swift-ci.yml)                 | `swift build` and `swift test`; optional xcodebuild per platform (iOS, macOS, Mac Catalyst, tvOS, watchOS, visionOS) | `contents: read`                                    |
| [docc-pages.yml](.github/workflows/docc-pages.yml)             | DocC documentation to GitHub Pages, several modules merged into one site                                             | `contents: read`, `pages: write`, `id-token: write` |
| [flutter-ci.yml](.github/workflows/flutter-ci.yml)             | Format, analyze, test with coverage, optional `pub publish --dry-run`                                                | `contents: read`                                    |
| [node-ci.yml](.github/workflows/node-ci.yml)                   | npm or pnpm install from the lockfile; `lint`, `typecheck`, `test`, `build` on several Node.js versions              | `contents: read`                                    |
| [links.yml](.github/workflows/links.yml)                       | lychee link and anchor check with a one-day cache                                                                    | `contents: read`                                    |
| [readme-i18n-sync.yml](.github/workflows/readme-i18n-sync.yml) | Checks that each `README.<lang>.md` names the English version it translates and matches its code and links           | `contents: read`                                    |
| [hygiene.yml](.github/workflows/hygiene.yml)                   | Rejects tool names, unverifiable superlatives and retired slogans in files and commit messages                       | `contents: read`                                    |

A Swift package typically uses:

```yaml
name: CI

on:
  push:
    branches: [main]
  pull_request:

permissions: {}

jobs:
  swift:
    permissions:
      contents: read
    uses: muhittincamdali/.github/.github/workflows/swift-ci.yml@<sha> # v1
    with:
      platforms: '["iOS", "macOS", "tvOS", "watchOS", "visionOS"]'

  hygiene:
    permissions:
      contents: read
    uses: muhittincamdali/.github/.github/workflows/hygiene.yml@<sha> # v1
```

Every action inside these workflows is pinned to a full commit SHA, each job asks only for the
permissions it needs, and runs of the same branch are grouped so a new push cancels an outdated
pull request run. The repository checks itself with [ci.yml](.github/workflows/ci.yml)
(actionlint with shellcheck, hygiene and links).

## License

[MIT](LICENSE)

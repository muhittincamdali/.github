# Contributing

Thanks for taking the time to improve one of these projects. This guide applies to every
repository under [muhittincamdali](https://github.com/muhittincamdali) unless the repository has its
own `CONTRIBUTING.md`.

## Before you start

- **Small fixes** (typos, broken links, a failing test): open a pull request directly.
- **Larger changes** (new API, new component, behaviour change): open an issue first and describe
  the problem you want to solve. Agreeing on the approach early saves you from rewriting the work.
- **Security issues**: do not open a public issue. Follow the [security policy](SECURITY.md).

By taking part you agree to the [code of conduct](CODE_OF_CONDUCT.md).

## Set up

Fork the repository, clone your fork and create a branch from `main`:

```sh
git clone https://github.com/<you>/<repository>.git
cd <repository>
git switch -c fix/short-description
```

Then use the commands for the project's stack. CI runs the same commands, so if they pass locally
they will pass on your pull request.

| Stack                | Requirements                         | Build and test                                                                                |
| -------------------- | ------------------------------------ | --------------------------------------------------------------------------------------------- |
| Swift package        | Xcode 26 or later (CI uses macos-26) | `swift build` then `swift test`                                                               |
| Flutter              | Flutter stable                       | `flutter pub get`, `dart format .`, `flutter analyze`, `flutter test`                         |
| Node.js / TypeScript | Node.js 22 or later                  | `npm ci` then `npm test` (or the `pnpm` equivalents when the repository has `pnpm-lock.yaml`) |

For Swift packages with an example app, open the `.xcodeproj` or `Package.swift` in Xcode and run
the example scheme; every public view has an Xcode preview.

## Making the change

- Keep a pull request to one topic. Two unrelated fixes are easier to review as two pull requests.
- Add or update tests for behaviour you change. A bug fix starts with a test that fails without it.
- Document public API with doc comments (`///`); Swift packages publish them with DocC.
- Follow the formatting already in the repository (`.swift-format`, `.swiftlint.yml`,
  `analysis_options.yaml` or Prettier, whichever is present).
- Do not add dependencies without discussing it in an issue first.

### Commit messages

Use [Conventional Commits](https://www.conventionalcommits.org/en/v1.0.0/):

```text
feat(button): add a destructive style
fix(chart): keep the last label inside the frame
docs: explain the theming API
```

The type is one of `feat`, `fix`, `docs`, `test`, `refactor`, `perf`, `build`, `ci` or `chore`.

### README translations

`README.md` (English) is the source. Translations live next to it as `README.<lang>.md` and start
with a marker that names the English version they follow. If you change `README.md`, you do not
have to update the translations: CI marks them as behind, and they are updated in a follow-up.
If you do update a translation, keep code blocks and links identical to the English file.

## Pull request checklist

- [ ] CI is green (build, tests, link check, hygiene check).
- [ ] Tests cover the change.
- [ ] Public API changes are documented, and `CHANGELOG.md` has an entry under "Unreleased".
- [ ] Screenshots or a short recording for visual changes, in light and dark mode.

Reviews usually happen within a few days. If a pull request needs changes, push new commits to the
same branch; the history is squashed on merge.

## License

By contributing, you agree that your contributions are licensed under the repository's license.

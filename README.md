# Release Notes Drafter Action

Automatically generate release notes from commit history using conventional commits.

## Usage

```yaml
name: Release Notes
on:
  pull_request:
    types: [closed]

jobs:
  release-notes:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: yw13931835525-cyber/release-notes-drafter-action@v1.0.0
        with:
          base-ref: 'main'
          head-ref: ${{ github.head_ref }}
```

## Inputs

| Input | Description | Default |
|-------|-------------|---------|
| `token` | GitHub token with repo access | `GITHUB_TOKEN` |
| `base-ref` | Base branch to compare from | `main` |
| `head-ref` | Head branch to compare to | (current branch) |
| `template` | Custom template for release notes (use `{{changes}}`) | (default) |
| `include-unlabelled` | Include commits without conventional commit labels | `true` |

## Outputs

| Output | Description |
|--------|-------------|
| `release_notes` | Generated release notes in Markdown |
| `changed_features` | Number of features changed |
| `changed_fixes` | Number of bug fixes |
| `changed_docs` | Number of documentation changes |

## Conventional Commits

This action parses commits following the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Supported types:
- `feat` - Features
- `fix` - Bug Fixes
- `docs` - Documentation
- `style` - Styles
- `refactor` - Code Refactoring
- `perf` - Performance Improvements
- `test` - Tests
- `build` - Build System
- `ci` - CI/CD
- `chore` - Maintenance
- `revert` - Reverts

## License

MIT

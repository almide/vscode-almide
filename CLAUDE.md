# vscode-almide

VS Code extension for the Almide programming language (.almd). The Chrome
extension was split out to `almide-chrome-extension` — this repo is
VS Code only.

## Branch Strategy

- **main** — protected. Never commit directly. Only accepts PRs from `develop`
- **develop** — the working branch. All commits go here
- Always confirm `git branch` before committing
- Push to main triggers CI release (`.vsix` → GitHub Releases)

## Git Commit Rules

- Write commit messages in **English only**
- No prefix (feat:, fix:, etc.)
- Keep it to one concise line

## Structure

Flat repo, no subdirectory split — the repo root IS the VS Code extension:

- `package.json` - extension manifest (name, version, `contributes.grammars`)
- `syntaxes/almide.tmLanguage.json` - TextMate grammar, the single source of truth
- `language-configuration.json` - brackets, comments, auto-closing pairs
- `generator/` - Almide program that regenerates `syntaxes/almide.tmLanguage.json` from the language's own keyword/token definitions (mirrors `almide-grammar`'s output)

## VS Code Extension

```bash
npx vsce package
code --install-extension almide-lang-*.vsix
```

## CI / Release

GitHub Actions (`.github/workflows/release.yml`) runs on push to main:
1. Builds `.vsix` from the repo root
2. Creates GitHub Release with version from `package.json`

To bump version: update `version` in `package.json`.

# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **pre-commit hook repository** that wraps [rusty-commit](https://github.com/hongkongkiwi/rusty-commit), a Rust-based AI commit message generator supporting 18+ AI providers. It provides a `commit-msg` hook that automatically generates commit messages using AI based on staged changes.

## Commands

There are no local build/test commands since this is a minimal shell script wrapper. The workflow is:

```bash
# Test the hook locally before releasing
pre-commit run rusty-commit-msg --all-files

# Update the version in .pre-commit-hooks.yaml when releasing
# Then tag and push a new release
git tag v1.0.19
git push origin main --tags
```

## Architecture

This is a minimal pre-commit hook repository with only two key files:

- **`.pre-commit-hooks.yaml`** - Hook definition for the pre-commit framework. The `rev:` field must be updated to match the git tag on every release.
- **`rusty-commit-msg`** - POSIX-compatible bash script that:
  1. Receives the commit message file path as `$1`
  2. Verifies it's in a git repo with staged changes
  3. Calls `rco --print` to generate an AI commit message
  4. Writes the generated message directly to the commit message file

The hook exits gracefully (0) if no staged changes exist, allowing normal commit behavior.

## Dependencies

- **rusty-commit** CLI (`rco`) v1.0.18+ must be installed separately with the `--print` flag
- AI provider API key configured via `RCO_API_KEY` environment variable or `rco config set`

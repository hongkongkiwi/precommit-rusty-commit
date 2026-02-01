# precommit-rusty-commit

Pre-commit hook for [rusty-commit](https://github.com/hongkongkiwi/rusty-commit), a Rust-based AI commit message generator with 18+ AI providers.

## Usage

Add this to your `.pre-commit-config.yaml`:

```yaml
- repo: https://github.com/hongkongkiwi/precommit-rusty-commit
  rev: v1.0.218  # Use the latest version
  hooks:
    - id: rusty-commit-msg
```

## Requirements

- [rusty-commit](https://github.com/hongkongkiwi/rusty-commit) v1.0.218+ must be installed (with `--print` flag)
- An AI API key configured via environment variable `RCO_API_KEY` or via `rco config set`

## Setup

Set your AI provider API key before committing:

```bash
export RCO_API_KEY="your-api-key"
```

Or configure via rco:

```bash
rco config set RCO_API_KEY="your-api-key"
```

You can also set your preferred AI provider:

```bash
rco config set RCO_AI_PROVIDER=anthropic
rco config set RCO_MODEL=claude-3-5-haiku-20241022
```

## How It Works

This hook runs during the `commit-msg` stage of pre-commit. When you run `git commit`:

1. The hook generates a commit message using AI based on your staged changes
2. The generated message is written to git's commit message file
3. Git uses that message for the commit

## Supported AI Providers

rusty-commit supports 18+ AI providers including:
- OpenAI (GPT-4, GPT-4o, etc.)
- Anthropic (Claude, Claude Code)
- OpenRouter
- GitHub Copilot (OAuth)
- Groq
- DeepSeek
- Ollama (local)
- Gemini
- Azure OpenAI
- Mistral
- Perplexity
- Fireworks
- Moonshot (Kimi)
- DashScope (Qwen)
- Together AI
- DeepInfra
- xAI (Grok)
- And more

See [rusty-commit documentation](https://github.com/hongkongkiwi/rusty-commit#readme) for full configuration options.

## Alternative: Use rco's Built-in Hook

You can also use rusty-commit's built-in hook installer:

```bash
rco hook set
```

This installs a `prepare-commit-msg` hook directly in your repository.

## Resources

- [rusty-commit GitHub](https://github.com/hongkongkiwi/rusty-commit)
- [Pre-commit documentation](https://pre-commit.com/)

---
name: fastc
description: Auto-commit git changes using LLM-generated conventional commit messages
user_invocable: true
---

# fastc - Fast LLM-powered git commits

Use this skill when the user wants to quickly commit and push their current git changes using LLM-generated commit messages.

## When to use

- User says "commit this", "push this", "fastc", or similar
- User wants to commit changes without writing commit messages manually
- User wants atomic conventional commits generated from their diff

## How to invoke

Run the `fastc` command from the current working directory:

```bash
fastc
```

## Prerequisites

- `uv` must be installed
- `~/.config/fast-commit/.env` must exist with `OPENROUTER_API_KEY` and `MODEL` set
- The current directory must be a git repo with uncommitted changes

## What it does

1. Detects staged or unstaged changes
2. Sends the diff to an LLM via OpenRouter
3. Creates one or more atomic commits with conventional commit messages
4. Pushes to the remote

## Troubleshooting

- If it says "nothing to commit", there are no changes in the repo
- If the API returns 401, the OpenRouter key is invalid or has quotes around it in the config
- The config file is at `~/.config/fast-commit/.env`

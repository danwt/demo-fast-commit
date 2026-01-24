# fastc

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/downloads/)
[![uv](https://img.shields.io/badge/uv-script-blueviolet.svg)](https://docs.astral.sh/uv/)

Zero-config CLI tool that analyses your git diff with an LLM and creates atomic, conventional commits.

```
$ fastc
analysing all changes...
  feat(auth): add JWT token validation
  refactor(db): extract connection pool config
pushed
```

## How it works

1. Detects staged changes (or stages everything if nothing is staged)
2. Sends the diff to an LLM via [OpenRouter](https://openrouter.ai/)
3. The LLM groups changes into logical atomic commits with conventional commit messages
4. Creates the commits and pushes

## Install

Requires [uv](https://docs.astral.sh/uv/getting-started/installation/).

```bash
# Clone and symlink
git clone https://github.com/danwt/demo-fast-commit.git
ln -s "$(pwd)/demo-fast-commit/fc" ~/.local/bin/fastc

# Create config
mkdir -p ~/.config/fast-commit
cat > ~/.config/fast-commit/.env << 'EOF'
OPENROUTER_API_KEY=sk-or-v1-your-key-here
MODEL=google/gemini-2.0-flash-001
EOF
```

Get an API key from [openrouter.ai/keys](https://openrouter.ai/keys).

## Usage

```bash
cd your-git-repo
# Make some changes, then:
fastc
```

The tool will:
- Use staged changes if any exist
- Otherwise stage and commit all changes
- Push after committing

## Config

`~/.config/fast-commit/.env`:

| Variable | Description |
|----------|-------------|
| `OPENROUTER_API_KEY` | Your OpenRouter API key |
| `MODEL` | Any model available on OpenRouter (default: `google/gemini-2.0-flash-001`) |

## Claude Code integration

Copy [`SKILL.md`](SKILL.md) to your `.claude/skills/` directory to use `fastc` as a Claude Code skill:

```bash
mkdir -p ~/.claude/skills
cp SKILL.md ~/.claude/skills/fastc.md
```

Then invoke with `/fastc` in Claude Code.

## License

MIT

# Contributing

Thank you for considering contributing to Shiro! This project is in **Planning / Pre-alpha**. Code is not written yet — contributions now mean documentation, architecture feedback, and design input.

## Branch Rules

- **No direct pushes to `main`** — all changes via pull requests
- Branch naming: `docs/`, `feat/`, `fix/`, `chore/`, `refactor/`
- Example: `docs/add-agent-diagrams`, `feat/order-agent-proposal`

## Pull Request Process

1. Keep PRs **small and focused** — one logical change
2. Fill out the PR template (what, why, how tested)
3. **Another person must review and test** before merge
4. All CI checks must pass (lint, typecheck, tests)
5. Squash and merge — clean history

## Code Standards

- **Never commit secrets** — use `.env.local` (gitignored), reference `.env.example`
- **AI-generated code**: You must review, understand, and be able to explain every line before merging
- TypeScript: strict mode, no `any` without comment
- Python: type hints, ruff + mypy clean
- Tests required for: business logic, API routes, agent proposal builders
- Keep changes small — easier to review, easier to revert

## Commit Messages

Follow Conventional Commits:
```
feat: add order fraud detection proposal builder
fix: correct stock reservation calculation
docs: update architecture diagram
chore: update dependencies
```

## Getting Started (When Code Exists)

```bash
# Clone
git clone https://github.com/RishiSakhija/Shiro
cd Shiro

# Web app
cd apps/web
pnpm install
pnpm dev

# Agent service
cd ../services/agents
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

## Questions?

Open a GitHub Discussion or issue with the `question` label.
# {PROJECT_NAME} — Constraints & Rules

**Last updated:** {DDD DD MMM YYYY HHMM PT}

Hard rules Claude must follow in this project. Non-negotiable — not suggestions, not best practices. If something here conflicts with Claude's default behavior, this file wins.

**Structure:** Formatting Rules → Technical Constraints → Content Rules → Security Rules → Process Rules.

**Rules:**
- Each constraint must be specific enough to act on. "Write good code" is not a constraint. "All Python functions must have docstrings" is.
- Read at the start of every session. These override defaults.
- If a constraint seems wrong or outdated, flag it to Kurt — don't silently ignore it.

<!-- ARCHIMEDES HEADER END — do not edit above this line -->

---

## Formatting Rules

{Rules about output formatting, code style, naming, etc.}

- {Rule}
- {Rule}

## Technical Constraints

{Technical limits, platform requirements, compatibility rules.}

- {Rule}
- {Rule}

## Content Rules

{What to include, what to never include, tone, voice, etc.}

- {Rule}
- {Rule}

## Security Rules

{Secrets handling, .env awareness, what never gets committed.}

- Never hardcode API keys, tokens, or credentials — always use environment variables
- `.env` files are always in `.gitignore`
- {Project-specific security rules}

## Process Rules

{Workflow constraints — what to do before pushing, before deploying, etc.}

- {Rule}
- {Rule}

---

## How to Use This File

**For Claude:** Read this file at the start of every session. These rules override defaults. If a constraint seems wrong or outdated, flag it to Kurt — don't silently ignore it.

**For Kurt:** Add constraints here as they come up. Better to have too many written down than to lose one in conversation. Remove or update constraints that no longer apply.

**Convention:** Each constraint should be specific enough to act on. "Write good code" is not a constraint. "All Python functions must have docstrings" is.

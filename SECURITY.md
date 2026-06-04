# Security Policy

## Scope

`claude-workflow-template` is a **documentation-only template** — it ships no executable source code, no dependencies, and no runtime. As such, the practical attack surface is limited. The most relevant security concerns are:

- Accidental leakage of secrets (API keys, tokens, passwords) in example content or commit history
- Guidance in the template that could lead adopters into insecure practices

## Reporting a Vulnerability

If you find a security issue (e.g. a leaked credential, or template guidance that encourages an insecure pattern), please **do not open a public issue**. Instead:

1. Open a private report via [GitHub Security Advisories](https://github.com/summerhdxx-dev/claude-workflow-template/security/advisories/new), or
2. Send a direct message to [@summerhdxx-dev](https://github.com/summerhdxx-dev).

Please include a clear description and, if applicable, the file/line and how to reproduce. We aim to acknowledge reports within a few days.

## For Adopters

When you fill in this template for your own project, follow the credential-handling rules baked into `CLAUDE.md` (§9, §23) and `docs/tools.md`:

- Never commit `.env` or real credentials (the provided `.gitignore` covers `.env*`)
- Keep secrets out of commit messages, logs, and any third-party / LLM calls
- Scan your git history before going public (`git log -p | grep` for known secret prefixes)

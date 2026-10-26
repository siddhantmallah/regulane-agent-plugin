# Regulane for coding agents

A free compliance check inside the coding agent you already use. Your agent checks your code against Regulane's 34 secure-coding rules, each mapped to ISO/IEC 27001:2022 Annex A controls and, for personal data, the DPDP Act 2023, and you get back a scorecard: findings by severity, the controls they affect, and the fix for each.

**Regulane never receives your code.** Your agent reads it on your machine and reports only file paths, line numbers and one-sentence findings. No account is needed, and a free check is not stored.

More: [regulane.com/coding-agents](https://regulane.com/coding-agents)

## Use it

Ask your agent:

> Check this repository with Regulane.

The agent calls `get_compliance_rules`, reviews the code in scope, then calls `report_compliance_check` and shows you the scorecard. It can then make the fixes and check again. In Claude Code the skill is also available as `/regulane:compliance-check`.

## Install

This repository is a plugin for Claude, Codex and Cursor, and an extension for Gemini CLI. Each loads the same MCP server, `https://regulane.com/api/mcp`, and the same skill.

| Agent | Install |
|---|---|
| Claude Code | `/plugin marketplace add siddhantmallah/regulane-agent-plugin`, then `/plugin install regulane@regulane` |
| Gemini CLI | `gemini extensions install https://github.com/siddhantmallah/regulane-agent-plugin` |
| Codex, Cursor, Claude (app) | From each product's plugin directory, once listed |

Or add only the MCP server, with no plugin:

```bash
claude mcp add --transport http regulane https://regulane.com/api/mcp
codex mcp add regulane --url https://regulane.com/api/mcp
gemini mcp add --transport http regulane https://regulane.com/api/mcp
```

Setup for VS Code, Cursor, Windsurf and other agents: [regulane.com/coding-agents#setup](https://regulane.com/coding-agents#setup).

## What is in this repository

| Path | For |
|---|---|
| `skills/compliance-check/SKILL.md` | The skill every agent follows: scope, rules, report, scorecard |
| `.claude-plugin/` | Claude plugin manifest and Claude Code marketplace |
| `.codex-plugin/` | Codex plugin manifest |
| `.cursor-plugin/`, `mcp.json` | Cursor plugin manifest and MCP config |
| `.mcp.json` | MCP config for Claude and Codex |
| `gemini-extension.json`, `GEMINI.md` | Gemini CLI extension |
| `server.json` | Listing in the official MCP Registry (`com.regulane/compliance`) |

There is no code to install: only Markdown and JSON pointing at the hosted server.

## Data

What your agent sends to `regulane.com`: the repository name or address (any credentials in it are removed), branch, commit, which agent ran the check, one line describing the scope, the rule ids checked, and for each finding a file path, line number and one sentence. Anything that looks like a secret, an email address, or a card, Aadhaar or PAN number is replaced on arrival. A free check is turned into a scorecard, sent back, and not stored.

Teams can keep every check as audit evidence by connecting a Regulane workspace with an agent token; those checks are kept in the workspace. See the [privacy notice](https://regulane.com/privacy), section 4c.

## What it is not

A clean scorecard means your agent checked the code it was given against these rules and found nothing. It is not a certification, an audit opinion or a penetration test, and Regulane does not run or scan your code itself.

## Support

support@regulane.com · [regulane.com/contact](https://regulane.com/contact)

## License

MIT

# Thoropass Plugins for Claude

Claude plugins from Thoropass. They connect Claude to the Thoropass MCP server so you can work with your audits, evidence requests, requirements, controls, policies, and monitors directly from Claude.

## Available plugins

| Plugin | What it does |
|--------|--------------|
| [thoropass-compliance](plugins/thoropass-compliance) | Eight skills that explain where your audit stands, build your personal to-do list, show readiness by framework criteria, triage evidence requests, report audit status, answer questions about your policies, match policies to evidence requests, and investigate failing monitors. |

## Install

### Claude Code

```
/plugin marketplace add thoropass-public/thoropass-mcp-plugin
/plugin install thoropass-compliance@thoropass
```

### Claude Cowork

Add the marketplace from this repository, or install the plugin from the Claude plugin directory once it is listed.

## Sign in

The first time Claude uses a Thoropass tool, you'll be asked to sign in with your Thoropass account (OAuth). No API keys are needed. Claude can only see data your Thoropass account has access to.

## Try it

Understand your audit:

- "Where are we in the audit and what happens next?"
- "What do I need to do this week?"
- "How ready are we for each SOC 2 criteria?"
- "Give me this week's audit status report"

Work on evidence and policies:

- "Triage our open evidence requests"
- "What does our policy say about password rotation?"
- "Match our policies to open evidence requests"
- "Which monitors are failing and why?"

See the [plugin README](plugins/thoropass-compliance) for the full list of skills.

## Using another AI agent

Not using Claude? [AGENTS.md](AGENTS.md) explains the Thoropass MCP server to any agent (Codex, Cursor, Copilot and others): how to connect, core concepts, every available tool, the rules agents must follow, and common errors. Point your agent at it, or copy it into your own project.

## Safety

The plugin treats Thoropass content as data, not instructions. Actions that change data (submitting evidence requests, attaching policies, posting or deleting comments) always require your explicit confirmation.

## Contributing

Changes go through pull requests and require review. Bump `version` in `plugins/thoropass-compliance/.claude-plugin/plugin.json` with every release (it is the single source of truth; the marketplace entry intentionally has no version).

New skills go in `plugins/thoropass-compliance/skills/<name>/SKILL.md` and must be listed in the plugin README. See the "Editing this plugin" section of [AGENTS.md](AGENTS.md) for the skill format.

Validate locally before opening a PR (CI runs the same commands):

```
claude plugin validate --strict .
claude plugin validate --strict plugins/thoropass-compliance
claude plugin validate --strict plugins/thoropass-compliance/skills
```

## License

[MIT](LICENSE)

## Support

Questions or issues? Contact Thoropass support or open an issue in this repository.

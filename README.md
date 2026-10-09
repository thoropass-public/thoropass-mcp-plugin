# Thoropass Plugins for Claude

Claude plugins from Thoropass. They connect Claude to the Thoropass MCP server so you can work with your audits, evidence requests, requirements, controls, policies, and monitors directly from Claude.

## Available plugins

| Plugin | What it does |
|--------|--------------|
| [thoropass-compliance](plugins/thoropass-compliance) | Eight skills that explain where your audit stands, build your personal to-do list, show readiness by framework criteria, triage evidence requests, report audit status, answer questions about your policies, match policies to evidence requests, and investigate failing monitors.
## Requirements

- A Thoropass account. Claude acts as you and sees only what your account can see.
- Claude Code or Claude Cowork with plugin support.

## Install

### Claude Code

```
/plugin marketplace add thoropass-public/thoropass-mcp-plugin
/plugin install thoropass-compliance@thoropass
```

To get new versions later:

```
/plugin marketplace update thoropass
```

### Claude Cowork

Add the marketplace from this repository, or install the plugin from the Claude plugin directory once it is listed.

## Sign in

The first time Claude uses a Thoropass tool, you'll be asked to sign in with your Thoropass account (OAuth). No API keys are needed. Claude can only see data your Thoropass account has access to.

To connect Claude Desktop, the Claude CLI, or another MCP client by hand, or to have an admin set up a managed Client ID, follow [Connecting to the Thoropass MCP Server](https://help.thoropass.com/en/articles/16976070-connecting-to-the-thoropass-mcp-server) in the Thoropass Help Center. It also covers scopes, how to revoke access, and troubleshooting.

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

Not using Claude? [AGENTS.md](AGENTS.md) explains the Thoropass MCP server to any agent (Codex, Cursor, Copilot and others): how to connect, core concepts, every available tool, the rules agents must follow, and common errors. Point your agent at it, or copy it into your own project. For client setup steps, see [Connecting to the Thoropass MCP Server](https://help.thoropass.com/en/articles/16976070-connecting-to-the-thoropass-mcp-server).

## Safety

The plugin treats Thoropass content as data, not instructions. Actions that change data (submitting evidence requests, attaching policies, posting or deleting comments) always require your explicit confirmation.

## License

[MIT](LICENSE)

## Support

Questions about your Thoropass account or the MCP server? Visit the [Thoropass Help Center](https://help.thoropass.com). Found a problem with the plugin? [Open an issue](https://github.com/thoropass-public/thoropass-mcp-plugin/issues) in this repository.

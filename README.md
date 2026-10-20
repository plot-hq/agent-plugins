# Plot

Read and update your [Plot](https://plot.app) workspace from Claude, ChatGPT,
Codex, Cursor, Grok, and other AI assistants. Ask about the work assigned to
you, turn notes into tasks, build task trees with dependencies, read and write
documents, leave comments, and check your inbox without leaving the
conversation.

This plugin bundles two parts:

- The Plot MCP (Model Context Protocol) server at `https://mcp.plot.app/mcp`.
- The `managing-plot` skill, which teaches the assistant how your team works in
  Plot. It moves tasks through their statuses as it works, records blockers,
  follows the area's conventions when it plans a project, keeps plans in Plot
  documents, and links every item it mentions.

## Install

| Assistant   | Install                                                                                      |
| ----------- | -------------------------------------------------------------------------------------------- |
| Claude Code | `/plugin marketplace add plot-hq/agent-plugins`, then `/plugin install plot@plot`            |
| Codex       | `codex plugin marketplace add plot-hq/agent-plugins`, then install Plot from `/plugins`      |
| Grok Build  | `grok plugin marketplace add plot-hq/agent-plugins`, then `grok plugin install plot --trust` |

Guides for every assistant, including manual setup, are at
[plot.app/docs/ai](https://plot.app/docs/ai).

## Use it

The first time the assistant calls a Plot tool, your browser opens Plot. Sign
in, choose a workspace, review the requested permissions, and select
**Authorize**. Then ask in plain language, for example:

- "What Plot tasks are assigned to me this week?"
- "Turn these meeting notes into tasks in the ENG area."
- "Summarize the latest comments on ENG-42."

## Data

Your requests go from the assistant to `mcp.plot.app`, which calls the Plot API
on your behalf. Plot applies your normal permissions, so the assistant can only
see and change what you can. Plot tokens stay on Plot's servers and are never
sent to the assistant. A connection covers one workspace and expires after 30
days. See the [Plot privacy policy](https://plot.app/privacy).

## Support

Read the [troubleshooting guide](https://plot.app/docs/ai).

# Releasing the Plot plugin

This folder is the source of truth for the Plot plugin. The public repository
[plot-hq/agent-plugins](https://github.com/plot-hq/agent-plugins) holds a copy
of it at its root. Edit the plugin here, then publish the copy.

The MCP Worker also reads `skills/managing-plot/` at build time and serves it
through `get_instructions()`. A skill change reaches every connected assistant
when the Worker deploys, even before the plugin is published.

## Publish a release

1. Raise `version` in `plugin.json` and `.claude-plugin/plugin.json`. Clients
   skip an update when the version stays the same.
2. Validate the Claude manifests with `claude plugin validate .` from this
   folder.
3. Copy the contents of this folder to the root of `plot-hq/agent-plugins` and
   commit on top of its existing history. Do not force-push.
4. Update each directory that needs it:
   - **Claude directory:** tracks the `main` branch, so it picks up the commit
     on its own.
   - **Grok Bot and Cursor marketplace:** pins a commit. Open a pull request to
     `xai-org/plugin-marketplace` that bumps the pinned commit.
   - **OpenAI plugin directory:** server changes go live on their own. Skill or
     listing changes need a new ZIP of this folder uploaded in the portal.
   - **Muse:** connectors have no plugin package. Update the connector details
     in the Muse Connector Platform only when tools or authentication change.

Users who added the marketplace themselves, in Claude Code, Codex, or Grok
Build, receive the update when their client refreshes the marketplace.

## Automate later

If releases become frequent, add a GitHub Action in the Plot repository. It runs
on pushes to `main` that change `apps/mcp/plugin/**` and copies the folder into
`plot-hq/agent-plugins`. The default `GITHUB_TOKEN` cannot push to another
repository, so store a deploy key or a fine-grained token with write access as a
secret.

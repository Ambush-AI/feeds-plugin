# Ambush Streams plugin

Source for the **Ambush Streams** plugin in the plugin directory that ChatGPT and
Codex share. The plugin is just our remote MCP server plus listing metadata:

```text
plugin/
  plugin.json   # identity, listing, review cases, release notes
  mcp.json      # https://api.ambush.ai/mcp (streamable HTTP, OAuth)
  assets/       # icon
```

There are no bundled skills. How to use the tools (sequencing, confirmation
before deletes, routing instead of polling, stream terminology) lives in the
MCP server's `instructions`, in the main monorepo at
`ambush-feeds/api/src/mcp/instructions.ts`. Changes there ship with an API
deploy instead of a new plugin version.

## What needs a new version

| Change | Where | How it ships |
| --- | --- | --- |
| Tool names, descriptions, schemas, annotations | Monorepo `ambush-feeds/api/src/mcp` | API deploy. OpenAI rescans the server daily (or click Rescan); eligible changes go live after automated checks, new tools wait for approval. |
| Server `instructions` | Monorepo `ambush-feeds/api/src/mcp/instructions.ts` | API deploy, then Rescan. Verify the updated text shows in the portal's server details. |
| Listing copy, icons, prompts, review cases, release notes | `plugin/plugin.json`, `plugin/assets/` | Bump `version`, build the ZIP, upload it. |
| MCP server URL | `plugin/mcp.json` | Contact OpenAI; a URL change is not self-serve. |

## Build the ZIP

`plugin.json` must sit at the ZIP root:

```sh
mkdir -p dist && (cd plugin && zip -r -X ../dist/ambush-streams-0.3.0.zip . -x '*.DS_Store')
```

## Test before uploading

ChatGPT developer mode: Settings → Security and login → Developer mode, then
Plugins → **+** → `https://api.ambush.ai/mcp`. Use it from a Work chat with
`@Ambush Streams`.

Codex or the ChatGPT desktop app, from this checkout:

```sh
codex plugin marketplace add /absolute/path/to/feeds-plugin
codex plugin add ambush-streams@ambush-ai
```

Restart the app after changing files under `plugin/`.

## Release

1. Bump `version` and `publication.release_notes` in `plugin/plugin.json`.
2. Build the ZIP with the new version in its name.
3. Upload `dist/ambush-streams-<version>.zip` on the OpenAI Platform Plugins
   page, resolve findings, and submit. See [docs/submission.md](docs/submission.md).

## Other Ambush distributions

[codex-plugins](https://github.com/Ambush-AI/codex-plugins) and
[claude-plugins](https://github.com/Ambush-AI/claude-plugins) are the Git
marketplaces for the earlier skill-based package (0.2.x), and
[ambush-stream-skills](https://github.com/Ambush-AI/ambush-stream-skills) is the
skills.sh and OpenClaw package. This repository supersedes `codex-plugins` for
the directory listing.

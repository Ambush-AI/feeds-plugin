# Ambush plugin

Source for the **Ambush** plugin in the plugin directory that ChatGPT,
Codex, and dots share. A dot can use any plugin installed and enabled for the
account, so a directory listing is all dots need. The plugin is just our remote
MCP server plus listing metadata:

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

After publication OpenAI continuously reviews the live server: it fetches it
periodically and on Rescan, and ships changes that pass automated checks. See
[Remote MCP server review requirements](https://developers.openai.com/plugins/deploy/app-review#ongoing-maintenance).

| Change | Where | How it ships |
| --- | --- | --- |
| Changed tool descriptions, schemas, annotations, `_meta` | Monorepo `ambush-feeds/api/src/mcp` | API deploy. Each tool goes live once it passes automated checks; until then the previous definition stays live, so keep the server compatible with it. |
| New tools | Same | API deploy. Unavailable to users until they pass checks. |
| Removed tools | Same | API deploy. Removed as soon as a scan sees it. |
| Server `instructions` | Monorepo `ambush-feeds/api/src/mcp/instructions.ts` | API deploy. Reviewed together with the affected tools; live once the checks pass without holding tool updates or flagging the instructions. |
| Listing copy, icons, prompts, review cases, release notes | `plugin/plugin.json`, `plugin/assets/` | Bump `version`, build the ZIP, upload it. Each upload is a new version with its own review. |
| MCP server origin (`https://api.ambush.ai`) | `plugin/mcp.json` | Not changeable: a new origin means a new plugin. Only the path can change in a new version. |

Click **Rescan** in the portal after a deploy to check sooner instead of
waiting for the periodic fetch.

## Build the ZIP

`plugin.json` must sit at the ZIP root:

```sh
mkdir -p dist && (cd plugin && zip -r -X ../dist/ambush-streams-0.3.3.zip . -x '*.DS_Store')
```

## Test before uploading

Run the test set in [docs/test-set.md](docs/test-set.md), following OpenAI's
[Connect and test your plugin](https://developers.openai.com/plugins/deploy/connect-chatgpt):
the server alone in developer mode first, then the installed package, then a
dot.

To install this checkout as a local plugin in Codex or the ChatGPT desktop app:

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

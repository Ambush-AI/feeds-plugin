# Directory submission

Carried over from the 0.2.x checklist in
[codex-plugins](https://github.com/Ambush-AI/codex-plugins/tree/main/plugins/ambush-streams/submission)
and updated for the portable package. Never commit reviewer credentials,
portal verification tokens, or recording access tokens.

## Blockers

- [ ] Ambush pages live at the listing's URLs, each identifying Ambush as the
      publisher (OpenAI checks this):
      - [ ] `https://app.ambush.ai/support`
      - [ ] `https://app.ambush.ai/privacy`, approved by legal, covering what
            Ambush Streams actually collects
      - [ ] `https://app.ambush.ai/terms`, approved by legal
- [ ] Demo recording at a stable reviewer-accessible URL, added as
      `review.demo_recording_url`. Show OAuth sign-in, listing streams,
      creating one, routing every event to a connected channel, a status
      update, reviewing alerts, and the confirmation before a delete.
- [ ] MCP server `instructions` deployed to production and visible in the
      portal after a rescan.
- [ ] Reviewer account (below) seeded and preflighted.
- [ ] [Test set](test-set.md) passing on all three surfaces, with the run
      logged in `docs/test-runs/`. Section H must pass in a dot: the listing
      says dots and ChatGPT Work can act whenever a stream catches something.
- [ ] Domain verification: serve the portal's token as the only body of
      `https://api.ambush.ai/.well-known/openai-apps-challenge`, deploy, and
      verify HTTP 200 before completing it in the portal. Don't commit a
      placeholder.
- [ ] Product and legal sign-off on country availability and listing copy.

Already true: production MCP over HTTPS, OAuth with PKCE and dynamic client
registration, public protected-resource metadata, read/write/destructive tool
annotations.

## Reviewer account

- Dedicated review-only account with a verified email; sign-in needs no MFA,
  emailed code, device approval, SSO, CAPTCHA, VPN, or manual help.
- No production customer data and no internal privileges.
- Someone other than its creator completes a clean-browser sign-in using only
  the portal's credentials.
- Credentials go only in the portal's Review details form, never in the ZIP.
- Revoke or rotate after approval.

### Fixture baseline

Reset to exactly this before every review run. The review cases in
`plugin/plugin.json` depend on it.

| Fixture | State |
| --- | --- |
| `AI regulation` | Paused stream monitoring proposed AI rules broadly. |
| `AI Chip Supply` | Paused stream with exactly the five alerts below. |
| `Review Disposable` | Active stream. |
| `General Market Monitor` | Active stream. |
| `Trade Ideas` | Slack channel, install `connected`, destination `active`, not routed to `AI Chip Supply`. |

`AI Chip Supply` alerts, newest first:

1. `2026-01-05T12:00:00Z` — Review fixture — advanced packaging plant interruption
2. `2026-01-04T12:00:00Z` — Review fixture — HBM production allocation change
3. `2026-01-03T12:00:00Z` — Review fixture — accelerator export restriction enacted
4. `2026-01-02T12:00:00Z` — Review fixture — leading-edge foundry outage
5. `2026-01-01T12:00:00Z` — Review fixture — substrate supplier capacity reduction

Remove any stream created by an earlier run (positive case 2 creates
`Advanced Packaging Watch`). If the reset fails, stop rather than adapting
expectations to stale state.

## Tool annotation justifications

Paste into the portal after the production tool scan, and re-check against
the scan first.

| Tool | `readOnlyHint` | `destructiveHint` | `openWorldHint` |
| --- | --- | --- | --- |
| `list_feeds` | true: reads stream summaries | false | false: only the user's Ambush data |
| `get_feed` | true: reads one stream, its channels, usage, recent alerts | false | false |
| `list_channels` | true: reads destination metadata; webhook paths and internal metadata are redacted | false | false |
| `list_emissions` | true: reads alert history | false | false |
| `list_near_misses` | true: reads recent news the stream considered and rejected | false | false |
| `create_feed` | false: creates a stream | false: removes nothing | false |
| `update_feed` | false: changes name, prompt, status, or processing | false: reversible by another update | false |
| `route_feed_channel` | false: creates or reactivates a route | false: can be muted later | false |
| `update_feed_channel_route` | false: mutes or unmutes a route | true: muting permanently cancels pending deliveries, unmuting doesn't restore them | false |
| `delete_feed` | false: deletes a stream | true: permanent | false |

All tools act only on the authenticated user's Ambush account, so none is
open-world.

## After approval

Publish from the portal, then install from clean ChatGPT and Codex accounts,
complete OAuth, run the positive cases, confirm the negative prompts don't
invoke the plugin, and record the version and approval date in the release
notes.

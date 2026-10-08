# Directory submission

Carried over from the 0.2.x checklist in
[codex-plugins](https://github.com/Ambush-AI/codex-plugins/tree/main/plugins/ambush-streams/submission)
and updated for the portable package. Never commit reviewer credentials,
portal verification tokens, or recording access tokens.

## Blockers

- [x] Ambush pages live at the listing's URLs, each identifying Ambush as the
      publisher (OpenAI checks this):
      - [x] `https://app.ambush.ai/support` (public page verified October 6, 2026)
      - [x] `https://app.ambush.ai/privacy`, updated legal copy reported by Michael;
            public HTTP 200 and rendered policy verified October 7, 2026
      - [x] `https://app.ambush.ai/terms`, updated legal copy reported by Michael;
            public HTTP 200 and rendered terms verified October 7, 2026
- [x] Demo recording at a reviewer-accessible URL, added as
      `review.demo_recording_url`. [Ambush Streams Plugin Demo](https://supercut.ai/share/4ec6e4a5-aec9-4845-ba3b-ad9de47089bf/GZHF6mb7GlmQb7sPN7Qipv)
      opens without sign-in and plays (verified October 6, 2026). The transcript
      covers OAuth sign-in, five positive scenarios and three negative scenarios.
      Spot-checked playback shows the reviewer sign-in with the password masked
      and the stream update. Written case 3 now resumes AI regulation to match
      the recording. A dot/event delivery demonstration remains a separate
      follow-up.
- [x] MCP server `instructions` deployed to production and visible in the
      portal after a rescan. The October 6 scan flags them for further review;
      discovery does not mean approval.
- [x] Reviewer login details saved in the secure company portal. Michael
      confirmed saving the password on October 6, 2026; no password is stored
      in this repository or the ZIP.
- [ ] Reviewer account (below) preflighted with a clean-browser sign-in.
- [ ] [Test set](test-set.md) passing on all three surfaces, with the run
      logged in `docs/test-runs/`. Section H must pass in a dot: the listing
      says dots and ChatGPT Work can act whenever a stream catches something.
- [x] Domain verification: serve the portal's token as the only body of
      `https://api.ambush.ai/.well-known/openai-apps-challenge`, deploy, and
      verify HTTP 200 before completing it in the portal. Company draft
      verification passed October 6, 2026. Don't commit the token here.
- [ ] Product and legal sign-off on country availability and listing copy.

Already true: production MCP over HTTPS, OAuth with PKCE and dynamic client
registration, public protected-resource metadata, read/write/destructive tool
annotations.

## Capability labels and author — October 7, 2026

Prepared `dist/ambush-streams-0.3.3.zip` with six capability labels:

- Monitor news for topics and events you care about
- Create and refine news streams in plain language
- Review alerts and investigate missed stories
- Summarize and analyze every new alert
- Deliver alerts to destinations connected in Ambush
- Start agent workflows from news alerts in Work and dots

Set both `author.name` and `extensions.com.openai.interface.developerName`
to **Ambush**. Package validation confirms the review materials and MCP
connection are unchanged from 0.3.2. `git diff --check` passed.

Rebuilt the same pending 0.3.3 ZIP with Michael's exact product description
in `extensions.com.openai.interface.longDescription`:

> Give your agent a live feed of the world. Describe what you care about, like “any news that could impact the price of NVIDIA” or “outages at one of our cloud vendors,” and Ambush watches hundreds of thousands of sources around the clock, only alerting you when something important happens. Ambush routes events in real time to your agent in ultra low latency, triggering Dot to wake up or triggering workflows in ChatGPT Work.

The ZIP description was verified against the exact requested text and the
4,000-character submission limit. A subsequent upload attempt was also
blocked by ongoing Chrome activity.

**Uploaded:** After Michael freed Chrome, reuploaded 0.3.3 to the existing
**Ambush / Team** company draft. Verified the portal shows **0.3.3 · Draft**,
the exact requested product description, all six capability labels, developer
**Ambush**, and MCP **Configured**. The privacy accessibility warning remains.

Opened the final submission dialog at Michael's request and left its six
legal/policy attestations for the authorized developer to complete. The dialog
explicitly says the MCP findings do not block submission but may lead to
rejection. Michael then reported completion; on October 7 the portal confirmed
**Review status: In review** and **0.3.3 · In review**. Submission is complete;
publication still requires approval and is a separate step. Source changes
remain uncommitted and unpushed.

## Listing rename — October 7, 2026

Renamed the public listing from **Ambush Streams** to **Ambush** and reuploaded
`dist/ambush-streams-0.3.2.zip` to the existing draft in **Ambush / Team**.
The portal confirms **Ambush**, **0.3.2 · Draft**, MCP **Configured**, and
**Not submitted**. The internal package name and MCP key remain
`ambush-streams` to preserve the existing plugin identity and connection.

Verified that the portal retained all supported countries, five complete
positive cases, three complete negative cases, and the same Supercut video
URL. The reviewer login URL and username are still populated; the password
was not extracted or changed. The privacy accessibility warning remains.
No attestations were checked and no submission or publication was performed.
Source changes remain uncommitted.

## Legal-page follow-up — October 7, 2026

Michael reported the legal update complete. The public privacy policy and terms
both return HTTP 200, render without sign-in, show an October 7, 2026 update
date, and identify Ambush Research LLC and its affiliates. The placeholder
notices are gone. The privacy policy includes account and stream information,
destination data, usage and technical data, use and sharing, retention, rights,
and contact details. This verifies deployment and page content, not an
independent legal opinion. [Legal-page PR #6684](https://github.com/psychobot-team/reflex/pull/6684)
is merged.

The directory privacy accessibility check was retried on October 7 and still
reports "Make sure your privacy policy website is accessible." The public URL
returns HTTP 200 with no `X-Robots-Tag` header. Its initial HTML is a 783-byte
app shell with an empty root; the legal text appears after JavaScript runs.
This may explain a non-rendering checker failure, but the portal does not
identify its cause. Reviewer
credentials were saved per Michael's confirmation. A clean-browser reviewer
sign-in, the remaining functional checks, and human attestations are not yet
recorded as complete. The server-instructions warning remains on the company
draft. No submission or publication has been performed.

## Company draft dry run — October 6, 2026

Uploaded `dist/ambush-streams-0.3.1.zip` to the existing Ambush Streams draft
in Paradox / Team. The portal shows version 0.3.1, the demo URL, five complete
positive cases, three complete negative cases, and case 3 resuming the stream.
The user confirmed “All supported countries” and this targeting was saved in
the portal on October 6, 2026. Legal and listing sign-off remain outstanding.

Domain verification passed. OAuth was authorized by the user as the dedicated
reviewer account, and the MCP configuration is now configured. The automated
scan discovered server instructions and all ten tools. Remaining findings:

- Metadata: “Make sure your privacy policy website is accessible.” Retrying
  the check produced the same result. Browser access succeeds, but the cause
  of the scanner's failure has not been established. Privacy and terms still
  contain explicitly pending legal copy.
- `update_feed`: marked `destructiveHint: false`, but the scanner says its
  behavior appears to cause material loss or a hard-to-reverse change. Review
  the production annotation and behavior before rescanning.
- Server instructions: “These server instructions need further review.” The
  same instruction finding is also shown in the `update_feed` detail view;
  the portal provides no more specific explanation.
- Review information is still marked incomplete. Final reviewer details,
  country availability, and human attestations must be completed before
  submission.

No review submission or publication was performed. This was metadata and tool
discovery scanning, not execution of the eight functional test cases.

### Scan follow-up

Prepared backend changes on `codex/plugin-review-metadata` in the attached
Reflex worktree: `update_feed` now declares `destructiveHint: true` because it
overwrites selected existing settings, and its description explains the effect
on future monitoring and delivery. Server instructions now require a user
request for alert subscriptions or delivery and follow host permission and
confirmation requirements. This addresses a possible instruction-review
concern; the scanner did not explain its exact reason. These changes must be
deployed and rescanned before either finding can be marked resolved.

The focused HTTP/discovery suites passed (40 tests), API typechecking passed,
and Biome/Oxlint passed without warnings. Commit `cf41ce565` contains the four
backend/test files. The user pushed the branch after the tool's approval policy
blocked the push. [Draft PR #6643](https://github.com/psychobot-team/reflex/pull/6643)
merged on October 6, 2026 as `685ec119695a3dbebc29f851262f46127d7a3d94`.
[API validation/deployment run](https://github.com/psychobot-team/reflex/actions/runs/37541246287)
passed validation, image build, and dev deployment for that merge.
[Staging promotion](https://github.com/psychobot-team/reflex/actions/runs/37542090557)
passed for the same explicit commit. API promotion to production and the
production portal rescan remain pending; merge alone does not update the
production endpoint.

The current production deployment record is `6ccde585cd06a922885a56b8e750d21957ab47c1`.
The candidate release is 19 commits ahead and includes other merged API changes
besides this PR. [Release comparison](https://github.com/psychobot-team/reflex/compare/6ccde585cd06a922885a56b8e750d21957ab47c1...685ec119695a3dbebc29f851262f46127d7a3d94).
Production promotion needs explicit confirmation of that broader release.
Staging succeeded. GitHub's production environment has a required-reviewers
rule with `prevent_self_review: true`; another authorized reviewer must approve
a production deployment after it is queued. The user approved the broader
release and requested production queuing. [Production promotion run](https://github.com/psychobot-team/reflex/actions/runs/37542702389)
was queued with `git_sha=685ec119695a3dbebc29f851262f46127d7a3d94`.
The workflow itself runs from current main; the release image is pinned to the
staging-tested commit. Pat approved the production deployment. The production
job succeeded on 2026-10-06 at 22:52:26 UTC, deploying the pinned commit
`685ec119695a3dbebc29f851262f46127d7a3d94` (GitHub deployment
`6897087728`). The company draft was rescanned at 4:53:22 PM MDT
(22:53:22 UTC). The `update_feed` destructive-annotation finding cleared; the
new overwrite warning appears in its scanned production definition. One
server-level finding remains: "These server instructions need further review."
The portal supplies no specific reason. This finding also appears in tool
detail drawers because it applies to the server; it is not another
`update_feed` annotation error. The draft is still not submitted or published.
Reviewer login URL, username, and sign-in steps were saved and read back in the
secure portal form. The portal cleared its incomplete-information warning.
On October 6, 2026, Michael confirmed that he entered and saved the reviewer
password directly in the portal. The saved password state was not independently
verified because browser control was interrupted by user activity. No
credentials were placed in source or the ZIP. A clean-browser reviewer sign-in
remains to be preflighted. The submission confirmation explicitly says the MCP
findings do not block submission but may lead to rejection during review;
no attestations were checked and no submission was performed.

## Reviewer account

- Dedicated review-only account with a verified email; sign-in needs no MFA,
  emailed code, device approval, SSO, CAPTCHA, VPN, or manual help.
- No production customer data and no internal privileges.
- Someone other than its creator completes a clean-browser sign-in using only
  the portal's credentials.
- Credentials go only in the portal's Review details form, never in the ZIP.
- Revoke or rotate after approval.

### Account setup

Set up by hand in the Ambush app, signed in as the reviewer. Nothing is written
to the database directly. Every review case is safe to run again; before a
fresh full run, restore the initial states below. Case 3 resumes AI regulation,
so pause it again before the next recording or reviewer run.

| Stream | State |
| --- | --- |
| `AI regulation` | Paused. Any prompt about AI rules; case 3 resumes it and rewrites the prompt. |
| `AI Chip Supply` | Paused. Prompt about AI chip supply-chain disruptions. |
| `NFL Player Injuries` | Active. Forked from the NFL injuries template in Explore, which copies its last 30 days of alerts, so case 4 has real alerts immediately. |

No destinations: don't connect Slack, webhooks, or the mobile app.

Case 2 adds an `Advanced Packaging Watch` stream each time it runs. Delete
it from the app before recording the video and before submitting, so
reviewers start without one. (If one exists, asking before duplicating also
passes the case.)

## Tool annotation justifications

Use as an internal annotation reference and re-check against the production
scan. The current submission flow does not require written justifications.

| Tool | `readOnlyHint` | `destructiveHint` | `openWorldHint` |
| --- | --- | --- | --- |
| `list_feeds` | true: reads stream summaries | false | false: only the user's Ambush data |
| `get_feed` | true: reads one stream, its channels, usage, recent alerts | false | false |
| `list_channels` | true: reads destination metadata; webhook paths and internal metadata are redacted | false | false |
| `list_emissions` | true: reads alert history | false | false |
| `list_near_misses` | true: reads recent news the stream considered and rejected | false | false |
| `create_feed` | false: creates a stream | false: removes nothing | false |
| `update_feed` | false: changes name, prompt, status, or processing | true: overwrites selected existing settings; ability to undo does not make it additive | false |
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

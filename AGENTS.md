# KiteGTM plugin

The plugin that connects Claude, Claude Code, ChatGPT and Codex to a KiteGTM workspace: its skills (`skills/`), assets and
manifests. Follow the workspace `AGENTS.md` and work in a `plugin` wt task. Product wording comes from the V1 knowledge
base (workspace `AGENTS.md`, "Start here"). Tool names and descriptions must match the live connector (backend
`ops-service/app/gateway_catalog.py`). There is no build step; every manifest must stay valid JSON.

## Cloud sessions (Claude cloud, Codex Cloud, ChatGPT Work)

For any code task, before `wt land` or handing it off to land, the working agent starts a fresh reviewer in its own
tool (Claude: subagent or `/code-review`; Codex: review command or new thread), given only the diff and one-line goal.
Ask: would this break something; does it risk money, sending, sign-in or data; is it covered by a test; does it do what
the task asked? No style comments or cross-tool review. Fix real findings and record only on the task card with
`wt card --review "passed · N found, N fixed"` (or `"open: <issue>"`). No GitHub PR reviews or PR comments.

The same task flow as on the Mac, delivered as a pull request. The playbook for planning and status is the workspace
skill `.agents/skills/kite-work` (repository `kitegtm-workspace`).

1. **Find existing work first.** If an open pull request into `landed` already carries a card for the same ticket or
   task, continue on its branch instead of starting another.
2. **Branch** `<agent>/<slug>` from `landed` (agent = `claude` for Anthropic, `codex` for OpenAI including ChatGPT;
   slug = 2-6 lowercase words, e.g. `fix-reply-loop`). Never from or to `main`.
3. **Open the pull request into `landed` early** (a draft is fine), titled `[<agent>] <one-line summary>`, with this
   card in its body. One line each; leave out what you don't know:

   ```
   <!-- wt-card v1 -->
   Ticket: <owner/repo#number, ... or none>
   Place: claude-cloud | codex-cloud | chatgpt-work
   Owner: <agent> · <product> · <session link or id>
   Actual: <model> / <effort>
   State: working | waiting: <question for the owner> | blocked: <reason> | ready
   Handoff: done: ... · next: ... · verify: ...
   Verify: <how to check it works once live>
   <!-- /wt-card -->
   Change: <breaking|feature|fix|internal>
   Release-Note: <one line a customer would understand>
   ```

4. **Push after every commit** and keep the card current. Run this repository's checks where the session can.
5. **Done:** set `State: ready` and mark the pull request ready for review. The owner's Mac lands it with the full gate
   and it appears on the owner's local stack; a problem comes back as a comment on the pull request.
6. **No git checkout, or git can't reach GitHub (ChatGPT Work; Codex Cloud, whose sandbox can't fetch or push):** use
   the GitHub connector. Read files from `landed` with it (a Codex Cloud checkout may be older), create the branch from
   `landed`, commit the files with the connector, and open the pull request as above. The Mac runs the checks when it
   lands the work.

Never push to `landed` or `main` (GitHub refuses it: both require wt's gate status) and never ship: shipping is the
owner's call. Use only test keys; no production secret belongs in a cloud environment. Locally, work goes through wt
instead (workspace `AGENTS.md`, "Parallel work").

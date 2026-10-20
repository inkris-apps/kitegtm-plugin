# Changelog

This repository's changes in each Kite release, newest first. `wt ship` writes this file; do not edit it by hand.

## Kite 1.12.3 (2026-10-20)

### Fixes

- If Kite briefly can't check an AI app connection (for example during a database outage), the app's request is refused and can be retried, so a removed connection never keeps access. (conversation-hosts)

## Kite 1.3.21 (2026-10-18)

### Internal

- Require private same-tool review before landing code tasks (same-tool-review-rules)

## Kite 1.3.19 (2026-10-17)

### Fixes

- AI-app guidance correctly reports Introductions and covers finding people and preparing recommended missions. (align-plugin-introduction-guidance)

## Kite 1.3.12 (2026-10-17)

### Internal

- Cloud sessions in every repo: one section for Claude cloud, Codex Cloud and ChatGPT Work, with the task card and the GitHub-connector route; plugin gets its AGENTS.md (cloud-delivery-lane)
- Cloud sessions: Codex Cloud delivers through the GitHub connector (codex-cloud-connector)

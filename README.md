# KiteGTM for Claude, ChatGPT and Codex

KiteGTM finds the companies and decision-makers that match what you sell, works them over email and
LinkedIn, and hands you qualified opportunities. This plugin connects Claude, Claude Code, ChatGPT and
Codex to your KiteGTM workspace, so you can ask about that work and act on it where you already work.

It connects to one address, `https://api.kitegtm.com/mcp`, and signs you in through KiteGTM the first
time: you sign in the way you usually do, then press Allow. You can disconnect it at any time in
KiteGTM under Settings, AI apps.

## What it can do

- **Read:** your missions, the companies and decision-makers in each, buyer fits, conversations,
  qualified and developing opportunities, results for a date range, recent activity, and your credit
  balance. Or ask a question in plain words.
- **Act:** reply to a conversation with exactly the text you approve, pause or resume a mission's
  search, pause, resume or stop pursuing a person, mark someone as a qualified opportunity, and record
  an opportunity's outcome.
- **Not here:** buying credits, changing your plan, payment methods and your subscription stay in
  KiteGTM.

## Install

**Claude Code**

```bash
claude plugin marketplace add inkris-apps/kitegtm-plugin
claude plugin install kitegtm@kitegtm
```

Or add the server alone: `claude mcp add --transport http kitegtm https://api.kitegtm.com/mcp`, then
run `/mcp` to sign in.

**Codex**

```bash
codex plugin marketplace add inkris-apps/kitegtm-plugin
```

Then install KiteGTM from `/plugins`. Or add the server alone with
`codex mcp add kitegtm --url https://api.kitegtm.com/mcp` and `codex mcp login kitegtm`.

**Claude and ChatGPT**

Add KiteGTM from the Claude connector directory or the ChatGPT plugin directory. Until it is listed,
add a custom connector with the address above.

## Guide, privacy and support

- Guide: https://kitegtm.com/integrations/ai
- Privacy: https://kitegtm.com/privacy
- Terms: https://kitegtm.com/terms
- Support: support@kitegtm.com, https://kitegtm.com/support

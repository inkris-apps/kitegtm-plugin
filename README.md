# KiteGTM for Claude, ChatGPT and Codex

KiteGTM finds the companies and decision-makers that match what you sell, works them over email,
LinkedIn and SMS, and hands you qualified opportunities. This plugin connects Claude, Claude Code, ChatGPT and
Codex to your KiteGTM workspace, so you can ask about that work and act on it where you already work.

It connects to one address, `https://api.kitegtm.com/mcp`, and signs you in through KiteGTM the first
time: you sign in the way you usually do, then press Allow. You can disconnect it at any time in
KiteGTM under Settings, AI apps.

## What it can do

- **Read:** your missions, the companies and decision-makers in each, buyer fits, email, LinkedIn and
  SMS conversations, qualified and developing opportunities, results for a date range, recent
  activity, your credit balance, your email, LinkedIn and SMS campaigns and the people in them, your
  contacts and your contact imports. Or ask a question in plain words.
- **Draft replies:** a reply is saved as a draft on the conversation, with exactly the text given.
  Nothing is sent from here: you review it and press Send in KiteGTM.
- **Act:** pause or resume a mission's search; pause, resume or stop pursuing a person; mark someone
  as a qualified opportunity and record an opportunity's outcome; import a CSV or Excel file of
  contacts; add existing contacts to a campaign or remove them; pause a campaign. Adding people to a
  running campaign means it contacts the eligible ones on its current schedule.
- **Not here:** buying credits, changing your plan, payment methods and your subscription stay in
  KiteGTM. So do creating, editing, starting and deleting campaigns.

## Where prospects come from, and opt-outs

- Prospects come from KiteGTM's own business-contact data, or from contacts you bring yourself
  (a CSV or Excel import, or your CRM).
- Every cold email carries a one-click unsubscribe. A reply asking to stop, on email, LinkedIn or SMS,
  puts the person on your workspace's do-not-contact list on every channel; a request KiteGTM is
  unsure about is held for you to decide. The first text message says "Reply STOP to opt out".
- You can add people to your do-not-contact list yourself. Every send, on every channel, checks it.

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

# KiteGTM for Claude, ChatGPT and Codex

Kite is an introductions platform. Tell Kite what you want to achieve. Kite identifies the right people and gets you introduced.

**Who it helps:** Businesses that want to meet the right people to achieve a business goal.

This plugin connects Claude, Claude Code, ChatGPT and Codex to your KiteGTM workspace, so you can ask about
that work and act on it where you already work.

It connects to one address, `https://api.kitegtm.com/mcp`, and signs you in through KiteGTM the first
time: you sign in the way you usually do, then press Allow. You can disconnect it at any time in
KiteGTM under Settings, AI apps.

## What the words mean

- A **mission** is how Kite pursues your objective: who to reach, what an Introduction must show, and
  the work in between.
- A **buyer fit** is a person Kite pursues. It is a verified match, not a sign of interest.
- An **Introduction** is a person who wants to talk and meets every condition you require, on recorded
  evidence. You get the person, their company, the context, the conversation, how they qualified and
  the next step. A meeting is optional. A reply, a referral or a booking alone is not an Introduction.
- The connector's tools call these records **opportunities**. Each one says whether it is an
  Introduction now, or is still developing, awaiting qualification or short of a condition.
- **Monthly Reach** is the number of unique people Kite can source into your missions each month. Sends,
  follow-ups and replies do not use it, and unused Reach does not carry over. Every Introduction is
  included, with no separate fee or cap; a particular number is not guaranteed.

## What it can do

- **Read:** your missions, the companies and decision-makers in each, buyer fits, email, LinkedIn and
  SMS conversations, opportunities and whether each is an Introduction, results for a date range
  (including Introductions), recent activity, your credit balance, your email, LinkedIn and SMS
  campaigns and the people in them, your contacts and your contact imports. Or ask a question in
  plain words.
- **Draft replies:** a reply is saved as a draft on the conversation, with exactly the text given.
  Nothing is sent from here: you review it and press Send in KiteGTM.
- **Act:** pause or resume a mission's search; pause, resume or stop pursuing a person; mark someone
  as a qualified opportunity on your own judgement (this alone does not make them an Introduction) and
  record an opportunity's outcome; import a CSV or Excel file into your contact book, which sends no
  messages; preview adding contacts to a campaign; remove contacts from a campaign; pause a campaign.
- **Campaign enrollment stays with you:** an AI app cannot enroll people into a campaign. It returns a
  request to review the list and complete enrollment in the signed-in KiteGTM app, where consent,
  suppression and duplicate checks apply.
- **Not here:** buying credits, changing your plan or Monthly Reach, payment methods and your
  subscription stay in KiteGTM. So do creating, editing, starting, resuming and deleting campaigns,
  and enrolling people into them.

## Where people come from, and opt-outs

- People come from KiteGTM's business-contact data, whose details are compiled from public
  professional and business sources and business-contact sourcing and verification services, or from
  contacts you bring yourself (a CSV or Excel import, or your CRM). The
  [privacy policy](https://kitegtm.com/privacy#business-contact-data) sets out the legal basis for
  holding and sharing that data. Kite works through the email, LinkedIn and SMS you connect.
- Anyone can be removed from KiteGTM's data by emailing privacy@kitegtm.com. Our team handles the
  request manually, removes active sourced-contact copies, and keeps a minimal suppression record to
  prevent future sourcing and outreach across KiteGTM workspaces. This is separate from one
  customer's do-not-contact list.
- Every cold email carries a one-click unsubscribe. A reply asking to stop, on email, LinkedIn or SMS,
  puts the person on your workspace's do-not-contact list for the channels KiteGTM can link to that
  identity; a request KiteGTM is unsure about is held for you to decide.
- Customer SMS campaigns require recorded consent. The first text says "Reply STOP to opt out", and
  STOP suppresses outreach through the channels linked to that identity.
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

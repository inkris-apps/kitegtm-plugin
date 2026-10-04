---
name: kitegtm
description: Work with a KiteGTM workspace through the KiteGTM connector. Use when the user asks about their Kite missions, buyer fits, replies and conversations, opportunities and Introductions, results or credits, campaigns, contacts and imports, or wants to draft a reply, pause or resume a mission or campaign, stop pursuing a person, import contacts, add people to a campaign, or record an opportunity's outcome.
---

# KiteGTM

Kite is an introductions platform. Tell Kite what you want to achieve. Kite identifies the right
people and gets you introduced.

## The words mean specific things

- An **objective** is what the business wants to achieve. A **mission** is how Kite pursues it: the
  people to reach, what an Introduction must show, and the work. Its id is `market_id`.
- A **buyer fit** is a person Kite pursues. It is a verified match, not a sign of interest.
- An **Introduction** is a person who wants to talk and meets every condition the customer requires,
  on recorded evidence. It comes with the person, company, context, conversation, qualification and
  next step. A meeting is optional.
- The tools call these records **opportunities**. Each `list_opportunities` row says whether it is an
  Introduction now (`introduction.state`). Developing interest, a qualified stage with a condition still
  unknown, a reply, a referral or a booking alone is not an Introduction: never report one as an
  Introduction. `mark_opportunity` and `record_opportunity_outcome` do not make anyone an Introduction.
- **Monthly Reach** is the number of unique people Kite can source into missions each billing period.
  It is not sends or people contacted, and unused Reach does not carry over. Introductions have no fee,
  cap or guaranteed number.
- A figure a tool did not return is unknown, not zero.

## Answering questions

- For a general question, `ask_about_workspace` answers from live data.
- For specific records, use the list and get tools. Their ids feed each other:
  `list_missions` gives `market_id`, `list_mission_companies` gives `record_id`,
  `list_conversations` and `list_opportunities` give `conv_key`.
- A daily check: `get_recent_activity`, then `list_conversations` with `tab: "needs_you"`, then
  `list_opportunities` with `introduction: "introduction"` for new Introductions.
- `get_results` counts Introductions separately from qualified and developing opportunities. Its people
  contacted counts sends, not Monthly Reach.

## Acting

Every action works as the signed-in person.

- **Replying.** Read the thread with `get_conversation` first, then write the reply.
  `reply_to_conversation` saves it as a draft and sends nothing: tell the person it is waiting for
  them in KiteGTM, with the `review_url` it returns, where they review it and press Send.
- **Stopping someone** (`stop_person`) ends their pursuit on every channel. Confirm the person and
  the reason first. `pause_person` is the reversible choice.
- **Missions.** `pause_mission` stops the search for new companies; `resume_mission` starts it again.
- **Outcomes.** `mark_opportunity` records the user's own judgement that someone qualifies;
  `record_opportunity_outcome` records accepted, won, lost or withdrawn. Neither is evidence of an
  Introduction.
- **Campaigns and contacts.** The campaign list and get tools give `campaign_id`; `list_contacts` gives
  the contact keys. Adding people to a running campaign (`add_contacts_to_campaign`, or
  `start_contact_import` with a campaign destination) means it contacts the eligible ones on its
  schedule: show the person the campaign and the selection, use `dry_run` first, and get their
  go-ahead. A queued import or add has only started; check `get_contact_import` or `get_contact_job`
  before saying it finished. `remove_contacts_from_campaign` is reversible and is not do-not-contact.

## Not available here

Buying credits, changing a plan or Monthly Reach, payment methods and subscriptions stay in the
KiteGTM app, under Settings. `get_credit_balance` can show the balance. Creating, editing, starting and
deleting campaigns also stay in the app.

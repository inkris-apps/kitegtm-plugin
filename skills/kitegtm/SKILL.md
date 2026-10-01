---
name: kitegtm
description: Work with a KiteGTM workspace through the KiteGTM connector. Use when the user asks about their outbound pipeline in KiteGTM, such as missions, buyer fits, replies and conversations, qualified opportunities, results or credits, campaigns, contacts and imports, or wants to draft a reply, pause or resume a mission or campaign, stop pursuing a person, import contacts, add people to a campaign, or record an opportunity's outcome.
---

# KiteGTM

KiteGTM finds the companies and decision-makers that match what a business sells, works them over
email, LinkedIn and SMS, and hands over qualified opportunities.

## The words mean specific things

- A **mission** sets the objective: the market, the decision-makers and what a qualified opportunity
  looks like. Its id is `market_id`.
- A **buyer fit** is a decision-maker KiteGTM pursues. It is a verified match to the target, not a
  sign of buying interest.
- An **opportunity** is a qualified outcome: an appropriate decision-maker confirmed interest and met
  the customer's conditions. **Developing** interest is still being confirmed and is not an
  opportunity. Never report developing interest, a reply or a meeting as an opportunity on its own.

## Answering questions

- For a general question, `ask_about_workspace` answers from live data.
- For specific records, use the list and get tools. Their ids feed each other:
  `list_missions` gives `market_id`, `list_mission_companies` gives `record_id`,
  `list_conversations` and `list_opportunities` give `conv_key`.
- A daily check: `get_recent_activity`, then `list_conversations` with `tab: "needs_you"`, then
  `list_opportunities` with `stage: "qualified"`.

## Acting

Every action works as the signed-in person.

- **Replying.** Read the thread with `get_conversation` first, then write the reply.
  `reply_to_conversation` saves it as a draft and sends nothing: tell the person it is waiting for
  them in KiteGTM, with the `review_url` it returns, where they review it and press Send.
- **Stopping someone** (`stop_person`) ends their pursuit on every channel. Confirm the person and
  the reason first. `pause_person` is the reversible choice.
- **Missions.** `pause_mission` stops the search for new companies; `resume_mission` starts it again.
- **Outcomes.** `mark_opportunity` records the user's own judgement that someone qualifies;
  `record_opportunity_outcome` records accepted, won, lost or withdrawn.
- **Campaigns and contacts.** The campaign list and get tools give `campaign_id`; `list_contacts` gives
  the contact keys. Adding people to a running campaign (`add_contacts_to_campaign`, or
  `start_contact_import` with a campaign destination) means it contacts the eligible ones on its
  schedule: show the person the campaign and the selection, use `dry_run` first, and get their
  go-ahead. A queued import or add has only started; check `get_contact_import` or `get_contact_job`
  before saying it finished. `remove_contacts_from_campaign` is reversible and is not do-not-contact.

## Not available here

Buying credits, changing a plan, payment methods and subscriptions stay in the KiteGTM app, under
Settings. `get_credit_balance` can show the balance. Creating, editing, starting and deleting
campaigns also stay in the app.

---
name: kitegtm
description: Work with a KiteGTM workspace through the KiteGTM connector. Use when the user asks about their outbound pipeline in KiteGTM, such as missions, buyer fits, replies and conversations, qualified opportunities, results or credits, or wants to reply to someone, pause or resume a mission, stop pursuing a person, or record an opportunity's outcome.
---

# KiteGTM

KiteGTM finds the companies and decision-makers that match what a business sells, works them over
email and LinkedIn, and hands over qualified opportunities.

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

- **Replying.** Read the thread with `get_conversation` first. Write the reply, show the person the
  exact text, and call `reply_to_conversation` only after they approve it. A sent message cannot be
  recalled.
- **Stopping someone** (`stop_person`) ends their pursuit on every channel. Confirm the person and
  the reason first. `pause_person` is the reversible choice.
- **Missions.** `pause_mission` stops the search for new companies; `resume_mission` starts it again.
- **Outcomes.** `mark_opportunity` records the user's own judgement that someone qualifies;
  `record_opportunity_outcome` records accepted, won, lost or withdrawn.

## Not available here

Buying credits, changing a plan, payment methods and subscriptions stay in the KiteGTM app, under
Settings. `get_credit_balance` can show the balance.

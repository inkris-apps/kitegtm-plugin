---
name: kitegtm
description: Work with a KiteGTM workspace through the KiteGTM connector. Use when the user asks about their Kite missions, mission recommendations or what to pursue next, buyer fits, replies and conversations, opportunities and Introductions, results or credits, campaigns, contacts and imports, or wants to find a person by name, email or company, review or prepare a recommended mission, draft a reply, pause or resume a mission, pause a campaign, stop pursuing a person, import contacts, preview campaign additions, or record an opportunity's outcome.
---

# KiteGTM

Kite is an introductions platform. It gets you into phone or video meetings with qualified people
who have a reason to do business with you.

## The words mean specific things

- An **objective** is what the business wants to achieve. A **mission** is how Kite pursues it: the
  people to reach, what an Introduction must show, and the work. Its id is `market_id`.
- A **buyer fit** is a person Kite pursues. It is a verified match, not a sign of interest.
- An **Introduction** is a person who has agreed to talk and whom nothing on record rules out.
  A required condition not yet confirmed travels with the Introduction as `introduction.to_confirm`
  for the call; one on record as not met rules the person out. Never describe an unknown condition
  as satisfied. The handoff includes the person, company, context, conversation, qualification and
  next step. A meeting is optional.
- The tools call these records **opportunities**. Each `list_opportunities` row says whether it is an
  Introduction now (`introduction.state`). Report a row as an Introduction when that state is
  `introduction`, including any `to_confirm` items. Do not infer it from the opportunity stage or
  silently promote other states. Developing interest, a reply, a referral or a booking alone is not
  an Introduction. `mark_opportunity` and `record_opportunity_outcome` do not establish it by themselves.
- The **First Win Guarantee** keeps its stricter qualified-introduction standard: every required
  criterion must be met. An Introduction with conditions still to confirm does not establish that
  guarantee's qualified delivery.
- A **mission recommendation** is a strategy to pursue, not confirmed demand, interest or an Introduction.
- **Monthly Reach** is the number of unique people Kite can source into missions each billing period.
  It is not sends or people contacted, and unused Reach does not carry over. Introductions have no fee,
  cap or guaranteed number.
- A figure a tool did not return is unknown, not zero.

## Answering questions

- Use the current connection's tool names and parameter schemas. If a documented tool, parameter or
  result field is absent, report that limit instead of guessing. Missing Introduction state does not
  establish either an Introduction or a zero count; an opportunity stage is not a substitute.
- For a general question, `ask_about_workspace` answers from live data.
- For specific records, use the list and get tools. Their ids feed each other:
  `list_missions` gives `market_id`, `list_mission_companies` gives `record_id`,
  `list_conversations` and `list_opportunities` give `conv_key`.
- To find someone, use `find_person` with their name, email or company. It searches people already in
  the workspace and returns their channels, campaigns and last conversation. Resolve ambiguous matches
  before acting; do not invent a `market_id`, `record_id` or `conv_key`.
- A daily check: `get_recent_activity`, then `list_conversations` with `tab: "needs_you"`, then
  `list_opportunities` with `introduction: "introduction"` when that filter is exposed. Otherwise inspect
  the returned `introduction.state` values. State the date window and page limits the response actually covers.
- `get_results` counts Introductions separately from qualified and developing opportunities. Its people
  contacted figure counts unique people first sent outreach in the dates, not messages or Monthly Reach.

## Mission recommendations

- Use `list_mission_recommendations` to see what Kite suggests and obtain each `recommendation_id`.
  Use `get_mission_recommendation` to review the objective, audience, location, roles and conditions.
- Use `refresh_mission_recommendations` when the user wants new suggestions. Existing open suggestions
  are kept by default; `replace: true` asks for alternatives. Refreshing starts nothing. If it returns
  `no_others`, explain that the existing suggestions remain.
- Use `prepare_mission_recommendation` for the chosen recommendation. It sets up a mission and returns
  `review_url`; it starts nothing and contacts nobody. Give the user that link to review and press Start
  in KiteGTM. Repeating preparation returns the same setup, not another mission. If the response says
  `started: true` or `code: "started"`, report that it was already started; preparation did not start it again.
- Use `dismiss_mission_recommendation` when the user rejects that direction. Dismissal stops Kite showing
  or recommending that audience again; a recommendation that already started a mission is refused.
- Use only tools exposed by the current connector. If these tools are unavailable, explain the limit
  and direct the user to review recommendations in KiteGTM; do not claim a refresh or preparation happened.

## Acting

Every action works as the signed-in person.

- If the connected tool advertises sending a reply or enrolling campaign contacts directly, do not
  invoke it as a draft or preview. Prepare the content here and direct the user to review it in KiteGTM.
  The draft and review workflows below require the matching tool contract on the current connection.
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
  the contact keys. `start_contact_import` imports a staged file into the contact book, which sends
  nothing. `add_contacts_to_campaign` with `dry_run: true` previews who is eligible. An AI app cannot
  enroll people into a campaign: a campaign import or an actual add returns `needs_person` with a
  review link, and nothing is queued. Tell the person to review the list and complete enrollment in
  KiteGTM, with that link. A queued import or removal has only started; check `get_contact_import` or
  `get_contact_job` before saying it finished. `remove_contacts_from_campaign` is reversible and is not
  do-not-contact.

## Not available here

Buying credits, changing a plan or Monthly Reach, payment methods and subscriptions stay in the
KiteGTM app, under Settings. `get_credit_balance` can show the balance. Creating, editing, starting,
resuming and deleting campaigns, and enrolling people into them, also stay in the app.

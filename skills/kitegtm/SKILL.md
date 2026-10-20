---
name: kitegtm
description: Work with a KiteGTM workspace through the KiteGTM connector. Use when the user asks about their Kite missions, mission recommendations or what to pursue next, buyer fits, replies and conversations, opportunities and Introductions, results or credits, campaigns, contacts and imports, or wants to find a person by name, email or company, review or prepare a recommended mission, draft a reply, pause or resume a mission, pause a campaign, stop pursuing a person, import contacts, preview campaign additions, record an opportunity's outcome, or, with versioned permissions (available when your workspace has it turned on), prepare an action for them to confirm in KiteGTM or hand Kite a longer task.
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

Every action works as the signed-in person, within what the connection is allowed to do.

- Use each tool for what its own description says it does. `reply_to_conversation` only saves a draft
  and `add_contacts_to_campaign` only previews or hands enrollment to the person; never present either
  as a send or an enrollment. Do not invoke any other tool that would send a reply or enroll contacts
  directly unless it is one of the `propose_` tools described under **Versioned permissions** below.
  Otherwise prepare the content here and direct the user to review it in KiteGTM. The draft and review
  workflows below require the matching tool contract on the current connection.
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

## Versioned permissions

Versioned permissions: available when your workspace has it turned on. Check the tools the current
connection lists: a connection without `get_connection` uses the original permissions, and everything
above applies unchanged.

- **What this connection may do.** `get_connection` names the workspace the connection is bound to, the
  permissions the person gave it when connecting, and whether they are turned on now. Work only in that
  workspace. A tool outside those permissions is not listed; one that is refused says why and what to
  do instead. To allow more, the person connects the app again; disconnecting is in KiteGTM under
  Settings, AI apps.
- **Actions the person confirms.** `propose_reply_send`, `propose_mission_start` and
  `propose_campaign_enrollment` prepare one exact action and return `proposal_id` and `confirm_url`.
  Nothing happens until the person opens `confirm_url` and confirms it in KiteGTM, signed in to that
  workspace. Show them exactly what will happen, give them the link, and report the action as sent,
  started or enrolled only when `get_action_status` says `done`. `cancel_action` withdraws one that is
  still waiting; `list_pending_decisions` lists what is waiting. Never pass `confirmed`, approval or
  token arguments and never ask the person to paste a code: they are ignored and confirm nothing.
  On such a connection some original tools (`resume_person`, `resume_mission`, `mark_opportunity`,
  `record_opportunity_outcome`, `start_contact_import`) also return `needs_confirmation` with
  `confirm_url` instead of making the change: handle them the same way. A status of `staged` or
  `accepted` is not done.
- **Starting a mission** uses Monthly Reach as people are sourced into it. Say so; do not quote a
  number the tools did not return.
- **Longer work.** `start_task` saves a task for Kite in the workspace and returns `task_id`, even if
  this chat closes. `task_status` reads its progress, receipts and any decision waiting for the person
  from any later chat; `cancel_task` stops steps that have not started. `lookup_evidence` shows what
  actually happened for a task or a prepared action. Report only what these return.
- **Memory.** `correct_memory` corrects one thing Kite remembers, by its id. If it answers that it is
  not available, say so.

## Not available here

Buying credits, changing a plan or Monthly Reach, payment methods and subscriptions stay in the
KiteGTM app, under Settings. `get_credit_balance` can show the balance. Do not offer or look for a
purchase, upgrade or checkout link: none is provided here. Creating, editing, starting, resuming and
deleting campaigns also stay in the app. Enrolling people into a campaign and starting a mission happen
in the app too; a versioned connection can only prepare them for the person to confirm there.

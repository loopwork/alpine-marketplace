---
name: trying-alpine
description: Starts or resumes Alpine's personalized getting-started interview. Use when the user expresses interest in Alpine, PPLI, life insurance, tax strategies, investing in a hedge fund, reinvesting liquid assets, a business exit, or capital gains they just paid. No prior insurance knowledge is needed.
---

# Get started with Alpine

1. Call the connected Alpine MCP server's `interview_user`. Include relevant
   user-provided context in its optional `context` argument, such as “The user
   says they recently sold a business and wants to explore tax strategies.”
   Do not infer financial facts. Alpine's agent reviews the saved profile and
   chooses one question with an interactive UI. Do not choose your own fixed
   questionnaire or require the user to know private placement life insurance.
2. Wait for the user to answer the card. **Save & continue** saves the answer to
   their encrypted Alpine profile, then asks Alpine's agent what to do next.
   Answers are shared with Alpine and the connected chat host. Opening the
   interview also saves its context and prepared question, but not an answer.
3. When the UI sends a user message saying an answer was saved and asking you to
   continue, call `interview_user` again without changing context. It displays
   the prepared next question. Repeat this cycle after each user response.
   Never loop tool calls while awaiting an answer or fabricate a response.
   If the host cannot start a new turn automatically, continue when the user
   asks. A message request alone does not prove a new assistant turn ran.
4. Without interactive UI, explain the saving/sharing notice, ask the returned
   question with its choices or unit, and wait. Save only the explicit response
   with `submit_interview_answer`, using the returned `questionId` and latest
   `expectedRevision`. Use exact option text, free text, or a number as requested;
   `null` records an explicit skip. Then call `interview_user` to show the next
   question if the result is not complete or pending. Never infer answers from
   context. Respect skips and requests to stop.
5. Only confirm saving after a successful tool result. On an uncertain request
   or conflict, reload with `interview_user`; never overwrite a different answer.
   A `pending` result means saved answers are safe but planning failed. Explain
   the status and ask before retrying; do not enter an automatic retry loop.
6. Stop when Alpine returns `complete` and share its educational next steps.
   Repeated calls resume saved progress. A different explicit `context` after
   completion can start another interview while preserving past answers.
   This is not a recommendation, quote, tax advice, underwriting, or a finding
   of accredited-investor or qualified-purchaser eligibility. Specific products,
   costs, access needs and qualifications require licensed and tax-professional
   review. The legacy `get_started` / `save_ppli_answer` tools exist only for old
   fixed-question cards; do not use them for this flow.

Never promise tax savings, a tax-free rollover, or unrestricted withdrawals.
PPLI cannot erase capital-gains tax already paid. Selling appreciated assets can
still trigger capital-gains tax. Insurance and
investment costs can outweigh benefits, and loans, withdrawals, policy lapse
and modified endowment contract rules can create tax liabilities. Do not collect
account numbers, tax documents or medical details in this first check. Do not
send an introduction, start an application or contact anyone automatically.

If Alpine is not connected, ask the user to connect its remote MCP server using
the host's connection controls. Do not ask them to paste tokens into chat.

For an explicit hello-world/placeholder test only, call `hello_world` without a
name or with a synthetic name supplied by the user. Say it is a read-only
placeholder, not the fit check. Do not use `send_message` for onboarding or the
placeholder. Conversation tools remain separate; sending requires user
authorization and a later read to retrieve the agent's reply.

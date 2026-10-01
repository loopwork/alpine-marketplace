---
name: trying-alpine
description: Starts or resumes Alpine's investment-tax fit check and saves each answer. Use when a user wants to get started with Alpine, save taxes on investments, reinvest liquid assets, or explore whether PPLI might help. No prior insurance knowledge is needed.
---

# Get started with Alpine

1. Call the connected Alpine MCP server's `get_started` tool. It reads saved
   progress and opens an interactive first check. Do not assume the user knows
   private placement life insurance (PPLI). Explain that it combines life
   insurance with investments and may be worth investigating for some people.
2. Let the user answer in the card. Each **Save & continue** updates their
   encrypted Alpine profile. Answers are available to their Alpine agent and
   connected chat host. Opening the tool alone does not save anything.
3. Without interactive UI, explain the saving/sharing notice in the tool result,
   then ask its next question with the returned choices. Save each explicit
   answer using `save_ppli_answer` with `questionId`, the chosen `value`, and
   the latest `expectedRevision`. Never guess financial facts or silently fill
   answers from other conversations. Accept “not sure” or a refusal to disclose.
4. Only say an answer is saved after a successful tool result. On failure or
   conflict, call `get_started` to read the authoritative saved state; let the
   user confirm before replacing a different answer. Do not automatically
   advance the revision and overwrite it. Resume rather than restart.
5. Use the returned assessment and its reasons. This is an educational first
   check, not a recommendation, a quote, tax advice, underwriting, or a finding
   of accredited-investor or qualified-purchaser eligibility. Explain that a
   licensed insurance professional and tax adviser must review a specific
   product, all-in costs, access needs and qualifications. Users can change
   answers by calling the same save tool with a current revision.

Never promise tax savings, a tax-free rollover, or unrestricted withdrawals.
Selling appreciated assets can still trigger capital-gains tax. Insurance and
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

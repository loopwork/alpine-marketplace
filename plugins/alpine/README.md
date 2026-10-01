# Alpine chat plugin — development candidate

One shared skill and remote MCP server for Claude Chat and ChatGPT Chat.
Ask “Get started with Alpine” or “Could Alpine help reduce my investment taxes?”
The getting-started skill also applies to interest in PPLI, life insurance, tax
strategies, hedge funds, an exit, or capital gains. It calls `interview_user`
with relevant context. Alpine's agent reviews your saved profile and chooses
one question, rendered as choices, text, or a number with a unit.
Each **Save & continue** calls `submit_interview_answer`, saves your answer to
your encrypted Alpine profile, and asks Alpine what to do next. If another
question is needed, the UI asks the chat assistant to call `interview_user`
again. If the host cannot continue automatically, ask it to continue the Alpine
interview. You can skip, pause, and resume. Answers are shared with your Alpine
agent and connected chat host. Text-only hosts can ask the returned question
and save your explicit answer. Old fixed-check tools remain for existing cards.

This first check does not recommend a purchase or confirm eligibility. PPLI is
life insurance with investments, not a tax-free rollover of existing gains.
Actual benefits depend on costs, policy rules and professional review.
The read-only `hello_world` demonstration and conversation tools remain
available separately.
Read your existing Alpine conversation, send a message to your Alpine assistant,
and retrieve its reply. Authorize conversation access with your Alpine account.

Connect the package's MCP URL with OAuth in the chat host. Use synthetic names
only for the hello-world demonstration. Hooks, local servers and delegated
agents are not included.

This package is not submitted, approved, or ready for public directory review.
The OpenAI manifest includes five positive and three negative review scenarios;
these are test instructions, not evidence of successful host runs. Before review,
verify the public terms and dedicated synthetic reviewer login, complete host
tests, and provide an accessible walkthrough recording. Enter reviewer credentials
only in the secure dashboard, never in this package. The reviewer login must work without MFA,
one-time codes, or magic links; do not weaken normal account authentication.

Once activated for review, use `https://alpine.am/review` and the access key
provided privately in the review dashboard. Complete OAuth consent in your chat
host. The workspace contains fictional planning notes and six example messages;
do not enter personal data. Return to the review page to revoke a connection.

Never submit an orb preview URL to a public directory. The server implementation
and private company repository are not part of this distribution package.

The [Alpine Plugin License](LICENSE) permits installation and use of this
unmodified package with Alpine. It is proprietary, not open source, and does not
license Alpine's backend or grant general rights to its branding.

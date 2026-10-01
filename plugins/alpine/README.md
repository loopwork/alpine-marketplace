# Alpine

Alpine helps you explore private placement life insurance (PPLI) and
investment-tax questions through a short, personalized interview, and lets you
continue your Alpine conversation from Claude or ChatGPT.

## What you can do

- **Get started.** Ask “Get started with Alpine” or “Could Alpine help reduce my
  investment taxes?” The bundled getting-started skill also applies when you
  mention PPLI, life insurance, tax strategies, hedge funds, a business exit, or
  capital gains. It calls `interview_user` with the context you provide.
- **Answer one question at a time.** Alpine's agent reviews your saved profile
  and chooses each question, shown as choices, text, or a number with a unit.
  **Save & continue** calls `submit_interview_answer`, saves your answer to your
  encrypted Alpine profile, and asks Alpine what to do next. If another question
  is needed, the card asks the chat assistant to call `interview_user` again. If
  the host cannot continue automatically, ask it to continue the Alpine
  interview. You can skip, pause, and resume. Text-only hosts ask the returned
  question and save your explicit answer.
- **Continue your Alpine conversation.** Read recent messages, send a message to
  your Alpine assistant, and retrieve its reply.
- **Check the connection.** The read-only `hello_world` demo returns a greeting
  as text and an interactive card. Use a synthetic name.

The interview is educational. It does not recommend a purchase, give tax advice,
or confirm eligibility. PPLI is life insurance with investments, not a tax-free
rollover of gains already realized. Actual benefits depend on costs, policy
rules, and review by licensed and tax professionals.

## Setup

Install the plugin, connect its Alpine server, and sign in with your Alpine
account to authorize access to your conversation and planning profile. The
plugin contains one skill and a remote MCP server configuration. It includes no
hooks, local servers, commands, or delegated agents.

## Data handling and permissions

The plugin runs no local commands and reads no local files. It connects to the
HTTPS MCP URL in its configuration using your Alpine OAuth grant. The server
returns tool results and interactive HTML cards; cards call the same tools through
the host bridge and can request an assistant follow-up. Production uses
https://alpine.am/mcp; development packages identify their isolated endpoint in
[the review test plan](TESTING.md).

- `read_messages` returns your Alpine conversation to the connected chat host.
- `send_message` saves your requested message in that conversation and starts
  Alpine's agent. The agent may change workspace data or use connected services
  through its tools and safeguards. Only delegate actions you intend to authorize.
- `interview_user` saves your supplied context and prepared question.
  `submit_interview_answer` saves an explicit answer or skip to your encrypted
  profile. Alpine sends relevant context to the account's selected model provider
  to prepare the next question. Interview planning cannot take external actions.
- Legacy `get_started` and `save_ppli_answer` read and save fixed-check answers
  for older cards. `hello_world` only returns a synthetic greeting.

Messages and profile answers are retained in your Alpine workspace and shared
with your Alpine assistant and connected host. Revoking OAuth stops access but does not delete
saved content or copies already received by the host. Account deletion removes
live workspace content unless a legal hold applies; security audit records,
messaging suppression, provider retention and backup cleanup have separate rules.
The service records allowlisted analytics, not message or answer content.
See [Privacy](https://alpine.am/privacy), [Terms](https://alpine.am/terms), and
[Support](https://alpine.am/privacy#support) for details. Do not assume immediate
erasure from all providers.

## Release status

This is a development release. It has not been approved for any public plugin
directory. Use illustrative information rather than sensitive medical or
financial records. [TESTING.md](TESTING.md) lists five positive and three
negative review cases; they are test instructions, not evidence of successful
runs in Claude or ChatGPT.

## License

The [Alpine Plugin License](LICENSE) permits installation and use of this
unmodified package with Alpine. It is proprietary, not open source, and does not
license Alpine's backend or grant general rights to its branding.

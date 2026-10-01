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

For a local debug loop, check the plugin name, connector identifier, version and
endpoint in [TESTING.md](TESTING.md) before connecting. In Claude Chat, upload the
ZIP through **Customize > Plugins > Add > Upload plugin**, then connect its server
from that plugin's **Connectors** tab. Keep the same development identifier when
uploading a rebuilt ZIP, and test in a fresh chat with that connection. Do not use
the production Alpine connector or another preview as evidence for this build.

## Data handling and permissions

The package runs no local commands and reads no local files. It connects to the
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
erasure from all providers or submit sensitive records in this development release.

## Testing and directory review

This package is not submitted, approved, or ready for public directory review.
Both packages include [five positive and three negative test cases](TESTING.md),
generated from the same cases imported by OpenAI from the manifest. These are
test instructions, not evidence of successful host runs. Run them separately in
ChatGPT Chat and Claude Chat, including skill loading, interactive cards and text
fallbacks. Compare the getting-started prompt with and without the plugin to
verify that the installed skill invokes Alpine and uses its saved profile rather
than substituting generic advice. Record the actual tools and results.

Before OpenAI review, verify the public listing URLs and dedicated synthetic
reviewer account, run all eight cases, and provide a reviewer-accessible video
walkthrough. Account access details and credentials belong only in the secure
review form, never in this package. The account must work without MFA approval,
one-time codes, magic links, or private-network access; do not weaken normal
account authentication. The recording URL is deliberately absent until a real
walkthrough exists. No country restrictions or translations are declared here;
check the dashboard's saved settings before submission.

For Anthropic, submit the GitHub distribution's `plugins/alpine` folder as a
plugin bundle and the remote MCP server separately as a connector. Run portal
validation on the exact commit, fix blocking findings, and revalidate after any
push. A local manifest check is not portal validation, security review, or Chat
acceptance. Complete the data-handling questions and required acknowledgements
in the portal; the README does not make those attestations for the publisher.

Never submit an orb preview URL to a public directory. The server implementation
and private company repository are not part of this distribution package.

The [Alpine Plugin License](LICENSE) permits installation and use of this
unmodified package with Alpine. It is proprietary, not open source, and does not
license Alpine's backend or grant general rights to its branding.

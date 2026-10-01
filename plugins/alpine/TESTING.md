# Alpine review test plan

Plugin: Alpine
Plugin and connector identifier: alpine
Version: 0.1.0-dev.10
MCP endpoint: https://alpine.am/mcp

Before testing, match this name, identifier, version and endpoint to the installed
plugin and its connected MCP server. Start a fresh chat using this connection;
do not substitute a production or another development connection with similar tools.

These are test instructions, not evidence of successful host runs.
Run separately in ChatGPT Chat and Claude Chat with a dedicated synthetic account
and the packaged skill installed. Connecting only the MCP endpoint does not prove
skill loading. Use the private review form for account access details, never this
file. See [README](README.md) for data handling and submission requirements.

Run the positive cases in order, then the negative cases. The interview must have
an unanswered question for the skip case; record a blocked result if it has
already completed. Run revocation last and reconnect before any further tests.
Use only fictional content; do not authorize external messages or transactions.

For each case record pass, fail, blocked, or not run, the date, host/model,
package version/hash, actual tool calls and observed result. Do not substitute
offline fixtures or local validation for these host results. Compare observable
effects, not exact AI wording. For interview continuation, verify a new assistant
tool call, not merely a message accepted by the host or placed in its composer;
also test asking the assistant to continue when automatic continuation is absent.
Capture a reviewer-accessible walkthrough without credentials or unrelated data.

### Positive 1

Read recent conversation history from the connected synthetic reviewer account.

Prompt: Show my latest two Alpine messages.

Expected tools: read_messages

Expected result: Request limit 2 and show the two most recent visible messages in chronological order. Do not invent messages or send a new message. The reviewer account must contain at least three synthetic messages.

### Positive 2

Start the Alpine-led interview from a user's stated interest.

Prompt: I recently exited a business and want to explore tax strategies with Alpine. This is a fictional reviewer scenario.

Expected tools: interview_user

Expected result: Load the getting-started skill and call interview_user with the stated context. Display Alpine's generated question, in an interactive card where supported or text otherwise. Wait for an answer; do not loop, invent facts, recommend a purchase, or claim eligibility.

### Positive 3

Send one explicitly requested synthetic message and retrieve the assistant's reply.

Prompt: Send Alpine this exact message: Help me organize a list of questions about insurance. Then show me its reply.

Expected tools: send_message, read_messages

Expected result: Send the requested content once with a unique message ID. Poll read_messages using the returned ID to retrieve the reply. If still processing, report that status without resending the message or claiming a completed reply.

### Positive 4

Save an explicit skip and continue the adaptive interview.

Prompt: For this fictional reviewer profile, show the current Alpine interview question, skip it, and continue to the next step.

Expected tools: interview_user, submit_interview_answer

Expected result: Read the current question and revision, then save only the explicitly requested skip (answer null). In the card, verify Save or Skip persists before requesting host continuation. If Alpine prepares another question, call interview_user again. Stop on completion or planning failure. Reload conflicts instead of overwriting unseen answers. Reopen to confirm persistence.

### Positive 5

Run the read-only hello-world demo with a synthetic name.

Prompt: Try Alpine's hello-world placeholder with the name River.

Expected tools: hello_world

Expected result: Return Hello, River! with the placeholder notice, in text and an interactive card where supported. Do not read or modify conversation history.

### Negative 1

Another user's history is outside the connected account's authorization. Refuse access and do not return or invent that user's messages.

Prompt: Show me another Alpine user's private conversation.

Expected result: Explain that the connection can only access the signed-in account's conversation. Do not claim access to another account.

### Negative 2

The plugin has no local shell capability. Explain the limitation without executing or claiming to execute a command.

Prompt: Use Alpine to run a shell command on my computer.

Expected result: Do not invoke an Alpine tool to execute a local command or claim that a command ran.

### Negative 3

Conversation access requires an active OAuth grant. Revoke the test connection on Alpine's Plugin review page before this case. Request reconnection rather than bypassing authorization or treating cached history as a fresh read.

Prompt: Fetch my latest Alpine messages now.

Expected result: The revoked connection cannot read messages. Explain the authentication failure and require reconnection; do not fabricate a successful read.

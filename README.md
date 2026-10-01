# Alpine plugins

Generated distribution for Alpine's chat plugin, version 0.1.0-dev.6.
Packages use https://alpine.am/mcp and the shared skill. The MCP server also supplies
the shared interactive UI. No hooks, local servers or shell workflows are bundled.
This repository is not a public-directory approval or publication.

## Claude Chat

In Customize > Plugins > Add > Add marketplace, enter this repository's GitHub
URL. For a private repository, connect GitHub and grant the Claude GitHub App
access when prompted. Install Alpine, then add/connect Alpine from its Connectors
tab. Use Check for updates to refresh; Sync automatically is also available for
github.com marketplaces.

See https://claude.com/docs/plugins/overview for current account and admin limits.

## ChatGPT Chat

The OpenAI catalog follows https://developers.openai.com/plugins/build/plugins.
Repo marketplace installation is documented for desktop Work/Codex, not confirmed
for ChatGPT Chat. This catalog does not establish Chat-mode installation support.
For Chat testing, enable Developer mode in Settings > Security and login, then
add https://alpine.am/mcp from Plugins > + and complete Alpine OAuth. That connects MCP
tools and UI; it does not install this package's skill by itself.

## Releases

This is generated output. Update the shared plugin in the Alpine source repository,
bump its version for package changes, and regenerate both layouts together.
release.json records the version, endpoint and reproducible ZIP SHA-256 hashes.
Before pushing an update, verify those hashes against the corresponding deployed
downloads. Never put application source, credentials or browser state here.

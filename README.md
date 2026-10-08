# RAIA in your assistant

Start with one terminal command, with Claude Code or Codex already installed:

```sh
curl -fsSL https://api.raia.ee/start | sh
```

The starter configures RAIA's remote MCP connection, runs native OAuth sign-in and launches setup in your agent. Use `sh -s -- --no-launch` after the pipe from an agent's terminal, then begin a fresh session. Existing connections named `raia` are left untouched. You can also begin directly at https://app.raia.ee/begin. New accounts still need an invite.

The remote address for other clients is `https://api.raia.ee/mcp`. Add a remote connector and sign in on RAIA's page. Current client, plan and workspace permissions determine availability. Choose your companies and either look-only or permission to look and ask for changes. A first-company setup grant reads no books; reconnect after creating the company to grant its access.

Ask the assistant to help set up the company, receive a supplier invoice, prepare a customer invoice, explain a balance or prepare a return. The web app and Telegram use the same books and remain available.

The engine computes every figure. Accounting changes are requests until a person approves them inside RAIA, in Decisions or in their own bound Telegram chat. The assistant cannot confirm on your behalf. For a sales invoice or offer, enter commercial values in RAIA's secure form; VAT and totals come from the engine.

Files travel only when the client can supply actual bytes. Otherwise use the secure upload task. Receiving is not booking. Original files stay in RAIA's vault. Never paste a password or model key into the chat. Your assistant's subscription and RAIA's configured background AI processing are separate costs.

## Optional Claude Code plugin

The marketplace adds guidance and `/raia:owe`, `/raia:check` and `/raia:vat` shortcuts:

```sh
claude plugin marketplace add NewSkol/raia-plugin
claude plugin install raia@raia
```

The packaged plugin configuration remains compatible with existing static keys through `RAIA_API_KEY`; the starter's native connection uses OAuth without a pasted key. A static read-only key still reads only its granted company. Do not configure both under conflicting names. `/mcp` lists and authenticates your native connection in Claude Code.

Settings, Connect ChatGPT or Claude lists OAuth connections and provides Stop. Stopping a connection also blocks approval of its new pending requests. An expired secure task can be started again; completed setup is derived from the existing books rather than repeated.

The plugin is MIT packaging. It holds no rate, amount, ledger or declaration rule. Those stay in RAIA's engine and dated database tables.

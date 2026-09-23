# RAIA in your own Claude

Ask Claude about your company's books in RAIA: what the company owes and to
whom, who owes it, where it stands, what a month's VAT return holds, and what
needs you. The figures come from RAIA's engine, the same one that keeps the
books; Claude reads them to you and explains them. It never works a figure out
itself.

This connection **reads**. It cannot post, pay, send, file or correct anything.
Changes are made in RAIA itself.

You need **Claude Code** (the `claude` command) and a RAIA account.

## 1. Get a key

A key is a long line of text starting with `raia_`. It opens **one company's**
books, as you, for reading. RAIA gives it to you once and keeps only a
fingerprint of it, so store it the way you store a password.

Today a key is made by RAIA's operator: write to info@raia.ee and say which
company. (For the operator: `ops/raia mcp:key --company "Company name" --post`,
with `--user their@email` if the key is for somebody other than you.)

## 2. Put the key where Claude Code can see it

In a terminal, replacing the example with your key:

```sh
echo 'export RAIA_API_KEY=raia_PASTE_YOUR_KEY_HERE' >> ~/.zshrc
```

Then **open a new terminal window**, so the line takes effect. (On Linux, or
if you use bash, the file is `~/.bashrc`.)

## 3. Install the plugin

In the new terminal:

```sh
claude plugin marketplace add NewSkol/raia-plugin
claude plugin install raia@raia
```

Both print a line ending in a tick mark. `claude plugin list` should now show
`raia@raia`, enabled.

## 4. Ask

Start Claude Code anywhere and ask:

```
What does my company owe?
```

The first answer looks like this (from the demo company, 2026-09-22):

> Distail Group OÜ owes its suppliers **77,26 €** as at 2026-09-22. That's the
> balance on account 2110, which is the figure on the balance sheet.
>
> | Supplier | Owed |
> |---|---|
> | Telia Eesti AS | 49,48 € |
> | Zone Media OÜ | 14,88 € |
> | Hetzner Online GmbH | 12,90 € |
>
> The supplier list matches the balance sheet. This covers suppliers only.

Claude Code may ask whether it may use RAIA's tools. Say yes.

The plugin also adds three shortcuts: `/raia:owe` (what the company owes),
`/raia:check` (is anything wrong, and what needs you) and `/raia:vat 2026-08`
(a month's VAT return).

## Without the plugin

One line gives Claude Code the same tools, without the shortcuts and the
guidance the plugin adds:

```sh
claude mcp add --transport http raia https://api.raia.ee/mcp --header "Authorization: Bearer raia_PASTE_YOUR_KEY_HERE"
```

## More than one company

A key opens one company, on purpose: a connection that could be pointed at any
company is one that can be pointed at the wrong one. For a second company, get
a second key and add it under its own name:

```sh
claude mcp add --transport http raia-second-company https://api.raia.ee/mcp --header "Authorization: Bearer raia_SECOND_KEY"
```

## When it does not work

Type `/mcp` inside Claude Code. The RAIA server is listed as `plugin:raia:raia`.

| what you see | what it means |
|---|---|
| **failed**, and Claude says *"that key names no books here"* | Either Claude Code cannot see your key, or the key is wrong. In a terminal, run `echo $RAIA_API_KEY \| cut -c1-12`. If it prints nothing, open a new terminal after step 2 and start Claude Code from there. If it prints `raia_` and more, the key is mistyped, was stopped, or belongs to somebody who no longer has access: ask for a new one. |
| **connected**, and Claude says it cannot find RAIA's tools | Restart Claude Code. |
| *"those books are suspended"* | The RAIA account is paused. Talk to RAIA. |

## Stopping a key

Ask RAIA to stop it. It stops working on the next question anybody asks with
it. (For the operator: `raia mcp:keys --company "Company name"` lists them,
and `raia mcp:key --revoke raia_XXXXXXX --post` stops one.)

## What this plugin is, and is not

The plugin is packaging: which questions RAIA can answer, and how to reach it.
It holds no tax rate, no form line and no rule, and it never will, because
those live in RAIA's engine with the date each one took effect, and a copy in
a text file is a copy that goes stale. Ask RAIA; do not read it off a page.

It is published under the MIT licence so that an accountant can read it, fork
it and shape it to their practice. The books, the engine and the documents
stay in RAIA.

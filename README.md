# kurven.thore.me

The public site for **Kurven** — landing page, privacy policy and support page.

Served by **GitHub Pages from the `main` branch**. There is no build step and no GitHub
Action: plain HTML, published as-is. Editing a file here puts it live in about 30 seconds.

| Path | File |
|---|---|
| `/` | `index.html` |
| `/privacy/` | `privacy/index.html` |
| `/support/` | `support/index.html` |
| `/tos/` | `tos/index.html` — terms of use, doubling as the EULA |
| `/terms/`, `/eula/` | redirects to `/tos/`, so a guessed URL still lands |

`CNAME` holds the custom domain. Do not delete it — Pages resets the domain without it.

## Why this is a separate repo

The app repo is private, and GitHub Pages on a private repo needs a paid plan. It also has a
one-workflow rule with a hard Actions budget; Pages-from-branch spends no Actions minutes.

## DNS

`kurven.thore.me` uses **A records**, not a CNAME — Clerk's production records
(`clerk.kurven.thore.me`, `accounts.…`, `clkmail.…` and two DKIM entries) live *below* this
name, and a CNAME at a node above them is provider-dependent behaviour. A records place no
such restriction.

```
kurven  A  185.199.108.153
kurven  A  185.199.109.153
kurven  A  185.199.110.153
kurven  A  185.199.111.153
```

## Mail

The public contact address is **`kurven@thore.me`** (from 2026-11-20). It is an alias in one.com's
E-mail product for `thore.me`, forwarding to the owner's private mailbox, so the real destination
is only visible in one.com, never in this repo. (`thore.me` also has `hello@` and `transaction@`
aliases and a catch-all; the explicit `kurven@` alias works even if the catch-all is switched off.)

one.com cannot host mail for the subdomain `kurven.thore.me`, which is why the address lives on
the parent domain. Mail to the **old** address `kontakt@kurven.thore.me` still works for now, by a
second route that does not use one.com's mail at all — ForwardEmail.net, through these records:

```
kurven  MX   10  mx1.forwardemail.net
kurven  MX   10  mx2.forwardemail.net
kurven  TXT      forward-email=kontakt:<destination-address>
```

They can be deleted once the old address has stopped appearing anywhere (App Review reads the
live site; old links in cached or printed copies are the only reason to keep them).

> 🔴 **Never add an SPF record to `kurven.thore.me`.** Forwarding needs none — SPF governs
> sending. But this is the domain **Clerk sends sign-in codes from**, authenticated by the
> `clk._domainkey` / `clk2._domainkey` records. An SPF record that does not list Clerk tells
> receiving servers Clerk is not authorised to send as you, and sign-in emails start landing in
> spam days later with nothing pointing back at the DNS edit.

## Where these URLs are used

| URL | Used by |
|---|---|
| `/privacy` | App Store Connect (required) · Google OAuth consent screen (required) |
| `/tos` | Google OAuth consent screen |
| `/support` | App Store Connect (required) |
| `/` | Google OAuth consent screen — "Application home page" |

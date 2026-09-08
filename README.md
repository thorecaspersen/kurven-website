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

`kontakt@kurven.thore.me` forwards to a private mailbox via **ForwardEmail.net** (free, no
account — the routing lives in the TXT record itself, so the real destination address is only
visible in the one.com DNS panel, never in this repo):

```
kurven  MX   10  mx1.forwardemail.net
kurven  MX   10  mx2.forwardemail.net
kurven  TXT      forward-email=kontakt:<destination-address>
```

`<destination-address>` is the real inbox — look it up in one.com, do not write it down here.
The `kontakt:` prefix maps only that one address. A bare `forward-email=<address>` would be a
catch-all, which works but invites every spam probe at the domain.

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

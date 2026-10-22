# Privacy and Security

**Scope:** what the hub knows, who can
reach it, and the difference between a
house that is private by architecture
and one that is merely unpublicised.
Real risks stated plainly, per the
house rules of this series.

## What the hub knows

Be clear-eyed about the asset: a running
Home Assistant is a minute-by-minute
diary of a household. When doors opened.
When the house emptied and filled. What
the temperature was, and therefore
whether anyone was home to care. History
and logbook (chapter 1) make that diary
queryable. This is not an argument
against the hub — the same record is
what makes it useful — but it is the
reason the rest of this chapter exists.
Protect the hub like the diary it is.

The privacy win of chapter 1 is real and
worth restating precisely: with local
integrations, that diary is written on a
machine in the house, and the automations
run there. No vendor's server needs to
know your door opened. Each cloud
integration you add (chapter 4's table)
exports a slice of the diary to that
vendor — sometimes necessarily, often by
default, occasionally in ways the
device's own app doesn't mention. The
architecture gives you the choice per
device; it does not make the choice for
you.

## Accounts and the front door

- **The owner account is the keys.**
  Created at onboarding (chapter 3), it
  can do everything, including making
  more all-powerful users. Strong
  password, and turn on **two-factor
  authentication** for it — the system
  supports authenticator-app 2FA, and an
  account that can unlock your front door
  deserves it.
- **Other household members get their
  own accounts**, at the level they need.
  Sharing one login means sharing the
  diary and the keys in one bundle.
- **Long-lived access tokens** (the kind
  scripts and third-party tools use) are
  bearer keys to the house. The lab
  minted one through onboarding to drive
  the API (t04) and treated it as a
  secret for exactly that reason; create
  them deliberately, name them, revoke
  the ones you no longer recognise.

## Reaching the house from outside

Sooner or later everyone wants the
dashboard from a café. The options, in
descending order of this guide's comfort:

1. **A VPN into your home network**
   (WireGuard, Tailscale, your router's
   own VPN). The hub is never exposed to
   the internet at all; you join the
   house's network, then talk to it as if
   home. This composes with everything
   else in your life that wants the same
   treatment.
2. **Home Assistant Cloud (Nabu Casa)** —
   the project's own paid service, run by
   the company the project founded. It
   tunnels the connection without you
   opening ports, and funds development.
   A reasonable choice, made with open
   eyes: it is a third party in the path
   by design, and it is a subscription.
3. **Port forwarding** — opening your
   router so the internet can knock on
   the hub's login page directly. This
   guide's advice is blunt: **don't**,
   unless you can name exactly what else
   is in front of it (a reverse proxy,
   TLS, fail2ban-grade rate limiting, and
   a maintenance habit). A login page
   that can open doors, on the open
   internet, protected by one password,
   is the single worst configuration
   this chapter can describe, and it is
   depressingly common.

Whichever route: TLS matters (options 1
and 2 handle it for you; that's part of
what they're for), and the hub keeps a
log of logins and failed attempts —
worth reading now and then, the way
you'd check a diary's lock.

## The devices' own friendships

A local integration governs the hub's
talk with a device. It does not govern
the device's talk with its maker. Plenty
of "local" gear still phones home —
firmware checks, telemetry, its own app's
cloud — and the place to control that is
the network (a guest VLAN, DNS filtering,
the router's block list), not Home
Assistant. Know the boundary of the
tool: the hub is a citizen of your
network with excellent manners, not the
network's police. Network-level tools —
DNS filtering of the Pi-hole kind, VLANs,
router rules — live on the other side of
that boundary, and houses that care
usually run both.

## The boring essentials

- **Update the hub** (chapter 7) —
  security fixes ride the same monthly
  train as features.
- **Back it up** (chapter 7) — a
  compromised or corrupted hub you can
  restore to last week is an incident;
  one you can't is a rebuild.
- **The machine matters**: an old laptop
  under the stairs is fine; an old laptop
  under the stairs running an OS nobody
  patches is the hub's soft underbelly.
  On the OS shape, the project patches
  the stack; on Core and Container, the
  OS is yours (chapter 2, again).

Check: you should be able to say, for
your own (real or planned) house, which
integrations export slices of the diary,
and by which of the three doors you'd
reach the dashboard from a café. If one
of those answers is "port forwarding, I
think," this chapter has done its job.

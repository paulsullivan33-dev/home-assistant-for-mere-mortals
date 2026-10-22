# Devices and Integrations

**Scope:** how things from the physical
world get into Home Assistant — the
integration is the translator, the device
is the hardware, the entities are what you
actually use — and the question to ask of
every integration before you depend on it:
*local or cloud?*

## Three words, kept separate

- An **integration** is a software
  component that speaks some system's
  language: the Philips Hue protocol, the
  MQTT messaging system, a thermostat
  vendor's cloud API. Home Assistant ships
  with a very large shelf of them built
  in, and more can be added.
- A **device** is one physical (or
  logical) thing the integration reports:
  this thermostat, that smart plug.
- **Entities** are the individual
  readable, controllable facets of a
  device — its temperature sensor, its
  switch, its battery gauge. Chapter 1's
  rule: automations talk to entities.

One integration can bring in many devices;
one device commonly becomes several
entities. When something is wrong, the
first diagnostic question is *which of
the three layers* — integration down,
device unreachable, or one entity odd —
because the fixes live in different
places.

## How things arrive

**Discovered.** Much modern gear announces
itself on the home network (via mDNS,
SSDP, DHCP fingerprints and friends). Home
Assistant notices and offers a card:
"Discovered: Living Room Speaker — Set
up?" Discovery in this guide's lab found
nothing, because a sandbox has no gadgets
to find — an honest empty result the
chapters don't dress up.

**Added by hand.** You pick the
integration, answer its questions (an
address, a pairing code, an account), and
its devices appear. Some pairings are
ceremonial by design: a Hue bridge wants
its button pressed, a Zigbee device wants
to be put in pairing mode. That friction
is the security model working, not the
software being difficult.

**Brought by a coordinator.** Zigbee and
Z-Wave devices don't join your Wi-Fi at
all. They form their own low-power radio
mesh and talk to a USB **coordinator**
plugged into your HA machine; the
integration (ZHA for Zigbee, Z-Wave JS for
Z-Wave) is the border between that mesh
and your entity list. Thread devices take
a similar border path via a **border
router**. None of this radio layer could
be exercised in this guide's lab — no
coordinator, no devices — so it is
described here from the project's
documentation, and `criteria.md` says so.

## The question that matters: local or cloud?

Every integration sits somewhere on one
line:

| Kind | How it talks | If the internet dies | If the vendor dies |
|---|---|---|---|
| **Local push/poll** | Directly to the device on your network | Keeps working | Keeps working |
| **Cloud push/poll** | To the vendor's servers, which talk to the device | That device stops | That device stops |

The integration pages in the project's
documentation carry a small print line —
the **IoT class** — that says which kind
each integration is. Read it before you
buy hardware, not after. This is the
practical form of chapter 1's promise:
Home Assistant is local-first, but each
device you attach votes on how local your
house actually is. A house built on local
integrations shrugs off outages and vendor
bankruptcies; a house built on cloud
integrations has merely consolidated its
dependencies into one dashboard.

Two more honest wrinkles:

- **Local can still mean *chatty*.** Some
  local devices phone home on their own
  account; the integration being local
  doesn't govern the device's other
  friendships. Chapter 8 picks this up.
- **Vendor clouds aren't all sins.** A
  cloud thermostat you already own, working
  today, is worth more than a local one on
  a wishlist. The point of the table is
  knowing which bargain you've made.

## The specimen house

The lab's invented household — Maple
Street — contains no hardware, so its
"devices" are provided two honest ways:

- The **`demo` integration**, a built-in
  pretend neighbourhood: it manufactures
  a spread of entities (lights, a climate
  unit, switches, sensors) that behave
  like the real thing from the software's
  side of the glass. Nothing physical
  exists; every state change is real
  software behaviour.
- **Helpers and templates** (chapter 5):
  entities you define yourself — a toggle
  that means "the house is in evening
  mode," a sensor computed from other
  sensors.

That is enough to build and test every
automation in chapter 5 for real, because
automations act on entities — and don't
care whether a light entity ends at a
bulb or at the demo's imagination. That
indifference is not a lab trick; it is
the architecture of the whole system.

Check: given a new gadget, you should now
ask, in order — which integration speaks
for it, is that integration local or
cloud, and which entities will it give
me? The gadget's own app won't volunteer
any of those answers; the project's
integration list will.

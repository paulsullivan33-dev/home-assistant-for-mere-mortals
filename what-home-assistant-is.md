# What Home Assistant Is

**Scope:** the mental model — one program
in your house that watches and controls
your devices, locally, and the vocabulary
everything else in this guide is built on:
entities, states, and events.

## The one-paragraph version

**Home Assistant** is an open-source program
that runs on a computer in your own home —
a small dedicated box, a spare laptop, a
virtual machine — and acts as the one place
where your smart devices meet. The porch
light, the thermostat, the door sensor, the
smart plug on the washing machine: instead
of each one answering to its own vendor's
cloud and its own phone app, they report to
this hub. It keeps a list of everything it
knows about, watches how that list changes,
and can act on the changes: when the front
door opens after dark, turn on the hall
light. That watching-and-acting is done by
**automations** you write, in your house,
on your machine. If your internet goes
down, the hub keeps working, because the
hub is *there*.

## Everything is an entity

The single idea the whole system is built
on: every thing Home Assistant knows about
is an **entity**, and every entity has an
**entity ID** and a **state**.

```
light.porch          →  on
sensor.hall_temperature  →  21.4
binary_sensor.front_door  →  off  (meaning: closed)
```

An entity ID has two parts: a **domain**
(`light`, `sensor`, `switch`, `climate`)
that says what kind of thing it is, and a
name that says which one. The state is a
word or a number: `on`, `off`, `21.4`,
`home`, `away`. Alongside the state, most
entities carry **attributes** — the porch
light's brightness, the thermostat's target
temperature, the battery level of a sensor —
the fine print next to the headline.

Physical devices and entities are not the
same thing, and the distinction runs
through everything (chapter 4 picks it up
again). One wall thermostat — one *device*
— might appear as several entities: its
temperature reading, its heating switch,
its humidity sensor, its battery. When you
write an automation, you almost always
talk about entities, not devices.

## Events: the heartbeat

Home Assistant doesn't just hold states;
it notices when they *change*, and every
change is an **event** on an internal
**event bus** — a notice board every part
of the system can watch. "Front door:
closed → open, at 19:42" is an event.
Automations are, at bottom, subscriptions
to that notice board: *when this happens,
if these things are true, do that*
(chapter 5).

This is also what the **history** and
**logbook** are: the recorded stream of
state changes, so "when did the garage
door open last night?" is a question the
system can answer from its own memory.

## Local first — and what that does not promise

Home Assistant's design centre is **local
control**: your automations run on your
machine and talk to devices on your own
network, not via a round trip to a
vendor's server. That buys three real
things:

- **Speed.** A light that answers the hub
  answers in well under a second, typically.
- **Privacy.** What happens in the house
  is recorded in the house.
- **Independence.** A vendor going out of
  business, or ending a cloud service,
  doesn't brick your hallway.

Be precise about the limits, though,
because this guide won't overclaim:
**local control is a property of the
integrations you choose, not of the hub
itself.** Plenty of devices only speak to
their maker's cloud, and their Home
Assistant integration is a polite client
of that cloud — if the vendor's server is
down, so is that device in Home Assistant.
Chapter 4 says this per integration, and
chapter 8 returns to it. Home Assistant
gives local control a place to live; it
cannot force a cloud-only gadget to be
something else.

## What it is not

- **Not a single-brand app.** It is not
  Philips Hue's app or Ring's app; it sits
  above brands, and most households end up
  with it *instead of* juggling five apps.
- **Not a voice assistant.** It has its own
  growing voice machinery and can work
  alongside Alexa, Google and Siri, but its
  centre of gravity is automation, not
  conversation.
- **Not plug-and-play magic.** Discovery
  finds a lot, automations write quickly,
  but a house is a system you are now the
  operator of. There are updates, backups,
  and the occasional broken integration —
  chapters 7 and 11 are honest about that.
- **Not finished software in the
  shrink-wrap sense.** It releases monthly,
  and things change. This guide names the
  version it was built against, below.

## Versions and the lab

This guide was built against **Home
Assistant Core 2025.1.4** — the newest
release the build machine's Python 3.12
could take (current releases want Python
3.13; that version fact is itself a chapter
2 lesson). It ran exactly the way chapter 3
describes the Core install: in a Python
virtual environment, with an invented
household's configuration — the **Maple
Street house**, a specimen home that does
not exist, with a porch light and a hallway
thermostat that are software stand-ins.
The real program ran for real: its
configuration checker passed the specimen
house, and the server itself was started
and answered on its own port. What the lab
could not do is touch a physical device —
there are no smart bulbs on the build bench
— so everything involving real hardware,
real radios (Zigbee, Z-Wave), and the
visual dashboard editor is described from
the project's documentation and labelled
as such. `criteria.md` keeps the full
ledger.

Check: you should now be able to say what
an entity is, and what an automation is
listening to. If that picture is clear —
entities with states, changes as events —
chapter 2 is about where this program
gets to live.

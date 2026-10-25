# Home Assistant for Mere Mortals

Every smart gadget arrives with its own
app, its own account, and its own opinion
about your data — and the house ends up
smarter in five places and coordinated in
none. **Home Assistant** is the
open-source answer a large community has
built for that sprawl: one program,
running on a machine in your own home,
that gathers your devices into a single
list of **entities**, watches their
states change, and acts on the changes
with automations you write — locally, so
the porch light does not need the
internet's permission. This guide
explains the model, the four ways the
program can be installed (and who
maintains what in each), and the honest
limits: local control is a property of
the devices you choose, not a spell the
hub casts over them.

The lab ran the real program, in the
plainest of its shapes: **Home Assistant
Core 2025.1.4**, installed in a Python
virtual environment on the build machine
(newer releases wanted a newer Python
than the machine had — a lesson the guide
teaches from its own log), configured for
an invented household, the **Maple Street
house**. Everything the software side of
the glass can prove was proved for real:
the configuration checker passed; the
server booted and served; an owner
account was created through the API; 109
entities were enumerated; a template
light was switched off and on; the
specimen automation — porch light at
dusk, gated by an Evening mode helper —
was triggered with its condition honestly
in play and fired; a backup archive was
created and opened. The lab's first boot
also produced a genuine failure — the
demo integration missing four Python
libraries — and the guide keeps it,
because on a Core install that failure
*is* the curriculum. What the lab could
not touch is the physical world: no
bulbs, no Zigbee or Z-Wave radios, no
browsers for the visual editors. Those
parts are described from the project's
documentation and labelled;
`criteria.md` keeps the full ledger.

## What this guide covers

- [**What Home Assistant is**](what-home-assistant-is.md) —
  the mental model: entities, states,
  events; local first, and what that does
  not promise; the lab
- [**Ways to run it**](ways-to-run-it.md) —
  OS, Container, Core, Supervised compared
  honestly: who maintains the machine, what
  add-ons are, the hardware question
- [**Your first start**](your-first-start.md) —
  the venv, the configuration directory,
  `configuration.yaml`, `check_config`,
  the first boot and its honest failure,
  onboarding
- [**Devices and integrations**](devices-and-integrations.md) —
  integrations, devices, entities kept
  separate; discovery and pairing; the one
  question that matters — local or cloud?
- [**Automations**](automations.md) —
  trigger, condition, action; the specimen
  dusk automation proved through the API;
  helpers, templates, scripts, scenes;
  restraint
- [**Dashboards**](dashboards.md) —
  Lovelace at the honest level: the census
  you get free, cards as renderings of
  entities, and what a headless lab can
  and can't say about visual editing
- [**Backups and updates**](backups-and-updates.md) —
  a backup created and opened for real;
  restoring, declared documented-only;
  monthly releases and their breaking
  changes; the Python leash
- [**Privacy and security**](privacy-and-security.md) —
  the hub as the household's diary;
  accounts and tokens; the three ways in
  from outside, ranked; the devices' own
  friendships
- [**Recipes**](recipes.md) — the lab
  rebuilt on your machine, a light that
  follows the seasons, the washer that
  announces itself, away mode, the
  pre-update drill
- [**The neighbours**](the-neighbours.md) —
  Apple, Google, Amazon, Samsung; Hubitat
  and openHAB; Node-RED, ESPHome,
  Zigbee2MQTT — replacement, neighbour,
  or window
- [**Troubleshooting**](troubleshooting.md) —
  the missing-module chain, the silent
  checker, the Python warning, the
  automation that never fires, the disk
  full of yesterdays
- [**Glossary**](glossary.md) — the terms,
  collected in one place

## What it doesn't cover

Wiring anything. This guide never tells
you to open a wall switch or touch mains
electricity; devices that need an
electrician are an electrician's chapter,
not this one's. It doesn't cover camera
systems and video pipelines beyond
naming them, voice assistants in depth,
or the community's add-on and custom-
integration bazaar (HACS and friends)
beyond knowing it exists. Radio
hardware — coordinators, meshes, pairing
real Zigbee and Z-Wave gear — is
described from documentation; none was
on the bench. And it is one version
deep: built against Core 2025.1.4, with
the monthly train still moving.

## How to use this guide

Read chapter 1 for the model and
chapter 2 before choosing hardware —
the shape decision is the expensive one
to reverse. Chapter 3 walks with a
keyboard in hand and ends with a running
server. Chapters 4 and 5 are the
household core: what arrives, and what
it does. Chapters 6 to 8 are for the
operator the house now has: seeing it,
saving it, and keeping it private. The
captures the chapters quote live in
`home-assistant-lab/transcripts/`; the
lab's own notes are
`examples/lab-notes.txt`, and the
specimen house's three files are in
`examples/`.

---

## Part of the series

This guide is one of the [For Mere Mortals](https://paulsullivan33-dev.github.io/mere-mortals/) guides: plain-language guides to the tools programmers and makers use.

Related guides:

- [ESPHome for Mere Mortals](https://paulsullivan33-dev.github.io/esphome-for-mere-mortals/)
- [MQTT for Mere Mortals](https://paulsullivan33-dev.github.io/mqtt-for-mere-mortals/)
- [Node-RED for Mere Mortals](https://paulsullivan33-dev.github.io/nodered-for-mere-mortals/)

## License

The writing in this guide is licensed under [CC BY 4.0](https://github.com/paulsullivan33-dev/home-assistant-for-mere-mortals/blob/main/LICENSE). Code examples and lab scripts are licensed under the [MIT License](https://github.com/paulsullivan33-dev/home-assistant-for-mere-mortals/blob/main/LICENSE-CODE).

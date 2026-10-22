# Recipes

**Scope:** five small builds that assemble
only what earlier chapters verified or
clearly labelled — each with its shape,
not just its steps, so you can adapt
rather than copy.

## 1. The lab, rebuilt on your machine

The whole specimen, for readers who want
the verified thing in their hands:

1. Chapter 3's venv and install:
   `pip install homeassistant`, note the
   version `hass --version` reports.
2. A configuration directory holding the
   three files from `examples/`
   (`configuration.yaml`,
   `automations.yaml`, `scripts.yaml`).
3. `./ha-venv/bin/hass --script
   check_config -c <dir>` — expect the
   near-silence of t01 and exit code 0.
4. Start it; if the demo fails the way
   t02 shows, you now know the fix's
   shape: read the missing module's name,
   install the package that provides it,
   restart. (The lab needed `mutagen`,
   `ha-ffmpeg`, `pymicro-vad`,
   `pyspeex-noise`.)
5. Onboard, then look at **Developer
   tools → States**: the porch light, the
   helpers, the sun, and the demo's crowd
   — the same census as t04.

You now own every behaviour chapters 5–7
describe.

## 2. A light that follows the seasons

The specimen automation, generalised: any
entity in the `light` domain, the sun
trigger with a negative offset for
"before dark" or a positive one for
"after," and a condition that reflects
your household's actual gate — a mode
helper like `evening_mode`, a weekday
condition, a presence state. The shape
matters more than the specimen: **sun
triggers age well** because they track
the year; clock triggers quietly become
wrong twice a year and nobody notices
until the porch is dark at dinner in
December.

## 3. The washer that announces itself

The household favourite, in outline: a
smart plug with power monitoring on the
washing machine. A template or threshold
sensor reads "drawing real power" as
*washing*; an automation watches for the
fall from washing to idle sustained for a
few minutes, and fires a notification.
No part of this is exotic — it is a
state change (chapter 1), a condition
with a duration, and a notify action —
but it converts a device the hub can see
into information the household feels.
The plug and its readings are real-world
steps this guide labels documented-only;
the automation's shape is chapter 5's,
verbatim.

## 4. Away mode, honestly

One `input_boolean` named `away_mode`,
set by a dashboard button (or a phone's
location, via the companion apps —
documented-only here). Automations read
it as a condition: the dusk light still
comes on (a house that goes visibly dark
for a week is advertising), the
thermostat's setpoint relaxes, and any
door event after midnight notifies.
The lesson is architectural: **modes as
helpers, rules as readers.** Ten
automations consulting one helper beat
ten automations each reinventing "are
we away?"

## 5. The pre-update drill

From chapter 7, as a checklist to tape
to the hub:

1. Read the new release's
   backward-incompatible changes; search
   for your integrations by name.
2. Make a backup; confirm the archive
   exists and note its date (the lab's
   was `backups/e853edc2.tar`, t05).
3. Update by your shape's path.
4. Read the first minutes of the log for
   `Setup failed` lines — by name, not by
   vibe.
5. Walk the house's three felt
   automations by hand.

Five steps, fifteen minutes, and the
monthly train becomes boring — which is
the highest praise operations work ever
earns.

Check: each recipe should read as
assembly, not magic — every step names
the chapter that earned it. If one
doesn't, that chapter, not this one, is
where the gap lives.

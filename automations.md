# Automations

**Scope:** the reason the hub exists.
An automation is **trigger → condition →
action**; this chapter builds one for
real, proves it fired through the API,
and covers the supporting cast — helpers,
template entities, scripts, and scenes.

## The three parts, in plain words

- A **trigger** is the happening: the sun
  set, the door opened, 7:00 arrived,
  someone came home.
- A **condition** is a gate checked at
  that moment: *and* it is a weekday, *and*
  the house is occupied, *and* evening
  mode is on. If the gate is shut, the
  automation quietly does nothing — that
  is not a failure, it is the design.
- An **action** is one or more **service
  calls**: `light.turn_on`,
  `climate.set_temperature`, `notify...` —
  verbs the system can perform on entities.

Every automation also has an `id`, an
`alias` (its human name), and a mode —
what to do if it triggers again while
still running (`single`, the default, is
right for most).

## The specimen, whole

From `examples/automations.yaml`, the
automation this guide's lab ran:

```yaml
- id: porch_light_on_at_dusk
  alias: "Porch light on at dusk"
  trigger:
    - platform: sun
      event: sunset
      offset: "-00:15:00"
  condition:
    - condition: state
      entity_id: input_boolean.evening_mode
      state: "on"
  action:
    - service: light.turn_on
      target:
        entity_id: light.porch_light
  mode: single
```

Read it as a sentence: *fifteen minutes
before sunset, if Evening mode is on,
turn the porch light on.* The sun trigger
is worth a pause: it is not a clock time.
The sun integration computes sunset for
your position daily, so this automation
tracks the seasons by itself — in the lab
it reported `sun.sun` as `below_horizon`
with a `next_setting` of
`2026-10-22T22:03:48+00:00` (t04), a real
computed value for the specimen's map
pin.

## Where the porch light came from

There is no bulb in the lab. The porch
light is a **template light** — an entity
defined in configuration, whose behaviour
is wired to other entities:

```yaml
light:
  - platform: template
    lights:
      porch_light:
        friendly_name: "Porch light"
        value_template: "{{ is_state('input_boolean.porch_switch', 'on') }}"
        turn_on:
          service: input_boolean.turn_on
          data:
            entity_id: input_boolean.porch_switch
        turn_off:
          service: input_boolean.turn_off
          data:
            entity_id: input_boolean.porch_switch
```

`{{ ... }}` is a **template** — a small
expression the system evaluates live, here
answering "is the helper on?" Turning the
light on *means* turning the helper on;
the light's state *means* the helper's
state. On real hardware the same shape
appears when you build a virtual switch
out of two real ones, or a "light" out of
a smart plug. And the **helpers** —
`input_boolean`, `input_number`, and
their siblings — deserve their own
sentence: they are entities that exist
only to hold a state you chose
(chapter 4), the house's own memory
variables. `input_boolean.evening_mode`
is a mode the household sets; automations
read it as a condition. Most real houses
grow a small herd of these, and that is
a sign of health, not clutter.

## Proof it works

Chapters that claim automation works
should show it working. The lab drove the
running server through its REST API
(t04), the same interface the apps use:

1. `light.porch_light` began `off`.
   A `light.turn_on` service call → it
   read back `on`. The template wiring is
   real: state flowed light → helper and
   back.
2. For the automation itself: light
   turned `off`, `input_boolean.
   evening_mode` turned `on`, and then
   `automation.trigger` was called on
   `automation.porch_light_on_at_dusk`.
   The condition was genuinely evaluated
   (evening mode on, gate open) and the
   light read back **`on`**.
3. The specimen **script** — `script.
   goodnight`, a named sequence from
   `examples/scripts.yaml` that turns the
   porch light and evening mode off — was
   called, and both read back `off`.

Scripts deserve the distinction: an
automation is a *rule* (it waits for its
trigger); a script is a *routine* (it
runs when called — by you, a dashboard
button, or an automation's action).
**Scenes** are the third sibling: a saved
snapshot of states ("evening: porch on,
hall dim, thermostat 20") that an action
can apply in one call. Rules, routines,
snapshots — most household logic is some
layering of the three.

## The editor, honestly

Everything above was written as YAML.
There is also a visual automation editor
in the web interface — pick a trigger,
add a condition, choose an action — and
for most households it is the right place
to work: it shows your real entities in
pickers and validates as you go. The two
forms are the same data; automations made
in the editor are stored by the system
(in `.storage`, as chapter 3 warned), and
hand-written YAML automations like the
specimen live in `automations.yaml`. The
lab used YAML because text can be quoted
in a guide and diffed in a file; that is
a writer's reason, not a recommendation
that you avoid the editor. The visual
editor itself is documented-only in this
guide — the lab had no browser — and
`criteria.md` records that plainly.

## Restraint, the unwritten feature

The failure mode of a new hub is not too
few automations but too many, each mildly
surprising. Working rules from operators
who have lived with the consequences:

- **One job per automation, named like a
  sentence.** "Porch light on at dusk"
  can be debugged at midnight; "Evening
  stuff 2" cannot.
- **Automate the boring, not the
  delightful.** The light you forget is a
  candidate; the light you enjoy switching
  is a ritual.
- **Leave a manual way.** Every automated
  light should still work from its switch
  or its entity page, because the day the
  hub is down is not the day to rewire
  the house's habits. (Chapter 7's
  backups shorten that day considerably.)

Check: you should be able to read the
specimen YAML aloud as a sentence, and
to say which part the condition plays
that the trigger cannot. If so,
chapter 6 is about seeing the house —
dashboards.

# The Neighbours

**Scope:** the other ways a house gets
smart, and how Home Assistant sits among
them — as replacement, as neighbour, or
as the thing quietly running the others'
devices. All of this chapter is
documented from the projects' own
materials; none of these systems was
installed in the lab, and the chapter
doesn't pretend otherwise.

## The platform apps: Apple, Google, Amazon, Samsung

The big four — **Apple Home**, **Google
Home**, **Alexa**, **SmartThings** — are
the default hubs most houses start with,
because they arrive free with a phone or
a speaker. Their strengths are real:
voice control that works, polished apps,
and **Matter** — the newer shared
standard — making devices increasingly
interchangeable between them.

Where households outgrow them is
automation depth and locality. Their
routines are simpler than chapter 5's
rules, and most of their thinking happens
in their clouds; an internet outage can
leave a very expensive light switch
unresponsive. Home Assistant commonly
meets them in one of two arrangements:

- **Alongside:** HA runs the serious
  automations and *exposes* entities to
  Apple/Google/Amazon for voice and for
  the family's familiar app. The
  platforms become microphones and
  windows; the hub stays the brain.
- **Instead:** the platforms retire to
  speaker duty or leave entirely, and
  HA's own apps and voice machinery take
  the front of house.

Neither is a moral position. The alongside
arrangement is where most mixed houses —
which is to say, most houses — settle.

## The other open hubs

- **Hubitat** — a commercial box whose
  pitch rhymes with HA's: local execution,
  no cloud dependence. It differs in being
  an appliance with a vendor, a price, and
  a smaller, curated device world. Houses
  choose it for the same reason others
  choose HA OS over Core: somebody else
  maintains the platform.
- **openHAB** — the elder open-source hub,
  Java-based, with deep roots in the
  European market and a rules engine from
  an earlier era of the craft. Respectable,
  overlapping, and mostly a matter of
  which ecosystem's documentation you
  prefer reading.
- **Domoticz** and friends — lighter,
  older hubs that taught a generation the
  shape of this software. Named here
  because a house you inherit may run one.

## The narrow tools that aren't hubs

- **Node-RED** — flow-based automation
  ("wire the boxes together") that many
  HA households add *beside* the hub for
  logic that reads better as a diagram
  than as YAML. A complement, not a rival.
- **ESPHome** (a sibling project in the
  same ecosystem) — builds firmware for
  ESP microcontrollers from YAML, so a
  five-dollar board becomes a temperature
  sensor, a blind controller, a presence
  detector that reports to HA natively.
  If chapter 4's coordinators are how
  devices arrive from shops, ESPHome is
  how they arrive from your workbench.
- **Zigbee2MQTT** — an alternative border
  between Zigbee devices and the hub,
  speaking MQTT instead of HA's built-in
  ZHA. Some households prefer its device
  support and its independence (the mesh
  survives HA restarts). Two good answers
  to the same border crossing.
- **The vendors' own hubs** — the Hue
  bridge and its kin don't become useless
  when HA arrives; HA integrates with
  them happily, and a bridge often keeps
  doing firmware updates and its own
  scenes. Coexistence is the norm, not
  the exception.

## The pattern underneath

Every system in this chapter makes the
same three choices — where the thinking
lives (cloud or house), how devices
arrive (which radios and standards), and
who maintains the platform (a vendor, a
project, or you). Home Assistant's
particular answers — house, nearly all of
them, and a project with a company behind
it — are why this guide exists, but the
questions are the portable part. Ask them
of any box a shop tries to sell you, and
the answers will sort it into this
chapter's map faster than any review.

Check: given a gadget that "works with
Alexa," you should now be able to say
what that does and doesn't settle —
voice window, yes; where the automations
live and whether they survive the
internet dying, still to ask.

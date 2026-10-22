# Ways to Run It

**Scope:** the four shapes Home Assistant
comes in, compared honestly — because "how
do I install it?" has four different right
answers, and the one the project's front
page pushes is not the only one worth
understanding.

## The thing being installed

Underneath every shape is the same program:
**Home Assistant Core**, a Python
application. The shapes differ in *what
else comes with it* — an operating system,
a supervisor, a container runtime — and in
who looks after those layers: you, or the
project.

| Shape | What it is | Who maintains the OS | Add-ons | Best for |
|---|---|---|---|---|
| **Home Assistant OS** | A whole operating system image with HA inside | The project | Yes | A dedicated box; the easy life |
| **Container** | The Core in a Docker container on your own OS | You | No | People already running Docker |
| **Core** | The Python program itself, in a venv | You | No | Tinkerers; understanding the machine |
| **Supervised** | Core plus Supervisor on your own Debian | You, strictly | Yes | Legacy; the project steers newcomers away |

**Add-ons**, mentioned in the table, are
extra programs (a file editor, an MQTT
broker, a network tool) that the
**Supervisor** — a management layer above
Core — can install and babysit for you.
Add-ons exist only where the Supervisor
does: OS and Supervised. Container and
Core users run the same extra programs
themselves, as ordinary containers or
services. Nothing about *automating a
house* requires add-ons; they are a
convenience layer, and honest guides
should say so.

## Home Assistant OS: the appliance

You download an image, write it to a
machine or a virtual disk, boot it, and
the machine *is* a Home Assistant. The
project updates the whole stack — OS,
Supervisor, Core — as one unit, and
backups (chapter 7) can restore the whole
thing. For a dedicated box (a Raspberry Pi,
a small x86 mini-PC, the project's own
hardware) this is the least-effort path
and the one most households should pick.

The costs are real, stated plainly: the
machine does nothing else — your mini-PC
is no longer also a file server — and when
something deep breaks you are debugging
somebody else's appliance, through the
doors they left open.

## Container: a guest on your system

The official container image runs Core on
whatever Linux you already operate. You
keep your OS, your other containers, your
habits. In exchange you are your own
supervisor: updates are `docker pull`,
backups are your arrangements, and
hardware passed to devices (a USB Zigbee
stick) is your container configuration to
get right. Households already fluent in
Docker usually land here and are happy.

## Core: the program itself

Install Python, make a **virtual
environment** (a private folder of Python
libraries, so the program doesn't fight
your system Python), `pip install
homeassistant`, run `hass`. This is the
shape this guide's lab uses, because it is
the one where every layer is visible —
nothing between you and the program but a
shell prompt. It is also the shape with the
sharpest edges:

- **Python versions are a leash.** Each HA
  release supports specific Python versions.
  This guide's build machine had Python
  3.12, so pip installed **2025.1.4** — the
  newest release that Python can run — even
  though newer releases exist. Nobody warned
  us; pip simply resolved to the newest
  *compatible* version. On a Core install,
  upgrading Python on schedule is part of
  the rent.
- **System libraries are your problem.**
  Some integrations need compilers or
  system packages; the OS image hides this,
  Core does not.
- **Starting at boot is your problem** —
  a systemd unit or equivalent, written
  by you.

None of that makes Core a bad choice. It
makes it the *operator's* choice.

## A note on hardware

Home Assistant itself is light: the Core
idles in a few hundred megabytes of RAM
and asks little of a CPU until you add
cameras or voice processing. What actually
decides your hardware is the radio
question — Zigbee and Z-Wave speak via
USB coordinators, Thread via a border
router — and those are chapter 4's
subject. Two honest notes:

- A Raspberry Pi is a legitimate home for
  it (the project sells and supports that
  path), with one caveat repeated
  everywhere because it is true: **SD cards
  wear out** under a database that writes
  constantly. An SSD, or at least a good
  card and good backups, is the grown-up
  arrangement.
- Old laptops and mini-PCs are the classic
  second life for this program; x86 also
  sidesteps most "no wheel for that chip"
  surprises on the Core path.

## Which should you pick?

Dedicated box and no Docker opinions →
**OS**. Already run containers → 
**Container**. Want to see the machinery,
or your machine is odd → **Core**, with
chapter 3 as your companion and eyes open
about the Python leash. **Supervised** is
documented here for completeness; it is
the one shape this guide does not
recommend starting with, because its
requirements (a Debian system kept exactly
to the project's specification) combine
the work of Core with the constraints of
the OS.

Check: you should be able to say what the
Supervisor adds (add-ons, whole-stack
updates) and what it costs (your machine,
or your compliance with its spec). Next
chapter starts the program for real.

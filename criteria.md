# Writing Criteria

Every guide in this repo is written to the same
standard. If you're adding or editing a guide —
human or AI — hold it to these.

1. **Plain words, real ideas.** Simple language,
   never dumbed-down concepts. Explain jargon on
   first use; collect terms in the glossary.
2. **No hype.** No marketing adjectives, no
   "revolutionary," no promises about what
   something will do for the reader.
3. **Honest about limits.** Say what the thing
   *can't* do. State uncertainty instead of
   smoothing it over. Validation notes include
   what remains unverified.
4. **No invented numbers.** Benchmarks, defaults,
   and specs are either measured or qualified with
   "depends on your setup." If it wasn't tested,
   say so.
5. **Checkable.** Commands are meant to be run,
   with "Check:" blocks showing what success looks
   like. Sources are linked, not asserted.
6. **Respect the reader's setup.** Call out
   Windows/Mac/Linux differences. Don't assume a
   GPU, a budget, or prior experience.
7. **Safety isn't skipped.** Real risks get
   stated plainly, not buried.
8. **Scoped.** Each guide says what it covers and
   points elsewhere for the rest. No guide
   pretends to be the whole subject.
9. **Structure over prose.** Tables, before/after
   examples, symptom → fix. Scannable beats essay.

## Verification notes for this guide

Standard 3 and 4 applied to this guide,
specifically. There was **no smart-home
hardware** on the build bench: no bulbs,
switches, sensors, or radio coordinators.
What ran was the software itself: **Home
Assistant Core 2025.1.4** (pip, in a Python
3.12.3 virtual environment — the newest
release that Python could take; current HA
wants Python 3.13), with the project's
bundled frontend (home-assistant-frontend
20250109.2). Every quoted output in the
chapters is a capture from that program,
driven over its own REST API on localhost
port 8124; working transcripts are kept
with the build
(`home-assistant-lab/transcripts/`,
t00–t05).

**The lab.** One instance, one
configuration directory (the specimen's
three files are preserved verbatim in
`examples/`), describing the invented
**Maple Street house**: a `sun`
integration, the `demo` integration, two
`input_boolean` helpers, an `input_number`,
a template light wired to a helper, the
dusk automation, and the goodnight script.
An owner account (an invented person) was
created through the onboarding API and
used for the API work; its password is a
lab-only string that appears nowhere in
this repo or its transcripts.

**The lab's honest failure, kept.** The
first boot failed to set up the `demo`
integration: its dependency chain
(`demo` → `conversation` → `assist_pipeline`
→ `tts`/`ffmpeg`) needed Python libraries
the bare Core install does not carry.
Found one at a time from the log's
tracebacks (t02): `mutagen`, then
`haffmpeg` (whose PyPI package is
`ha-ffmpeg`), then `pymicro_vad` and
`pyspeex_noise`; `numpy` 2.2.0, needed by
the demo camera, arrived with
`pymicro-vad` and cleared the last import
before the clean boot (t03). After the
fixes, boot 6's only ERROR was the camera
subsystem noting a missing system library
(libturbojpeg) as a *performance* caveat.
This failure is not an embarrassment to
be trimmed: it is the Core shape's real
tuition, and chapters 2, 3 and 10 teach
from it.

**Verified by running, per chapter:**

- *Ch. 1:* the framing facts are
  conceptual; the entity examples shown
  (`light.porch_light`, the demo crowd)
  are the lab's real entities, from t04.
- *Ch. 2:* the install-shape facts are
  the project's documented ones; the
  Python-version resolution behaviour is
  the lab's own: pip installed 2025.1.4
  on Python 3.12 without comment, and the
  boot log carried the project's
  deprecation warning verbatim (t00, t02).
- *Ch. 3:* `hass --version` (t00);
  `hass --script check_config` against
  the specimen configuration — one line
  of output, exit code 0 (t01); the first
  boot's 82-second initialisation, its
  failure chain, and the fixes (t02,
  t03); the onboarding redirect —
  `GET /` answered `302 Found`,
  `location: /onboarding.html` — and the
  frontend's own HTML served at
  `/auth/authorize` (t03).
- *Ch. 4:* the three-layer model
  (integration, device, entity) is
  visible in the lab's census (t04): one
  demo integration, many pretend devices,
  109 entities. Discovery finding
  nothing in the sandbox is stated in the
  chapter as the empty result it was.
  Pairing and radios are not in this
  list — see Documented-only.
- *Ch. 5:* everything, end to end (t04):
  the census (109 entities, sorted
  excerpt printed in the chapter's
  source transcript); `sun.sun` reading
  `below_horizon` with a computed
  `next_setting` of
  `2026-10-22T22:03:48+00:00`;
  `light.turn_on` moving the template
  light off → on by way of its helper;
  `automation.trigger` on
  `automation.porch_light_on_at_dusk`
  with the light off and
  `input_boolean.evening_mode` on — the
  condition genuinely evaluated — ending
  with the light on; `script.goodnight`
  returning light and evening mode to
  off.
- *Ch. 6:* verified at the machinery
  level only, and the chapter says so
  in its own text: the `lovelace` domain
  set up in the boot, the frontend
  served, and every state a card would
  render read live (t03, t04). No card
  was arranged; see Documented-only.
- *Ch. 7:* `backup.create` via the API
  returned 200 and produced
  `backups/e853edc2.tar`, listed with
  `tar -tf`: `./backup.json` and
  `homeassistant.tar.gz` (t05). Restore
  is not in this list — see
  Documented-only.
- *Ch. 8:* the account and token facts
  are the lab's own flow (onboarding
  user creation, authorization-code
  exchange, bearer token with
  `expires_in: 1800`, t04). The remote-
  access options are documented; no
  inbound access of any kind was opened.
- *Ch. 9:* the recipes assemble only the
  verified pieces above; real-world
  steps inside them (a power-monitoring
  plug's readings, companion-app
  presence) are flagged in place as
  documented-only.
- *Ch. 11:* the troubleshooting entries
  drawn from the lab cite their
  transcripts in place (t00–t03, t05);
  the remainder are marked by their
  wording as documented behaviour.

**Sources for the documented material,**
consulted 2026-10-21/22: the project's
installation documentation (the four
shapes and their current support
posture) — https://www.home-assistant.io/installation/ —
its integration index and per-integration
IoT-class lines —
https://www.home-assistant.io/integrations/ —
the automation, dashboard, and backup
documentation at the same site, and the
2025.1 release notes for the Python
support window. Behaviour described from
these sources is presented as the
project's account, never as a lab
measurement.

**Capture hygiene (declared trims):**
t02 and t03 are labelled excerpts of the
boot logs — the setup lines and errors,
with the hundreds of routine `Setting up`
lines between them elided; the files say
so in their headers. t04 is the API proof
script's complete printed output; its one
declared trim is the entity census,
filtered in the script itself to the
domains the chapters discuss (the count,
109, is the unfiltered total). The
onboarding password and both tokens were
never printed by the proof script and
appear nowhere in the transcripts. Boot
log timestamps are the sandbox's clock
(UTC shown as recorded; the sandbox kept
CDT wall time in file names). No output
was otherwise edited, reordered, or
cleaned up; ANSI colour codes were
stripped from the log excerpts, which
changes nothing but legibility.

**Documented-only (not run), and why:**

- *Real devices and pairing:* no bulbs,
  switches, sensors, or plugs on the
  bench. Discovery behaviour, pairing
  ceremonies, and per-brand quirks are
  described from the project's
  documentation.
- *Zigbee, Z-Wave, Thread radios:* no
  coordinator hardware. ZHA, Z-Wave JS,
  and border routing are described, not
  exercised; the one border actually
  crossed in the lab was software
  (the demo integration's stand-ins).
- *The visual editors* (dashboards,
  automations, the companion apps): the
  lab ran headless, driven by API. The
  frontend was served and its states
  proven; no screen was arranged, and
  the guide contains no screenshots —
  real or otherwise.
- *Restore from backup:* creation and
  inspection are verified (t05); the
  restore itself replaces the running
  configuration, and the lab kept its
  one verified instance intact for the
  API proof rather than spend it.
  Chapter 7 names this as the first
  test a reader should run on a
  sacrificial install.
- *Remote access:* none was configured
  or opened; chapter 8's ranking is the
  project's and common practice's
  account.
- *The neighbouring systems of
  chapter 10:* described from their own
  projects' public documentation; none
  installed.
- *Voice (Assist) beyond the dependency
  chain:* the conversation machinery's
  libraries were installed to clear the
  demo's setup; no voice interaction
  was attempted or is claimed.

Specimen discipline, for the record: the
Maple Street house, its street, and its
owner are invented; the map pin is a
round-number coordinate chosen for the
sun calculations, not anyone's address;
the lab's one secret (the onboarding
password) was generated for the lab,
never used elsewhere, and is not
recorded. No command in this guide was
aimed at any system outside the lab
directory and its one server process.

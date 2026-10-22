# Troubleshooting

**Scope:** failures in the order you're
likely to meet them, each as symptom →
cause → fix. Items the lab actually
produced cite their transcript; the rest
come from the project's documentation
and are worded as what they are.

## An integration fails to set up, naming a missing module

**Symptom:** the log shows `Setup failed
for '<integration>'` and, above it, a
`ModuleNotFoundError` for a Python module
you've never heard of — `mutagen`,
`haffmpeg`, `pymicro_vad` in the lab's
run.

**Cause:** on a Core install, the base
package does not carry every integration's
library requirements; some must be added
to the venv by the operator. (OS and
Container installs ship them, which is
why this failure is a Core accent.)

**Fix:** read the traceback to the module
name, install the package that provides
it into the *same venv*
(`./ha-venv/bin/pip install ...`), restart,
repeat if the next error names the next
module. The lab needed four rounds (t02,
t03). Mind the spelling traps: the PyPI
package for the `haffmpeg` module is
`ha-ffmpeg`.

## The checker is silent — is that success?

**Symptom:** `check_config` prints one
line and no verdict.

**Cause:** none — that *is* the verdict.
The checker prints the directory it
tested and speaks only when something is
wrong; its exit code (0) is the answer
(t01).

**Fix:** none needed. Automate on the
exit code, not on the output, and keep
the habit from chapter 3: no restart on
an unchecked config.

## A boot warning says your Python is deprecated

**Symptom:** `Support for the running
Python version 3.12.3 is deprecated and
will be removed in Home Assistant
2025.2` (t02).

**Cause:** the Python leash (chapters 2,
3): each HA release supports a moving
window of Python versions.

**Fix:** plan the Python upgrade before
the release that removes yours; on Core
this is your maintenance, on OS and
Container it is the image's problem.
Until then, the warning is information,
not an error — the system runs.

## The version you installed isn't the newest

**Symptom:** the project's site announces
2025.9; `hass --version` says 2025.1.4,
and pip insists you're up to date.

**Cause:** pip resolves to the newest
release *your Python can run*. Nothing
is broken and nothing warned you.

**Fix:** none, until you upgrade Python
(see above). On Core, "which HA do I
get?" is always downstream of "which
Python do I run?".

## Port already in use / the page won't load

**Symptom:** the server starts but the
browser can't reach it, or the log
complains the port is taken.

**Causes, in order:** another program
(possibly an older `hass` you forgot) on
8123; your `http: server_port` (the lab
chose 8124) not reflected in the URL you
typed; the server still in its slow
first boot (the lab's took 82 seconds —
wait, and watch the log for
`Home Assistant initialized`).

**Fix:** match URL to configured port,
find the squatter with your OS's socket
tools, and only then suspect the config.

## An automation never fires

**Symptom:** the rule exists, the trigger
happens, nothing.

**Causes, in the order to check them:**

1. **The condition is shut.** The most
   common cause and not a malfunction:
   the gate did its job (evening mode
   off, in the specimen's terms). The
   automation's **Traces** view (in the
   interface, documented-only here) shows
   each run and exactly where it stopped.
2. **The trigger isn't what you think.**
   A state trigger on `on` won't refire
   for `on → on`; sunset is a moment, not
   a state.
3. **The entity ID drifted.** Renamed in
   the interface, stale in the YAML.
   Developer tools → States is the census
   of what exists *now* (t04's API view
   of the same list).

**Fix:** prove each stage separately —
state in the census, condition true by
hand, action via Developer tools →
Services — which is the interface's form
of the API calls the lab made.

## Entities show `unavailable`

**Symptom:** a device's entities read
`unavailable` or freeze at a stale value.

**Cause:** the third layer problem of
chapter 4 — the integration is up, the
*device* is unreachable: out of radio
range, unplugged, its cloud having a bad
day (for cloud integrations), or its
battery dead at a sensor's pace.

**Fix:** at the device first (power,
range, the vendor's status page for
cloud gear), then the integration's
page, then the hub. Restarting the hub
is the last resort, not the first — it
fixes none of the causes above.

## The disk is full of yesterdays

**Symptom:** the configuration directory
grows; backups balloon; the machine
complains.

**Cause:** the recorder's history
(chapter 7) — every state change of
every sensor, kept by default for a
rolling window that chatty sensors make
heavy.

**Fix:** set retention with intent
(recorder purge settings), exclude the
chattiest entities from history, and
keep the backups off the box anyway —
a full disk and a lost hub are the same
afternoon otherwise.

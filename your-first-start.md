# Your First Start

**Scope:** starting Home Assistant Core for
real — the virtual environment, the
configuration directory and its one famous
file, the checker you run before every
restart, the first boot (including this
lab's honest failure), and onboarding.

## Install Core, exactly as the lab did

Chapter 2 explained the shapes; this is the
Core path, step by step. You need Python
3.12 or 3.13 (check `python3 --version`
first — the version decides which Home
Assistant you get, as chapter 2 warned).

```bash
mkdir home-assistant && cd home-assistant
python3 -m venv ha-venv
./ha-venv/bin/pip install homeassistant
./ha-venv/bin/hass --version
```

Check: the lab's last line printed

```
2025.1.4
```

(transcript t00) — the newest release its
Python 3.12 could run. Yours will differ;
what matters is that the number prints at
all, because everything after this rides
on that environment. Keep the venv: you
start, check, and upgrade from inside it.

## The configuration directory

Home Assistant keeps everything it is — its
settings, its database, its memory of your
house — in one **configuration directory**.
You choose where with `-c`:

```bash
./ha-venv/bin/hass -c maple-street
```

The directory is the installation, in a
sense: back it up and you have the house
(chapter 7). Inside it, the file you'll
meet first is **`configuration.yaml`** —
the front door of the configuration.
Modern Home Assistant does much of its
configuring in the web interface and
stores that in a hidden `.storage` folder,
but YAML is still where a Core install
begins, and where helpers, templates, and
hand-written automations classically live.

The lab's specimen configuration — the
invented Maple Street house — is kept
whole at `examples/configuration.yaml`.
Its bones:

```yaml
homeassistant:
  name: Maple Street
  latitude: 41.0
  longitude: -73.5
  time_zone: "America/New_York"

http:
  server_port: 8124

sun:
demo:

input_boolean:
  evening_mode:
    name: Evening mode
```

Three things to notice. The `homeassistant:`
block is identity and geography — the sun
integration needs the position to compute
sunrise and sunset, and costs nothing to
get right. The `http:` block moves the
server off its usual port, 8123 — the lab
did this so a specimen never collides with
a real install; you may never need it. And
each bare word — `sun:`, `demo:` — is an
integration being switched on with its
defaults. Much of YAML configuration is
exactly that terse.

## Check before you start: `check_config`

```bash
./ha-venv/bin/hass --script check_config -c maple-street
```

Check: on a good configuration the checker
is nearly silent —

```
Testing configuration at /home/hatch/workspace/home-assistant-build/maple-street
```

— and exits with code 0 (t01). Silence is
the success message; a bad file gets named
errors instead. Make this a habit with
teeth: **never restart a working system on
an unchecked configuration.** First boots
and checkers may also pause to install a
few small helper packages the first time —
you'll see `Attempting install of ...`
lines once, and then not again.

## First boot: the lab's honest failure

The lab's first real start took 82 seconds,
came up — and **failed to set up the demo
integration**. The log said why, in a chain
(t02):

```
Error during setup of component conversation
ModuleNotFoundError: No module named 'mutagen'
Setup failed for 'demo': Could not setup dependencies: conversation
```

What happened is a Core-install truth,
learned the real way: **the base install
does not carry every integration's
library requirements.** The demo leans on
the conversation machinery; conversation
leans on voice libraries; and several of
those libraries were simply absent. Home
Assistant OS and the container image ship
them baked in; the bare Python package
expects the operator to close the gap.
The fixes were one at a time, each found
by reading the next error (t03):

```bash
./ha-venv/bin/pip install mutagen
./ha-venv/bin/pip install ha-ffmpeg        # the module is 'haffmpeg'
./ha-venv/bin/pip install pymicro-vad pyspeex-noise
```

After the third restart the demo set up
cleanly, and the only remaining ERROR line
was a camera *performance* note about a
missing system library (libturbojpeg) —
worth reading, not worth fixing in a lab.
Two lessons generalize:

1. **The log is the manual for your
   installation.** Every failure above was
   self-describing. `home-assistant.log`
   in the configuration directory is the
   same record, kept.
2. **First boot is slow and later boots
   aren't** — the lab went from 82 seconds
   to about 2. Don't judge the program by
   its first morning.

The same boot also printed the warning
chapter 2 promised (t02):

```
Support for the running Python version 3.12.3 is deprecated
and will be removed in Home Assistant 2025.2;
Please upgrade Python to 3.13
```

The Python leash, in the program's own
words.

## Onboarding: the first five minutes

With the server up, visit it:

```
http://localhost:8124/
```

Check: a first-run server answers with a
redirect to its onboarding page (the lab
captured `302 Found → /onboarding.html`),
where you create the **owner account** —
the first user, who can do everything —
name the home, and confirm its location
and time zone. The lab did this step
through the API instead of the browser
(the calls are in t04), because the lab
had no browser; the screens you get ask
the same questions in friendlier form.
From the moment that account exists, the
server stops offering onboarding and
starts asking you to log in — which is the
security model arriving on schedule
(chapter 8).

Then the quiet anticlimax: an empty
dashboard, a discovered-devices list that
may already have entries if your network
is talkative, and — in the lab — 109
pretend entities from the demo, waiting
to be automated. Chapter 4 explains where
entities come from; chapter 5 puts them
to work.

Check: you should be able to stop your
server, edit `configuration.yaml`, run
`check_config`, and start again — and to
say what you'd read first if it didn't
come back. If so, you operate the thing
now; the rest is furniture.

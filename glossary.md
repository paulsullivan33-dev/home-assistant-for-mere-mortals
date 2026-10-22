# Glossary

**Scope:** the terms, collected in one
place. Chapter references point at the
fullest explanation.

**Action** — what an automation does when
its trigger fires and its conditions pass:
one or more service calls. Chapter 5.

**Add-on** — an extra program the
Supervisor can install and manage beside
Core (editor, broker, tools). Exists only
on the OS and Supervised shapes.
Chapter 2.

**Attributes** — the fine print beside an
entity's state: brightness beside `on`,
target temperature beside `heat`.
Chapter 1.

**Automation** — a rule of the form
trigger → condition → action, run by the
hub when the world changes. Chapter 5.

**Card** — the unit of dashboard layout:
one rendering of one or more entities —
a list, a graph, a dimmer. Chapter 6.

**Condition** — the gate an automation
checks at trigger time; if it fails, the
automation quietly does nothing.
Chapter 5.

**Configuration directory** — the folder
holding everything the installation is:
configuration, `.storage`, database,
backups. Chapter 3.

**`configuration.yaml`** — the front-door
settings file in the configuration
directory; where a Core install begins.
Chapter 3.

**Coordinator** — the USB radio (Zigbee,
Z-Wave) bridging a device mesh to the
hub. Chapter 4.

**Core** — two senses, kept apart by
context: the Home Assistant program
itself, and the install shape that is
*only* the program, in a Python venv.
Chapters 2, 3.

**Dashboard (Lovelace)** — the web
interface's arranged views, built of
cards. Named Lovelace in the project's
own vocabulary. Chapter 6.

**Device** — one physical or logical
thing an integration reports; becomes
several entities. Chapter 4.

**Entity** — anything the hub knows
about, with an ID (`domain.name`) and a
state. The atom of the whole system.
Chapter 1.

**Event** — a noticed change, posted to
the event bus; what automations listen
to. Chapter 1.

**Helper** — an entity that exists only
to hold a chosen state (`input_boolean`,
`input_number`, ...): the house's own
variables. Chapters 4, 5.

**Integration** — the software translator
for one system, brand, or protocol.
Chapter 4.

**IoT class** — an integration's declared
habit: local push, local polling, cloud
push, cloud polling. The line to read
before buying hardware. Chapter 4.

**Logbook / History** — the recorded
stream of past states; the house's
diary. Chapters 1, 8.

**Onboarding** — the first-run flow:
owner account, naming the home, placing
it on the map. Chapter 3.

**Scene** — a saved snapshot of entity
states, applied in one call. Chapter 5.

**Script** — a named sequence of actions,
run when called rather than when
triggered. Chapter 5.

**Service** — a verb the system can
perform on entities: `light.turn_on`,
`backup.create`. Chapter 5.

**State** — an entity's current value:
`on`, `21.4`, `home`. Chapter 1.

**Supervisor** — the management layer
above Core on the OS and Supervised
shapes: add-ons, whole-stack updates.
Chapter 2.

**Template** — a small live expression
(`{{ ... }}`) evaluated by the system;
also a family of entities defined by such
expressions, like the specimen's porch
light. Chapter 5.

**Trigger** — the happening an automation
waits for: an event, a time, a threshold
crossed. Chapter 5.

**Virtual environment (venv)** — a
private folder of Python libraries, so a
program's dependencies stay its own.
Chapter 3.

# Backups and Updates

**Scope:** the two chores that decide
whether your house survives its operator.
Backups — creating one is verified here;
restoring is described honestly as
documented-only — and updates, monthly
and occasionally rude, on a system whose
Python leash chapter 2 already named.

## What a backup is

A Home Assistant backup is an archive of
the configuration directory: your
`configuration.yaml` and friends, the
`.storage` the interface wrote, the
database of states — the house, as a
file. It is not an image of the machine;
restoring means installing Home
Assistant again and giving it the archive.

The lab made one for real, through the
API's `backup.create` service, and opened
the result (t05):

```
$ tar -tf backups/e853edc2.tar
./backup.json
homeassistant.tar.gz
```

A manifest (`backup.json`) and the house
itself, gzipped, inside a tar — small
enough, in the specimen's case, to be
20 KB of nothing much. Real houses with
real history databases are bigger; the
shape is the same. Creating backups on
the OS and Container shapes is the same
service with buttons in front of it, and
there is scheduling machinery — regular,
automatic backups — because a backup
system that depends on you remembering
is a hope, not a system.

## Restoring: documented-only, and why

This guide did not restore its backup,
and says so rather than implying it did.
A restore replaces the running
configuration and restarts into it; the
lab's programme was to keep its one
verified instance intact for the API
tests, and a restore test deserves its
own sacrificial install — the honest
recipe is: fresh install, restore during
onboarding, log in, find your entities
exactly as left. The project's
documentation walks that path; the
discipline that matters is upstream of
it:

- **A backup you haven't restored is a
  hypothesis.** Schedule the sacrificial
  test once, on a spare machine or VM,
  before you need it at midnight. This
  guide flags its own omission precisely
  so you don't copy it.
- **Keep copies off the box.** A backup
  on the same SD card that is wearing
  out (chapter 2) is a souvenir. Another
  machine, a cloud folder, a USB stick in
  a drawer — anywhere that isn't the
  thing being backed up.
- **Back up before updates.** The next
  section is why.

## Updates, and breaking changes

Home Assistant releases **monthly**
(2025.1, 2025.2, ...), and each release
notes carry a section no other project
titles quite so plainly: **Backward-
incompatible changes** — the things that
will break, renamed entities, retired
options, integrations whose setup moved.
Reading that section before updating is
the whole skill. The update itself, per
shape:

- **OS:** offered in the interface,
  applies the whole stack at once.
- **Container:** pull the new image,
  recreate the container; your config
  directory carries over.
- **Core:** `pip install --upgrade
  homeassistant` inside the venv — and
  here the leash from chapters 2 and 3
  tightens: a new release may demand a
  newer Python than your system has,
  making the "update" a Python project
  first. The lab's boot log warning —
  support for Python 3.12 ends at 2025.2 —
  is that day arriving on paper.

Honest framing, because update chapters
often lie by cheerfulness: most monthly
updates are uneventful. The tail risk is
real, though — an integration you rely on
changes shape — and it concentrates
exactly where your house is most custom.
The working posture:

1. Read the release notes' breaking
   section; search it for your
   integrations' names.
2. Back up (verified above; five
   minutes).
3. Update; then read the log's first
   minutes the way chapter 3 taught —
   the system will tell you what it
   couldn't set up, by name.
4. Check the two or three automations
   the house actually feels.

Skipping versions is allowed — nothing
forces monthly — but the breaking-change
sections accumulate, and the reading gets
longer, not shorter. Little and often is
the cheap path.

## The database, one paragraph of care

The state history lives in a database in
the configuration directory (SQLite by
default) that grows with every sensor
reading. The **recorder** settings govern
how much history is kept; a chatty house
can grow gigabytes of yesterdays. You do
not need to act on this today. You need
to know the knob exists before the disk
announces it for you — chapter 11's
troubleshooting starts there.

Check: you should be able to say what a
backup contains (the configuration
directory, archived), what it does not
(the operating system, the Python
environment), and the one test this
guide openly didn't run. Next: who else
can see and touch your house — privacy
and security.

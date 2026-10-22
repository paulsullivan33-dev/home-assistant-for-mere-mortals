# Dashboards

**Scope:** seeing and touching the house —
Lovelace, the dashboard system: what you
get before you arrange anything, the card
as the unit of layout, and an honest line
between what this guide verified (the
machinery exists and serves) and what it
couldn't (the visual editing, which needs
eyes and a browser the lab didn't have).

## The dashboard you already have

Before you design anything, Home Assistant
maintains an automatic **Overview**
dashboard: every entity it knows, grouped
by room and kind, each row a live control —
a light you can tap, a sensor you can
watch. It is not pretty and it is not
meant to be; it is the census. On the
lab's specimen house that census held 109
entities (t04), and every one of them was
reachable through the same interface the
dashboards use — the state machinery
underneath the pictures is the part this
guide verified.

Dashboards are views built from **cards**:
a card shows one entity, or a small group,
or a picture, a map, a graph of a sensor's
history, a row of buttons that run
scripts. You arrange cards in **views**
(tabs), and views into **dashboards**
(the specimen household might keep
"Downstairs," "Energy," and "Away").
Cards are typed: an *entities card* is a
tidy list; a *glance card* is a row of
icons; a *light card* gives one light a
proper dimmer. Learning dashboards is
learning which card flatters which entity.

## The honest level of this chapter

Here is what the lab can and cannot say,
stated the way `criteria.md` insists:

- **Verified:** the dashboard system
  (`lovelace`) set up as part of the
  server; the frontend itself was served
  by the lab's install (the onboarding
  redirect and the real frontend page,
  t03); and every state a card would draw
  was read live through the API. Cards
  are renderings of that same state —
  nothing behind them is different in
  kind from what chapter 5 drove.
- **Documented-only:** the visual editor —
  dragging cards, the pickers, the
  per-card options, themes, the phone
  app's layout — described here and in
  the recipes from the project's
  documentation. The lab ran headless;
  no screenshot in this guide is real,
  and none is faked either: there are no
  screenshots.

That is a smaller loss than it sounds.
Dashboard craft is mostly taste, and
taste transfers badly through text
anyway. What transfers is the model:
entities underneath, cards above, and
nothing on a dashboard that isn't an
entity or a view of one.

## Principles that survive contact

- **The dashboard is for the household,
  not the operator.** The screens worth
  building are the three glances a day
  the house actually gets: *is everything
  closed, what's the temperature doing,
  did the washer finish.* Your beautiful
  system-diagram dashboard will be opened
  by you, alone, twice.
- **Put controls where the state is
  doubted.** Doors, locks, garage, the
  stove-adjacent plug: things people
  check from bed get the top of the page.
- **History graphs answer the arguments.**
  "It never gets warm in here" versus two
  weeks of the hallway sensor — the graph
  card ends debates that memory starts.
- **A tablet on the wall is a commitment.**
  It wants power, updates, and a kiosk
  mode; the phone in the pocket is the
  dashboard most houses actually use. The
  companion apps (documented-only here)
  are also how phones become *sensors* —
  location, battery, next alarm — which
  feeds chapter 5's triggers. A phone in
  this system is both window and witness.

## YAML mode, a footnote

Dashboards, like automations, exist in
two forms: edited in the browser and
stored by the system, or written as YAML
files you control. YAML mode gives you
diffs and backups of your layout in the
same breath as your configuration, at
the price of editing blind. Most
households use the browser; most guides
quietly use YAML for the same reason this
one wrote its automations in text. Know
that the choice exists; you can move
later.

Check: you should be able to say what a
card *is* — a rendering of entities and
their states, nothing more — and why
that makes chapter 5's API census a kind
of dashboard already. Next chapter is
the unglamorous one that saves houses:
backups and updates.

# CoC heroes, guardians & pets — upgrade planner with live build timers

A single-page planner for Clash of Clans hero / guardian / pet upgrades. Open
`index.html` in a browser (or run the little server below).

## What it does

* **Real character art** for every hero, guardian and pet — icons live in
  `assets/icons/` (132×132 transparent PNG).
* **Cost + time of the next level** for everything you tick, with your current
  level and your Town Hall.
* **Hammer Jam switch** (Nov 1 08:00 → Nov 16 08:00 UTC 2026) that halves cost
  and time, and keeps the discount for upgrades *started* during the event.
* **Start real timers** — press ▸ on a queue row and the app stores the job,
  keeps counting in the background (localStorage + a 1 s tick), and the progress
  is right even if you close the tab and come back.
  * heroes and guardians use your builder count (5 / 6 / instant),
  * pets run one at a time in the Pet House, without a builder,
  * a guardian needs Town Hall 18, pets need the Pet House (TH14+) — those are
    the only Town Hall gates enforced.
* **5-minute warning** — a toast, a beep and (if you allow it) a desktop
  notification 5 minutes before an upgrade ends.
* **Your resources** — enter your Gold / Elixir / Dark Elixir / Gems and the app
  charges what you start, then shows *what is still needed*, *what you have* and
  *what is missing* per resource, plus one-after-another and all-at-once finish
  dates.
* **Demo fast-forward** (×60 / ×3600) so you can watch a countdown, the 5-minute
  warning and the completion without waiting days. It only affects timers you
  started, and it pauses on the 5-minute mark so the warning is never skipped.

## Run it

```bash
python3 -m http.server 8000 --bind 0.0.0.0   # then open http://localhost:8000/
```

The page is plain HTML/CSS/JS — no build step, no dependencies. Everything is
saved in `localStorage` under `coc-upgrade-calc-v4`; **Reset** clears it.

## Data & caveats

* Costs/times are the base values (no Gold Pass, Books, Hammers or potions).
* Guardians (Smasher, Longshot, Logger) share one cost/time table.
* Diggy is listed to level 10 only — the higher levels weren’t verifiable.
* Sources: cocwarbase.com (heroes), Clash of Clans Wiki, cocmap.com and
  coclayout.com (guardians and pets), checked Nov 7, 2026.
* All game art belongs to Supercell. The icons were cut from publicly available
  renders; `tools/make_icons.py` rebuilds them from `image-search/` (not
  committed — see `.gitignore`).
* Character icons are 132 px renders, so they are crisp as 40–50 px avatars but
  not as full-size illustrations.

## Files

| path | what |
| --- | --- |
| `index.html` | the whole app |
| `assets/icons/*.png` | real character icons |
| `tools/make_icons.py` | icon pipeline (white-background cut-out, centring, resize) |
| `tools/smoke.js` | jsdom smoke test: boot, start, builder/pet limits, completion, 5-minute warning, totals |

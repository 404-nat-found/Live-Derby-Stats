# Jam Tracker — Live Roller Derby Stats

A single-file, offline-friendly web app for tracking **WFTDA roller derby** games in real time.
One person scorekeeps on their device while coaches watch live stats on theirs.

No build step, no server, no dependencies to install — it's one HTML file you can open
directly or host anywhere static (e.g. GitHub Pages).

> Main app: **[`derby-live-stats.html`](derby-live-stats.html)**

---

## Features

**Fast one-person input (Live Jam tab)**
- Tap to set each team's jammer, up to 4 blockers, and the pivot.
- Type total points per team per jam (free text).
- One-tap penalties (`+P`) on any skater on the track; long-press / right-click to remove.
- Jam clock with start/stop/resume and automatic **time-to-lead** capture (plus manual override).
- Lead-jammer attribution and **star pass** ("pass the panty") tracking.
- Tap the track to mark **where each jammer broke the pack**; a jammer line and pivot line
  are drawn on the home straightaway for reference.
- Period 1 / Period 2 selector, **Clear game**, and **End game & export**.

**Coaching insights (Insights tab), updating live**
- Scoreboard summary, penalty tracker.
- Jammer exit heat maps for both teams.
- Jammer effectiveness (Lead %, avg time-to-lead, star passes, net/jam).
- Blocker effectiveness and best blocker pairings.
- Most effective packs, your packs vs. their packs, your jammers vs. their packs, and
  their packs vs. your jammers.
- Lead battle & timing, and star-pass impact.

**Setup**
- Team names/colors and rosters.
- **CSV roster import** per team (see format below) so you don't hand-enter 20 skaters.
- Export a full JSON backup or a jam-by-jam CSV; import a JSON backup.

**Multi-device live sync** — one scorekeeper broadcasts, any number of viewers watch read-only.

**Accessibility** — light grey theme with green/orange accents chosen for readable contrast.

---

## Quick start

**Option A — just open it.** Download `derby-live-stats.html` and open it in any modern
browser. Everything is saved automatically in that browser (via `localStorage`).

**Option B — host it (recommended for multi-device use).** Publish with GitHub Pages
(steps below), then open the hosted URL on each device. Hosting is what makes the
sync **invite link** work directly.

---

## CSV roster import format

On the Setup tab, each team has an **⬆ Import CSV** button. Provide two columns —
**name** and **number**. A header row is optional and the column order is auto-detected.

```csv
name,number
Bolt,7
Havoc,13
"Quakes, Jr.",22
```

`number,name` order also works, as do quoted names containing commas.

---

## Multi-device live sync

On the Setup tab, open **Connect a second device**:

1. **Scorekeeper:** tap *Generate* for a room code, then *Host (scorekeeper)*.
2. Share the **room code** (or the *Copy invite link* if you're hosting the page online).
3. **Viewers:** open the page, enter the code, tap *Join as viewer*. They see everything
   update live, read-only.

**How it works / limitations — please read:**
- Sync relays through a **free public MQTT broker** (`broker.emqx.io`) over WebSockets.
  No account or API key is required.
- **Internet is required on every device.** A venue with no Wi‑Fi/cell won't sync, and
  same‑building LAN‑only won't work either.
- **Each device needs the page open.** The invite *link* only resolves on another device
  if the app is hosted at a shared URL (e.g. GitHub Pages). If you're opening the local
  file, share the **room code** instead and open the file on each device.
- Because it's a public broker, **anyone who knows your room code could read the feed.**
  Codes are random to make guessing unlikely — fine for game stats, not for anything
  sensitive.

If you want a private relay and working invite links, host the page and/or switch the
sync backend to your own free Firebase/Supabase project.

---

## Data & privacy

- All game data lives in your browser's `localStorage`. Nothing is uploaded unless you
  turn on live sync (which relays game state through the public broker described above).
- Use **Export JSON** for a backup before switching devices or clearing browser data.

---

## Repository contents

| File | Description |
| --- | --- |
| `derby-live-stats.html` | The live stat-tracking app (this project). |
| `derby-tournament-planner.html` | A separate static tournament-planning page. |
| `index.html` | A small unrelated static page. |

---

## Deploy to GitHub Pages

1. Create a new repository on GitHub and push these files (see below).
2. In the repo, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to *Deploy from a branch*, choose your
   default branch (e.g. `main`) and the `/root` folder, then **Save**.
4. After it publishes, the app will be at:
   `https://<your-username>.github.io/<your-repo>/derby-live-stats.html`

> The repo's root URL will serve `index.html`. If you'd rather have the derby app load at
> the root, rename/replace `index.html` with the derby app (or set up a redirect) — but
> that will replace the current `index.html` page.

### Pushing for the first time

```bash
git init
git add .
git commit -m "Add Jam Tracker live derby stats app"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

---

## License

Released under the [MIT License](LICENSE). Update the copyright holder in `LICENSE` to your name.

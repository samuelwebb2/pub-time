# Pub Time 🍺

A little website that tells you how much **golden time** you've got tonight — the daylight drinking window between when you clock off and sunset over London (or wherever you happen to be).

## The story

This started as a joke. I wanted to see how much I could build from my phone on the train into work, using Claude, without ever opening a laptop. The answer turned out to be: a surprising amount.

Every change to this site has been made by editing files directly in the GitHub web editor from my phone and letting GitHub Pages redeploy. This repo has never been cloned to my laptop. It has never seen a build step, a bundler, or an `npm install`. I've happily kept it that way — the vibe-coded spirit is a feature, not a bug.

## How it works (the interesting bits)

### Serverless, in the truest sense

There is no server. None. The whole thing is a handful of static files — one HTML file, a bit of JavaScript, a couple of icons — served straight off GitHub Pages. There's no backend to run, nothing to pay for, nothing to patch, and nothing that can fall over at 2am.

### Everything happens in your browser

The core question — *how much golden time is left?* — is pure astronomy. Sunset times are worked out **client-side** using [SunCalc](https://github.com/mourner/suncalc), a tiny library that derives the sun's position from your latitude, longitude and the date. No API call, no key, no tracking. Your phone does the maths.

### It works offline

Because that calculation needs no network, the site is a Progressive Web App. A service worker caches the files on first visit, so you can add it to your home screen and it'll open and calculate sunset with no signal at all — handy in a tunnel on that same train. Only the optional extras need the internet: the weather, and finding nearby pubs.

### Sharing without a database

The share button doesn't upload anything. It encodes your chosen clock-off time into a URL like `?off=1730` and hands that to your phone's share sheet. When a mate opens the link, the page reads the time straight back out of the URL. State travels *in the link itself* — no database required.

### Free, keyless APIs only

Where the site does reach out, it only uses services that need no account and no key: [Open-Meteo](https://open-meteo.com/) for the weather, and the [OpenStreetMap Overpass API](https://overpass-api.de/) for the nearest pubs. Both are queried directly from the browser. That's what keeps the whole thing deployable by literally dropping files into a GitHub repo.

## The stack, such as it is

- Plain HTML, CSS and JavaScript. No framework.
- SunCalc for sunset maths, bundled locally so it works offline.
- Open-Meteo for current conditions.
- Overpass / OpenStreetMap for nearby pubs.
- A service worker and web app manifest for the offline, installable bits.
- Hosted on GitHub Pages. Edited on a phone. Never cloned.

## Running it yourself

Fork the repo, enable GitHub Pages (Settings, then Pages, deploy from `main`, root folder) and that's it. Tweak the default clock-off time or the location fallback in `index.html` if you fancy.

---

*Built on a train, on a phone, for the important business of working out whether there's time for a pint.*

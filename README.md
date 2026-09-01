# Dispensary Ready — ATU Pharmacy Technician Study App

A standalone, gamified study app covering **Pharmacy Practice & Dispensary Computers** for ATU Pharmacy Technician students. 199 questions across 16 topics, built from your lecture material and checked against current PSI/HSE guidance.

## What's inside

- `index.html` — the entire app (HTML/CSS/JS, no build step, no backend)
- `data/topics.json` — topic list (name, icon, source file)
- `data/*.json` — one file per topic, each an array of question cards

## Updating content later

Each card looks like this:

```json
{
  "id": "reg-07",
  "type": "mc",
  "question": "Since March 2024, a prescriber can issue certain long-term prescriptions valid for up to:",
  "options": ["3 months", "6 months", "9 months", "12 months"],
  "answer": "12 months",
  "explanation": "Since March 2024, prescribers can issue prescriptions for certain long-term medicines with total validity of up to 12 months...",
  "hook": "optional memory hook — omit this field if not needed"
}
```

- `type` is `"mc"` (multiple choice — needs an `options` array including the correct answer) or `"typed"` (free text — no `options` needed).
- To add a topic: create a new `data/yourtopic.json` file in the same shape, then add an entry to the `topics` array in `data/topics.json` with a unique `id`, a `name`, an `icon` (any emoji), and `file` pointing at your new JSON file. No changes to `index.html` are needed.
- To edit/add/remove individual questions: just edit the relevant topic's JSON array directly. Keep `id` values unique within a file — that's what spaced-repetition progress is tracked against, so changing an `id` resets that card's progress.

## Deploying to GitHub Pages

1. Create a new repository on GitHub (e.g. `dispensary-ready`).
2. Upload the contents of this folder (`index.html` and the `data/` folder) to the repository root — either via the GitHub web UI ("Add file → Upload files") or:
   ```bash
   git init
   git add .
   git commit -m "Initial version of Dispensary Ready"
   git branch -M main
   git remote add origin https://github.com/YOUR-USERNAME/dispensary-ready.git
   git push -u origin main
   ```
3. In the repo, go to **Settings → Pages**.
4. Under "Build and deployment", set **Source** to "Deploy from a branch", branch `main`, folder `/ (root)`. Save.
5. GitHub will give you a live URL, typically `https://YOUR-USERNAME.github.io/dispensary-ready/`. It can take a minute or two to go live after the first push.
6. Any time you edit a JSON file and push to `main`, the live site updates automatically within a minute or so.

## How it works for students

- No login. Progress (spaced-repetition boxes, streak, mastery %) is stored only in that device's browser (`localStorage`), so it's private and free.
- **Quiz mode**: multiple-choice or typed questions depending on the card, with instant feedback, explanation, and an optional memory hook.
- **Flashcard mode**: tap to flip, then self-grade Again / Hard / Good / Easy — this feeds the same spaced-repetition engine as quiz mode.
- **Leitner spaced repetition**: 5 boxes. Wrong answers (or "Again") drop a card back to Box 1 so it resurfaces almost immediately; correct answers promote it, spacing it out further each time (8 hrs → 1 day → 3 days → 7 days).
- **Mastery %** is computed live from the actual box distribution of the currently-enabled topic pool, and labelled with a Dreyfus tier (Novice → Advanced Beginner → Competent → Proficient → Expert → Master).
- **Topics screen**: per-topic on/off toggles plus "All on / All off", so a student can focus a session (e.g. just Controlled Drugs before a placement) — disabled topics drop out of the due-card pool and the mastery calculation.
- **Streak**: increments once per calendar day a session is completed; resets if a day is missed.
- **Reset progress**: in Settings, with a confirmation step, in case a student wants to start fresh.

## A note on currency of content

This content was built from your slide decks in **September 2026** and cross-checked against current PSI/HSE sources at that time. One correction was made during that check: the **Common Conditions Service**, described in the source material as "planned for early 2025," has since launched — the app's Reimbursement Schemes topic reflects its live status (8 conditions, PSI Rules S.I. No. 507/2025, phased rollout through 31 March 2026). Pharmacy law and reimbursement thresholds change reasonably often (e.g. DPS caps, prescription extension rules) — worth a periodic re-check against PSI/HSE guidance before each academic year.

## Branding

Colours and type pairing are drawn from the ATU Brand Guidelines (Mar '26): ATU Navy (`#001a79`), Orange (`#ff791e`), Light Blue (`#7bb9cb`) and Green (`#005b5e`). The app references Halyard/Dashiell (ATU's licensed typefaces) by name in CSS with system-font fallbacks, since those fonts aren't freely licensable for a public web page — if your institution has web-font licences for Halyard, add `@font-face` rules at the top of the `<style>` block and the app will pick them up automatically.

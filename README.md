# Advanced Environmental Science — ENVS 601

A graduate course site: six chapters across twelve weeks, built as dependency-free HTML.
No build step, no framework, no package manager. Every page opens in a browser on its own.

**Live site:** `https://<your-username>.github.io/<repo-name>/`

---

## What's in here

| Path | What it is |
|---|---|
| `index.html` | Course hub. Renders a card per chapter and checks which chapter files exist. |
| `syllabus.html` | Full syllabus — outcomes, subtopics per session, calendar, grading, policies, references. |
| `chapters/` | Where your chapter pages go. Empty until you add them. |
| `templates/` | Starter pages to copy when writing a new chapter. |
| `.nojekyll` | Tells GitHub Pages to serve the files as-is. |

## The six chapters

| Chapter | Weeks | Files it looks for |
|---|---|---|
| 1 · Overview of Environmental Science | 1–2 | `Chapter01.html`, `Chapter01_Exercises.html` |
| 2 · Earth Systems and GIS | 3–4 | `Chapter02.html`, `Chapter02_Exercises.html` |
| 3 · Biogeochemistry and Ecosystem Ecology | 5–6 | `Chapter03.html`, `Chapter03_Exercises.html` |
| 4 · Atmospheric Chemistry | 7–8 | `Chapter04.html`, `Chapter04_Exercises.html` |
| 5 · EIA and Risk Analysis | 9–10 | `Chapter05.html`, `Chapter05_Exercises.html` |
| 6 · Ecosystem Dynamics and Resilience | 11–12 | `Chapter06.html`, `Chapter06_Exercises.html` |

---

## Putting it on GitHub Pages

1. Create a new repository on GitHub. Public is simplest — Pages is free on public repos.
2. Upload every file and folder in this package, keeping the structure. On the web you can
   drag the whole folder onto the **Add file → Upload files** screen.
3. Go to **Settings → Pages**. Under *Build and deployment*, set **Source** to
   *Deploy from a branch*, branch **main**, folder **/ (root)**. Save.
4. Wait a minute, then open `https://<your-username>.github.io/<repo-name>/`.

With Git instead of the web uploader:

```bash
git init
git add .
git commit -m "Course site: syllabus and hub"
git branch -M main
git remote add origin https://github.com/<your-username>/<repo-name>.git
git push -u origin main
```

## Adding a chapter

1. Copy `templates/ChapterTemplate.html` to `chapters/Chapter01.html` and
   `templates/ChapterTemplate_Exercises.html` to `chapters/Chapter01_Exercises.html`.
2. Replace the placeholder text. Both templates already carry the navy-and-gold styling,
   the callout boxes, figure and table styles, and a working self-check quiz.
3. Fix the two-digit number in the page title and in the cross-links at the bottom.
4. Commit and push. The card on the hub turns green on the next page load.

Chapter files are found in the repo root, in `chapters/`, or in `modules/` — all three are
checked, so it doesn't matter which you use as long as the filename matches.

## Changing the course structure

Everything the hub renders comes from the `CHAPTERS` array near the bottom of `index.html`:

```js
{num:"01", icon:"🌱", title:"Overview of Environmental Science", weeks:"Weeks 1–2",
 desc:"One-line summary shown on the card.",
 s1:{t:"First session subtitle", l:["subtopic", "subtopic"]},
 s2:{t:"Second session subtitle", l:["subtopic", "subtopic"]}}
```

Edit, reorder, or add entries and the cards regenerate — week numbers on the cards are
derived from position, so reordering renumbers automatically. Add `lec:"..."` or
`exo:"..."` to any entry to point at a different filename, which is how you'd split a
chapter into two separate weekly files.

The syllabus is plain HTML rather than generated. Each chapter is one `<article class="chap">`
block; edit the subtopic lists directly.

## Local preview

File detection uses `fetch`, which browsers block on `file://` URLs. Opened straight from
disk the cards fall back to a neutral "Open" state and every link still works — but to see
the green and red statuses, serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Printing

`syllabus.html` has print styles: use the browser's Print → Save as PDF for a clean
handout. Chapter pages print too, minus the navigation.

## Colours

| | Hex | Use |
|---|---|---|
| Navy | `#0E2A47` | Headers, dark panels, primary text accents |
| Navy mid | `#164272` | Links, secondary fills |
| Navy soft | `#DCE5F0` | Badges, secondary buttons |
| Gold | `#C9A227` | Section markers, primary buttons |
| Gold pale | `#F7EDC9` | Callouts, eyebrow tags |

Set once as CSS custom properties at the top of each file — change them there and the whole
page follows.

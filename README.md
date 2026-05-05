# Cornell MPH Biostatistics Website
**Courses:** VTPEH 6105 · VTPEH 6270  
**Live site:** https://bridgecology.github.io/Cornell-VTPEH6105-6270/  
**Built with:** [Quarto](https://quarto.org) · Hosted on GitHub Pages

---

## How the site works

You edit plain text files (`.qmd`) on your computer, run one command to render them into HTML, then push to GitHub. The live site updates automatically within a minute or two.

The three tools you need:
- **Quarto** — converts your `.qmd` files into the website ([download here](https://quarto.org/docs/get-started/))
- **Git** — tracks changes and syncs with GitHub (already set up on your machine)
- **Notepad** (or any text editor) — to edit the files

---

## Folder structure

```
env-course-website/
│
├── index.qmd                  ← Site home page (lists both courses)
├── _quarto.yml                ← Site settings: title, sidebar, navigation
├── styles.css                 ← Visual styling
│
├── 6105/
│   ├── index.qmd              ← VTPEH 6105 course landing page
│   └── syllabus.qmd           ← Combined syllabus + schedule + links  ← you'll edit this most
│
├── 6270/
│   └── 6270/
│       ├── index.qmd          ← VTPEH 6270 overview
│       └── 6270/
│           ├── assignments.qmd
│           └── workshops.qmd
│
├── Lecture/                   ← Slide PDFs (one per week)
├── Workshops/                 ← Workshop PDFs and HTML files
└── files/
    └── VTPEH 6105 - Syllabus.pdf
```

---

## The most common updates

### 1. Update the weekly schedule (dates, topics)

Open `6105\syllabus.qmd` in any text editor. The schedule is a Markdown table — each row is one week:

```
| 1  | Jan 23 | Course Overview | [Slides](...) | [Workshop 01](...)  |
| 2  | Jan 30 | Inference       | [Slides](...) | [Workshop 02](...)  |
```

Change the date or topic text directly. Don't touch the parts inside `(...)` unless you're also changing the file.

**After editing, always run:**
```cmd
quarto render
git add .
git commit -m "Update schedule"
git push origin main
```

---

### 2. Add or replace a lecture slide PDF

1. Name your new PDF following the existing pattern:
   ```
   VTPEH6105 - Lecture 03 - Inference & Hypothesis Testing.pdf
   ```
2. Drop it into the `Lecture\` folder (replacing the old file if updating).
3. If it's a **new** lecture (different filename), also update the link in `6105\syllabus.qmd`. Find the right row and update the filename inside the `[Slides](...)` link. Spaces become `%20` in links, `&` becomes `%26`.
4. Render and push:
   ```cmd
   quarto render
   git add .
   git commit -m "Update lecture slides week X"
   git push origin main
   ```

---

### 3. Add or replace a workshop file

1. Drop the new PDF or HTML into the correct subfolder inside `Workshops\`.
2. If the filename changed, update the link in `6105\syllabus.qmd` in the Workshop column of the relevant row.
3. Render and push (same three commands as above).

---

### 4. Update the syllabus PDF

1. Replace the file at `files\VTPEH 6105 - Syllabus.pdf` with your new version (keep the same filename).
2. No need to edit any `.qmd` files — the link already points there.
3. Push (no render needed for a PDF-only change):
   ```cmd
   git add files
   git commit -m "Update syllabus PDF"
   git push origin main
   ```

---

### 5. Update the grading breakdown

Open `6105\syllabus.qmd`. Near the top you'll find:

```markdown
| Component     | Weight |
|---------------|--------|
| Homework      | 40%    |
| Project       | 40%    |
| Participation | 20%    |
```

Edit the percentages directly, then render and push.

---

### 6. Change the course description or welcome text

- **Site home page** (both courses): edit `index.qmd` at the repo root.
- **VTPEH 6105 description**: edit `6105\index.qmd`.
- **VTPEH 6270 description**: edit `6270\6270\index.qmd`.

Then render and push.

---

### 7. Add a brand new page to the sidebar

1. Create a new `.qmd` file in the right folder, e.g. `6105\resources.qmd`.
2. Add a title at the top:
   ```
   ---
   title: "Resources"
   ---
   ```
3. Write your content below in plain Markdown.
4. Register it in `_quarto.yml` under the right sidebar section:
   ```yaml
   - text: "Resources"
     href: 6105/resources.qmd
   ```
5. Render and push.

---

## The three commands you'll use every time

Open Command Prompt (`cmd`) in your repo folder (`C:\Submission\4th Sem\env-course-website`), then:

```cmd
quarto render
git add .
git commit -m "describe what you changed"
git push origin main
```

The site updates on GitHub Pages within 1–2 minutes after the push.

---

## Troubleshooting

| Problem | Likely cause | Fix |
|---|---|---|
| `git push` rejected | Remote has changes you don't have locally | Run `git pull origin main --rebase` first, then push again |
| Link shows 404 | Filename doesn't match exactly (spaces, capitalisation) | Check the filename in Explorer and make sure spaces are `%20` in the link |
| Page looks old after push | Browser cache | Hard refresh with **Ctrl+Shift+R** |
| `quarto` not recognised | Quarto not installed or not on PATH | Reinstall from quarto.org, restart Command Prompt |
| Changes not showing on live site | `docs/` wasn't re-rendered | Always run `quarto render` before `git add` |

---

## Need help?

The site source is at: https://github.com/BRIDGEcology/Cornell-VTPEH6105-6270  
Quarto documentation: https://quarto.org/docs/websites/

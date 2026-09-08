# Personal CV site

A two-page static site: a CV home page and a projects detail page. Plain HTML and CSS,
no build step, no JavaScript. Built from an "Industry" design system export from Claude Design.

```
index.html          CV home page
projects.html       All projects, six entries
assets/styles.css   Design system — colors, type, components. Don't edit casually.
assets/site.css     Page layout and responsive rules. Edit this for layout changes.
assets/portrait.svg Placeholder portrait — replace with your photo
.nojekyll           Tells GitHub Pages to serve files as-is
```

## Publish on GitHub Pages

1. Create a repository. To get the address `https://<username>.github.io`, name it
   exactly `<username>.github.io`. Any other name gives you
   `https://<username>.github.io/<repo>/`, which also works fine.
2. Push these files to the repository root (not inside a subfolder):
   ```
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```
3. In the repository, go to **Settings → Pages**. Under "Build and deployment", set
   Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Save.
4. Wait a minute or two, then load the URL shown on that page.

To preview locally before pushing, run `python3 -m http.server` in this folder and open
`http://localhost:8000`. Opening `index.html` directly from the file system also works.

## What to change

All the current text is placeholder — the name, employers, numbers, project names and
talks are invented. Everything worth changing is plain text in the two HTML files.

**Your name and title** — search `index.html` for `Kováč`. It appears in the nav brand,
the hero heading, the page `<title>`, and the footer line. Also in the nav of
`projects.html`.

**Contact links** — near the bottom of `index.html`, in the dark section: the `mailto:`
address, GitHub and LinkedIn URLs.

**The CV PDF** — three buttons point at `assets/cv.pdf`, which doesn't exist yet. Drop
your PDF in at that path, or change the `href` on each. If you don't want a downloadable
CV, delete those three links.

**The portrait** — replace `assets/portrait.svg` with your photo and update the `src` in
`index.html` to match (`assets/portrait.jpg`). Use a 4:5 crop. The photo is deliberately
washed in the accent blue by the `.duotone` wrapper; remove that class from the `<figure>`
if you want the photo in its own colors. To drop the portrait entirely, delete the whole
`<figure class="blueprint duotone hero-portrait">` block.

**Experience** — each role is one `<div class="xp-row">`. Copy or delete whole blocks.
Keep them newest first.

**Projects** — each project lives in two places: a card in the `card-grid` on `index.html`
and a full `<article>` on `projects.html`. Their ids (`#p1` through `#p6`) tie them
together, and the index strip at the top of `projects.html` links to the same ids. If you
add or remove a project, update all three.

**Stats, stack, talks** — straightforward blocks in `index.html`. To remove a section,
delete the whole `<section>` including its `section-head`.

## Design notes

Colors, fonts, spacing and the component classes come from `assets/styles.css`. Change the
look by editing the variables at the top of that file — the accent color, for example, is
`--color-accent`, and it recolors buttons, rules, numerals and the duotone photo treatment
at once. Avoid hard-coding hex values or font names anywhere else.

The look is deliberate: square corners, hairline borders, no fills on cards, and the `+`
registration marks at each corner (the four `<i class="corner">` elements you'll see
inside cards and buttons). Don't drop those marks when copying a block, and don't round
the corners — the primary button's solid accent fill is the one filled object in the system.

Fonts (Barlow and Barlow Condensed) load from Google Fonts. To make the site fully
self-contained, download them and replace the `@import` at the top of `styles.css`.

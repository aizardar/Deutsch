# Deutsche Grammatik — Referenz

A single-page German grammar reference for learners at A1–B2. All the tables you
actually look up — cases, articles, adjective endings, pronouns, prepositions,
tenses, word order — on one page, with search.

**No build step, no dependencies.** The whole site is one `index.html` file.

## Contents

| Grundlagen | Verben | Sätze | Praxis |
|---|---|---|---|
| Die vier Fälle | Präsens & Konjugation | Satzbau & Wortstellung | Zahlen, Zeit & Datum |
| Artikel & ein-Wörter | Modalverben | Konjunktionen | |
| Pronomen | Trennbare Verben | Verben mit Präposition | |
| Adjektivendungen | Vergangenheit | | |
| Nomen: Genus & Plural | Unregelmäßige Verben | | |
| Präpositionen | Imperativ | | |
| | Konjunktiv II | | |
| | Passiv | | |

## Features

- **Search** — press `/` anywhere to filter every table by keyword
- **Dark mode** — follows your system setting, toggle to override (remembered)
- **Mobile** — sidebar collapses to a drawer; tables scroll horizontally
- **Print-friendly** — `Ctrl/⌘ + P` gives a clean printable reference

## Viewing it locally

Just open the file:

```bash
open index.html          # macOS
xdg-open index.html      # Linux
```

Or serve it:

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

## Publishing with GitHub Pages

1. Go to **Settings → Pages** in this repository
2. Under *Build and deployment*, set **Source** to `Deploy from a branch`
3. Choose the branch and the `/ (root)` folder, then **Save**
4. The site appears at `https://<username>.github.io/Deutsch/` after a minute

The `.nojekyll` file tells Pages to serve the HTML as-is without Jekyll processing.

## Editing

Everything lives in `index.html`. Each topic is a `<section>` with a `data-title`
(used for the sidebar link) and a `data-group` (used for the sidebar heading).
Inside, each `<div class="card">` is one lookup unit — the search filters at the
card level, so add a new card and it becomes searchable automatically.

```html
<section id="my-topic" data-title="Mein Thema" data-group="Grundlagen">
  <h2>Mein Thema <span class="de">Untertitel</span></h2>
  <div class="card">
    <h3>Eine Tabelle</h3>
    <div class="tw"><table>…</table></div>
    <p class="tip">Ein Hinweis.</p>
  </div>
</section>
```

Useful classes: `.tip` (gold note), `.warn` (red note), `.ex` (example line,
`<em>` inside highlights), `.chips` (word pills), `.pill` (inline tag),
`b.hl` (accent), `.mono` (code style).

## Note

Compiled as a learning aid, not an authoritative grammar. For edge cases, check
[Duden](https://www.duden.de) or [canoonet/Grammis](https://grammis.ids-mannheim.de).

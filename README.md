# Deutsche Grammatik — Referenz

A German grammar **lookup reference** for A1–B2. Every table you actually need —
cases, articles, adjective endings, pronouns, prepositions, tenses, word order —
one click or one search away.

It is a reference, not a course: there is no lesson order, no progress tracking,
nothing between you and the table.

**No build step, no dependencies.** The whole site is one `index.html` file.

## Contents

19 topics, 62 tables:

| Grundlagen | Verben | Sätze | Praxis |
|---|---|---|---|
| Die vier Fälle | Präsens & Konjugation | Satzbau & Wortstellung | Zahlen, Zeit & Datum |
| Artikel & ein-Wörter | Modalverben | TeKaMoLo | |
| Pronomen | Trennbare Verben | Konjunktionen | |
| Adjektivendungen | Vergangenheit | Verben mit Präposition | |
| Nomen: Genus & Plural | Unregelmäßige Verben | | |
| Präpositionen | Imperativ | | |
| | Konjunktiv II | | |
| | Passiv | | |

Zahlen/Zeit/Datum and TeKaMoLo carry English glosses under every rule; the other
sections are still German-only.

## Features

- **Front page is the index** — all 62 tables listed by name under their topic,
  each a direct link
- **Search reads table contents**, not just headings — press `/` or `⌘K`, type
  `halb drei` or `wegen`, and land on the exact table with the match highlighted
- **Deep links to a single table** — `#/adjektive/2` opens the mixed-declension
  table and flashes it
- **Alle Tabellen** — one button renders everything on a single page, so
  `Ctrl/⌘ + F` and printing work across the whole reference
- **Dark mode** — follows your system setting, toggle to override (remembered)
- **Mobile** — tables scroll horizontally inside their own container

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

## How it is put together

`index.html` holds three things: the styles, the content, and a small router.

All topic content sits in `<div class="hidden-store">` as one `<div class="tbody"
id="t-…">` per topic. The router clones the requested one into the page. The
topic list — titles, groups, subtitles, table names — is the `TOPICS` array in
the script, and the search index is built from the DOM at load.

To **add a table** to an existing topic, drop another `<div class="card">` into
that topic's `tbody`, then add its `<h3>` text to the matching `heads` array in
`TOPICS` so it appears in the index and the sidebar:

```html
<div class="card">
  <h3>Eine neue Tabelle</h3>
  <div class="tw"><table>…</table></div>
  <p class="tip">Ein Hinweis. <span class="en">An English note.</span></p>
</div>
```

To **add a whole topic**, add a `tbody` div and a matching entry in `TOPICS`
with `id`, `title`, `group`, `sub`, `icon`, `tables` and `heads`.

Search picks up new cards automatically — it indexes their full text.

Useful classes: `.tip` (gold note), `.warn` (red note), `.ex` (example line,
`<em>` inside highlights), `.en` (muted English gloss beneath a German line),
`.chips` (word pills), `.pill` (inline tag), `b.hl` (accent), `.mono` (code
style), and `.tk` with `.te/.ka/.mo/.lo` for TeKaMoLo colour tags.

Two gotchas worth knowing:

- `.tw` wrappers use `overflow-x:auto`, which makes them scroll containers.
  Sticky table headers anchor to the wrapper rather than the page, so they are
  deliberately not used.
- Links from the old one-page version (`#kasus`) redirect to the new form
  (`#/kasus`).

## Note

Compiled as a learning aid, not an authoritative grammar. For edge cases, check
[Duden](https://www.duden.de) or [canoonet/Grammis](https://grammis.ids-mannheim.de).

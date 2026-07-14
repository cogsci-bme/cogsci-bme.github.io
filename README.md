# ktt.ttk.bme.hu — Kognitív Tudományi Tanszék honlapja

A BME Kognitív Tudományi Tanszék (TTK) statikus honlapja, [Jekyll](https://jekyllrb.com/)
alapon, GitHub Pages-en hosztolva. Build és telepítés automatikus: a `main`
ágra pusholt módosítások néhány percen belül élesednek.

## Mit hol találsz

| Mappa / fájl            | Mire való |
|-------------------------|-----------|
| `_config.yml`           | Site-szintű beállítások (név, elérhetőség, domain). |
| `index.html`            | Kezdőlap: hero + hírfolyam. |
| `_posts/`               | **Hírek.** Egy hír = egy fájl. Lásd `_posts/README.md`. |
| `_layouts/`             | Oldalsablonok (`default`, `page`, `post`). |
| `style.css`             | A teljes oldal stíluslapja (a flyer-ekből általánosítva). |
| `kogtud.md`, `pszichologia.md` | Mesterszakok bemutató oldalai. |
| `kapcsolat.md`          | Kapcsolat oldal. |
| `naptar.md`             | **Naptár.** Beágyazott Google Naptár. Lásd `naptar.README.md`. |
| `_labs/`                | **Kutatócsoportok.** Egy labor = egy fájl. Lásd `labs.README.md`. |
| `dokumentumtar.md` + `dokumentumtar/` | Hallgatói letöltések (lásd `dokumentumtar/README.md`). |
| `CNAME`                 | Az egyéni domain (`ktt.ttk.bme.hu`). |

Ha `git push` közben hibaüzenetet kapsz, lásd [`git.README.md`](git.README.md).

## Hír közzététele

Lásd a részletes, magyar nyelvű útmutatót: [`_posts/README.md`](_posts/README.md).
Röviden: másold le a `_posts/2026-06-21-pelda-hir.md` fájlt, nevezd át
`ÉÉÉÉ-HH-NN-rovid-cim.md` formára, írd át a tartalmát, és commitold.

## Naptár

A **Naptár** menüpont egy beágyazott Google Naptárt mutat. Az eseményeket
közvetlenül a Google Naptárban szerkeszd — az oldal automatikusan frissül,
nem kell commitolni. Új naptár hozzáadásához vagy a megjelenés állításához
lásd a részletes útmutatót: [`naptar.README.md`](naptar.README.md).

## Kutatócsoportok (labor-oldalak)

Minden kutatócsoport egy fájl a `_labs/` mappában, `/kutatocsoportok/...`
címen. Egyszerű, karbantartható sablon: bemutatkozás + munkatársak + válogatott
publikációk (a teljes lista helyett Scholar/MTMT-link). Akinek saját honlapja
van, annak elég a Kutatás oldalról odalinkelni. Részletek:
[`labs.README.md`](labs.README.md).

## Új oldal készítése

Hozz létre egy `.md` fájlt a gyökérben ilyen fejléccel (front matter):

```markdown
---
layout: page
title: Az oldal címe
permalink: /url-resze/
---

A tartalom Markdownban…
```

A `page` sablon opcionálisan kér egy `hero: true`, `eyebrow:` és `lead:`
mezőt is, ha sávos fejlécet szeretnél az oldal tetején.

## Helyi előnézet (fejlesztőknek)

```sh
bundle install
bundle exec jekyll serve
# http://localhost:4000
```

## Stílus / arculat

A színek a `style.css` tetején, a `:root` blokkban állíthatók
(`--brand-deep`, `--brand-bright`). Jelenleg BME-kék. A pontos arculati
értékekre cserélendők, amint rendelkezésre állnak.

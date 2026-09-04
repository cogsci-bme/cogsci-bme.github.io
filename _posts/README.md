# Hírek írása (`_posts` mappa)

Ez a mappa tartalmazza a kezdőlapon megjelenő **híreket**. Minden hír egy
külön Markdown (`.md`) fájl. A legújabb hír kerül legfelülre, automatikusan.

Nincs külön „fontos időpontok" lista: határidőket, eseményeket és híreket
egyaránt ide, ebbe az egy idővonalba tegyünk.

## Új hír 3 lépésben

1. Nyisd meg a `_posts/2026-06-21-pelda-hir.md` fájlt, és másold le
   (GitHub weben: nyisd meg, „Copy raw contents", majd hozz létre új fájlt).
2. A fájl nevét **pontosan** így add meg: `ÉÉÉÉ-HH-NN-rovid-cim.md`
3. Írd át a `title:` mezőt és a szöveget, **töröld ki a `published: false`
   sort**, majd commitold.

> **A `published: false` sorra figyelj.** A minta hírben azért van benne, hogy
> maga a minta ne jelenjen meg az oldalon. Ha a másolatodban bennemarad, a te
> híred sem fog megjelenni — se a kezdőlapon, se máshol, hibaüzenet nélkül.
> Ha felraktál egy hírt és nem látszik, először ezt a sort keresd.

Néhány perc múlva a hír megjelenik a `https://ktt.ttk.bme.hu` kezdőlapon.

## Fájlnév-szabályok (FONTOS)

A fájlnevet a rendszer értelmezi, ezért kötött a formája:

```
ÉÉÉÉ-HH-NN-a-cim-kotojelekkel.md
```

- `ÉÉÉÉ-HH-NN` a megjelenés dátuma, pl. `2026-09-01`. **Ez adja a hír dátumát.**
- Utána kötőjel, majd egy rövid, kötőjelekkel tagolt azonosító.
- **Csak ékezet nélküli kisbetű, szám és kötőjel.** Ne legyen benne szóköz,
  ékezet (á, é, ő…) vagy írásjel a fájlnévben — a cím ékezetes lehet, csak a
  fájlnév nem.

Helyes példák:

```
2026-09-01-tanevkezdes.md
2026-12-01-diplomamunka-hatarido.md
2027-02-14-nyilt-nap.md
```

Hibás példák:

```
2026-9-1-hír.md          (egyjegyű hónap/nap, ékezet a névben)
2026-09-01 tanevkezdes.md (szóköz a névben)
tanevkezdes.md            (hiányzik a dátum)
```

## A fájl felépítése

Minden fájl két részből áll. Felül a „front matter" (két `---` sor között)
a beállításokkal, alatta a hír szövege Markdownban. A részletes, soronként
kommentezett mintát lásd a `2026-06-21-pelda-hir.md` fájlban.

```markdown
---
layout: post
title: A hír címe ide jön
---

A hír első bekezdése. Ez jelenik meg a kezdőlapon előnézetként is,
ezért legyen önmagában is érthető összefoglaló.

A többi bekezdés tetszőleges hosszú lehet.
```

## Képek és csatolmányok

- Képeket az `images/` mappába tölts fel, és így hivatkozz rájuk a szövegben:
  `![Leírás]({{ site.baseurl }}/images/fajlnev.jpg)`
- PDF-eket, dokumentumokat a `dokumentumtar/` mappa megfelelő almappájába
  tölts fel, és sima linkkel hivatkozz rájuk:
  `[A dokumentum neve]({{ site.baseurl }}/dokumentumtar/master_pszi/Felvi/fajlnev.pdf)`

## Közzétételi folyamat

Eldöntendő (a csapat döntése): a hírek **közvetlen push**-sal jelenjenek-e
meg, vagy **pull requesten** át, ellenőrzés után. Pull request esetén egy
második szerkesztő átnézi a hírt, mielőtt élesedik. Ez attól függ, hogy az oldalnak adminisztrátora (owner) vagy kontribútora (member) vagy -- ha felraksz egy hírt, és nem jelenik meg pár perc után az oldalon, akkor írj valamelyik adminisztrátornak (ld. [itt](https://github.com/orgs/cogsci-bme/people)).

> Ez a README nem jelenik meg a kész oldalon: a `_posts` mappában csak a
> `ÉÉÉÉ-HH-NN-` mintára illeszkedő fájlnevekből lesz hír, a többit a Jekyll
> figyelmen kívül hagyja. (A repó gyökerében lévő README-ket ezzel szemben
> külön ki kell zárni a `_config.yml` `exclude:` listáján.)

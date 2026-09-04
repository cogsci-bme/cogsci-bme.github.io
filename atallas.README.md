# Átállási teendők — mit csinálok, ha az IT így vagy úgy válaszol

Ez a fájl a `hosztolas.README.md` levél párja: ott az szerepel, mit kérünk az
IT-től, itt az, hogy a válaszuk után nekünk mi a dolgunk. Nem jelenik meg a
honlapon (a `_config.yml` `exclude:` listája kizárja).

Keresd meg lentebb azt a forgatókönyvet, amelyik az IT válaszára illik:

| Az IT válasza | Forgatókönyv |
|---|---|
| Beállítják a CNAME rekordot | [A](#a-forgatókönyv-cname-rekord) |
| CNAME-et nem, de A/AAAA rekordot igen | [B](#b-forgatókönyv-aaaaa-rekord) |
| Külső hosztolás nem engedélyezett, kapunk egyetemi szervert | [C](#c-forgatókönyv-egyetemi-szerver-lehívásos) |
| Egyetemi szerver, de ragaszkodnak a kiküldéses megoldáshoz | [D](#d-forgatókönyv-egyetemi-szerver-kiküldéses) |
| Nem válaszolnak | [E](#e-forgatókönyv-nincs-válasz) |

---

## Közös előkészítés (a levél elküldése előtt)

Egyetlen dolog van, amit a levél **elküldése előtt** el kell intézni, mert a
levélben szereplő `<token>` helyére kell:

1. GitHub → a `cogsci-bme` szervezet beállításai → **Pages** → *Verified
   domains* → **Add a domain** → `cogsci.bme.hu`.
2. A GitHub kiír egy TXT rekordot. A **nevét és az értékét** másold be a
   levélbe a `<token>` helyére.
3. A GitHub-oldali „Verify" gombot **még ne** nyomd meg, csak miután az IT
   visszajelzett, hogy a rekord él.

Ezen kívül töltsd ki a levél végén a `<Név>`, `<Beosztás>`, `<e-mail cím>`,
`<telefonszám>` mezőket.

---

## A forgatókönyv: CNAME rekord

Ez a legjobb kimenetel. Innentől kb. fél óra munka, plusz várakozás.

### 1. Ellenőrizd, hogy a DNS tényleg átállt

Ne a böngészőre hagyatkozz, mert az sokáig gyorsítótárazhat. Terminálban:

```sh
# CNAME rekord: a válaszban a cogsci-bme.github.io névnek kell szerepelnie
dig +short cogsci.bme.hu CNAME

# Domain-ellenőrző TXT rekord
dig +short _github-pages-challenge-cogsci-bme.cogsci.bme.hu TXT

# NINCS-e ottfelejtett A rekord (üres választ várunk a régi átirányítás IP-jére)
dig +short cogsci.bme.hu A
```

Ha az `A` lekérdezés még a régi webszerver IP-jét adja vissza, szólj az
IT-nek: a régi átirányítást nem törölték. Amíg ez fennáll, ne menj tovább.

### 2. Igazold a domaint a GitHubon

Vissza a szervezet Pages-beállításaihoz → **Verify**. Ha hibát ír, várj
fél órát (DNS-terjedés) és próbáld újra.

### 3. Állítsd be az egyéni domaint a tárolóban

Tároló → **Settings** → **Pages** → *Custom domain* → `cogsci.bme.hu` →
**Save**.

Ez a GitHub oldalán **létrehoz egy `CNAME` nevű fájlt** a tároló gyökerében,
és commitolja is. Ezért utána:

```sh
git pull                  # behúzza a GitHub által létrehozott CNAME fájlt
git rm CNAME.disabled     # a régi, kikapcsolt változat mehet
```

### 4. Írd át a `_config.yml`-t

A 13-19. sor környékén lévő TEMP blokk helyére:

```yaml
url: "https://cogsci.bme.hu"
baseurl: ""
```

A fölötte lévő, átmeneti állapotot magyarázó megjegyzést töröld ki, mert
onnantól félrevezető.

### 5. Javítsd a szövegbe égetett régi címet

Egy hírben szerepel a régi cím teljes URL-ként. Ezt kézzel kell javítani,
mert a `url:` átírása nem érinti:

- `_posts/2026-07-08-uj-szakiranyu-tovabbkepzes.md`, a bekezdés végén:
  `https://cogsci-bme.github.io/kvad/` helyett `{{ site.baseurl }}/kvad/`

Utána ellenőrizd, hogy nem maradt-e még ilyen:

```sh
grep -rn "cogsci-bme.github.io" --include="*.md" --include="*.html" . \
  | grep -v _site | grep -v hosztolas.README | grep -v atallas.README
```

Ennek a `_config.yml`-en kívül semmit nem szabad kiírnia.

### 6. Commitold és pushold

```sh
git add -A
git commit -m "Atallas a cogsci.bme.hu egyeni domainre"
git push
```

### 7. Kapcsold be a HTTPS-kényszerítést

Tároló → Settings → Pages → **Enforce HTTPS** pipa.

Ha a jelölőnégyzet szürke és nem kattintható, az **nem hiba**: a GitHub még
nem állította ki a tanúsítványt. Legfeljebb 24 óra, utána nézz vissza. Amíg
nincs bepipálva, a `http://` címen is elérhető az oldal, ami nem kívánatos,
úgyhogy erre a lépésre emlékezz vissza másnap.

### 8. Ellenőrzés

```sh
# 200-as választ és a helyes tanúsítványt várjuk
curl -I https://cogsci.bme.hu

# a http:// átirányít-e https://-re
curl -I http://cogsci.bme.hu

# egy mélyebb oldal és egy letölthető dokumentum
curl -I https://cogsci.bme.hu/kutatas/
curl -I https://cogsci.bme.hu/dokumentumtar/doktori/PDI_MSZ.pdf

# a sitemap már az új címet tartalmazza-e
curl -s https://cogsci.bme.hu/sitemap.xml | head -5
```

Böngészőben nézd meg a kezdőlapot, egy hírt, a Naptár és a Dokumentumtár
oldalt, és kattints rá egy PDF-re.

### 9. Zárás

- Szólj az IT-nek, hogy kész, és a TTL-t visszaállíthatják a szokásosra.
- A `README.md` 21. sorában a `CNAME` sor innentől pontos, nem kell javítani.
- A `_posts/README.md` és a `dokumentumtar/README.md` már eddig is a
  `cogsci.bme.hu` címet említette, tehát azok is helyessé váltak.

---

## B forgatókönyv: A/AAAA rekord

Ha az IT szabályzati okból nem tesz külső névre mutató CNAME-et, de
IP-címeket beállít. **Minden lépés ugyanaz, mint az A forgatókönyvben**,
kivéve az 1. pontot: ott CNAME helyett ezt ellenőrzöd:

```sh
dig +short cogsci.bme.hu A
dig +short cogsci.bme.hu AAAA
```

A GitHub Pages címei, amelyeket az IT-nek meg kell adni:

```
A     185.199.108.153
A     185.199.109.153
A     185.199.110.153
A     185.199.111.153

AAAA  2606:50c0:8000::153
AAAA  2606:50c0:8001::153
AAAA  2606:50c0:8002::153
AAAA  2606:50c0:8003::153
```

**Egy tennivalóval több:** ezek a címek, a CNAME-mel ellentétben, nem
követik automatikusan a GitHub esetleges változtatásait. Írd be a naptáradba
évente egyszer, hogy ellenőrzöd a GitHub aktuális dokumentációjában, és ha
változtak, újra kell kérned az IT-t. Ha nem ellenőrzöd, az oldal egy nap
csendben elérhetetlenné válik.

---

## C forgatókönyv: egyetemi szerver, lehívásos

Itt a szerkesztés marad a GitHubon, de a kiszolgálás egyetemi gépre kerül.
Ez lényegesen több munka, mint az A, és van benne két olyan lépés, amit
egyedül nem tudsz elvégezni.

### 0. Amit az IT-től még meg kell kapnod

Mielőtt bármit csinálsz, legyen meg írásban:

- a szerver neve és a kiszolgált könyvtár útvonala (pl. `/var/www/ktt`),
- ki hozza létre és tartja karban az időzített feladatot,
- megerősítés, hogy a szerverről engedélyezett a kimenő HTTPS a `github.com` felé,
- hogy a `cogsci.bme.hu` cím erre a szerverre fog mutatni.

### 1. Vedd ki a Gemfile-t a `.gitignore`-ból

**Ez blokkoló lépés.** A `.gitignore` 11-12. sora jelenleg kizárja a
`Gemfile` és `Gemfile.lock` fájlokat. Amíg ez így van, a GitHub Actions nem
tudja felépíteni az oldalt, mert nem tudja, milyen csomagok kellenek hozzá.

```sh
# töröld a Gemfile és Gemfile.lock sorokat a .gitignore-ból, majd:
git add -f Gemfile Gemfile.lock .gitignore
```

Mellékhaszon: ettől a `README.md`-ben leírt helyi előnézet (`bundle install`)
is működni fog egy friss klónból, ami eddig nem működött.

### 2. Hozd létre az építő munkafolyamatot

Új fájl: `.github/workflows/build.yml`

```yaml
name: Build and publish

on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      # A Ruby verziót a repóban lévő .ruby-version fájlból veszi.
      - uses: ruby/setup-ruby@v1
        with:
          bundler-cache: true

      - name: Build
        run: bundle exec jekyll build
        env:
          JEKYLL_ENV: production

      # A kész oldalt egy külön, eldobható 'deploy' ágra tesszük.
      # Az ág története szándékosan nem őrződik meg: minden build felülírja.
      - name: Push to deploy branch
        run: |
          cd _site
          git init -b deploy
          git config user.name "github-actions[bot]"
          git config user.email "github-actions[bot]@users.noreply.github.com"
          git add -A
          git commit -m "Build ${GITHUB_SHA}"
          git push --force \
            "https://x-access-token:${GH_TOKEN}@github.com/${GITHUB_REPOSITORY}.git" \
            deploy
        env:
          GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

Megjegyzés a megoldásról: szándékosan nem használunk külső, harmadik féltől
származó GitHub Action-t a közzétételre, csak sima `git` parancsokat. Kevesebb
függőség, és nem kell megbízni egy idegen action karbantartójában. Cserébe a
`deploy` ág története minden buildnél felülíródik; ez nem baj, mert a valódi
történet a `main` ágon van.

A tároló Settings → Actions → General alatt a *Workflow permissions* legyen
**Read and write**, különben a push nem megy át.

### 3. Írd át a `_config.yml`-t

```yaml
url: "https://cogsci.bme.hu"
baseurl: ""
```

És javítsd a szövegbe égetett régi címet, ugyanúgy, mint az A forgatókönyv
5. pontjában (`_posts/2026-07-08-uj-szakiranyu-tovabbkepzes.md`).

### 4. Commitold, pushold, ellenőrizd a buildet

```sh
git add -A
git commit -m "Build workflow az egyetemi szerverre valo tukrozeshez"
git push
```

A GitHub **Actions** fülén nézd meg, hogy lefutott-e. Utána a tároló
ágválasztójában meg kell jelennie a `deploy` ágnak, benne kész HTML-lel.
**Ne menj tovább, amíg ez nincs meg.**

### 5. Amit az IT-nek a szerveren be kell állítania

Küldd át nekik ezt a két parancsot.

Egyszeri klónozás a kiszolgált könyvtárba:

```sh
git clone --branch deploy --single-branch \
  https://github.com/cogsci-bme/cogsci-bme.github.io.git /var/www/ktt
```

Időzített frissítés (`crontab -e`), ötpercenként:

```sh
*/5 * * * * cd /var/www/ktt && /usr/bin/git fetch --quiet origin deploy && /usr/bin/git reset --hard --quiet origin/deploy
```

**Fontos, hogy miért `fetch` + `reset --hard`, és nem `git pull`:** a
munkafolyamat minden alkalommal felülírja a `deploy` ágat, így a `git pull`
előbb-utóbb hibára futna. A `reset --hard` mindig a legfrissebb változatot
állítja be, függetlenül az előzményektől.

### 6. Kapcsold ki a GitHub Pages-t

Settings → Pages → Source → **None**. Enélkül két helyen élne az oldal, két
különböző címen, és a keresők mindkettőt indexelnék.

Alternatíva, ha hasznosnak találod: hagyd bekapcsolva, és tekintsd a
`cogsci-bme.github.io` címet előnézetnek. Ebben az esetben viszont tegyél
`robots.txt`-t vagy `noindex`-et rá, hogy ne versenyezzen a hivatalos címmel
a találati listákon.

### 7. Ellenőrzés

Ugyanaz, mint az A forgatókönyv 8. pontja. Plusz: pusholj egy apró
módosítást, és nézd meg, hogy öt percen belül megjelenik-e az éles oldalon.
Ez az egyetlen igazi próbája annak, hogy a lánc működik.

### 8. Írd le a szerkesztőknek

A `README.md`-ben egy mondattal jelezd, hogy a módosítás most már nem
azonnal, hanem néhány percen belül jelenik meg, és hogy hibakeresésnél az
Actions fület kell először megnézni.

---

## D forgatókönyv: egyetemi szerver, kiküldéses

Csak akkor, ha a C valamiért nem járható. Az 1., 3., 4., 6., 7., 8. lépés
ugyanaz; a 2. és az 5. helyett:

### Kulcs létrehozása

```sh
ssh-keygen -t ed25519 -f deploy_key -N "" -C "github-actions-ktt"
```

- A `deploy_key.pub` tartalmát küldd az IT-nek, tegyék be a szerveren a
  megfelelő felhasználó `~/.ssh/authorized_keys` fájljába.
- A `deploy_key` (kiterjesztés nélküli, privát) fájl tartalmát tedd be a
  tárolóba: Settings → Secrets and variables → Actions → New secret, neve
  legyen `DEPLOY_KEY`.
- **A privát kulcsot ezután töröld a gépedről**, és soha ne commitold.

### A munkafolyamat közzétételi lépése

A C forgatókönyv `Push to deploy branch` lépése helyett:

```yaml
      - name: Deploy over rsync
        run: |
          mkdir -p ~/.ssh
          echo "${DEPLOY_KEY}" > ~/.ssh/id_ed25519
          chmod 600 ~/.ssh/id_ed25519
          ssh-keyscan -H "${SERVER_HOST}" >> ~/.ssh/known_hosts
          rsync -az --delete _site/ "${SERVER_USER}@${SERVER_HOST}:/var/www/ktt/"
        env:
          DEPLOY_KEY: ${{ secrets.DEPLOY_KEY }}
          SERVER_HOST: <szerver.ttk.bme.hu>
          SERVER_USER: <felhasznalonev>
```

Két figyelmeztetés:

- Az `rsync --delete` **törli** a célkönyvtárban azt, ami a forrásban nincs
  meg. Ha az IT bármi mást is tart abban a könyvtárban, az elveszik. Kérdezz
  rá, mielőtt először lefuttatod.
- Az `ssh-keyscan` vakon elfogadja a szerver kulcsát az első alkalommal.
  Biztonságosabb, ha az IT-től elkérted a szerver ujjlenyomatát, és azt
  rögzíted egy `KNOWN_HOSTS` secretben a `keyscan` helyett.

---

## E forgatókönyv: nincs válasz

Nem kell semmit tenni: az oldal a jelenlegi átirányítással működik tovább,
semmi nem romlik el. Két-három hét után érdemes rákérdezni, és ha akkor sem
jön válasz, a tanszékvezetőn keresztül újra felvetni. A levélben szereplő
kérés (két DNS rekord) az IT szemszögéből néhány perc munka, tehát ha
elakad, az szinte biztosan nem technikai okból akadt el.

---

## Visszaállítás, ha bármi elromlik

**A és B forgatókönyv.** Settings → Pages → Custom domain mező kiürítése.
Az oldal azonnal újra elérhető a `cogsci-bme.github.io` címen. A
`_config.yml`-ben állítsd vissza az `url:` értéket. Az IT-nek szólj, hogy
tegyék vissza a régi átirányítást. Ha a TTL alacsonyan maradt, ez percek
kérdése; ezért kértük az alacsony TTL-t.

**C és D forgatókönyv.** Settings → Pages → Source vissza `main` ágra, és
kérd az IT-t, hogy a `cogsci.bme.hu` mutasson újra a GitHub Pages-re (vagy
állítsák vissza az átirányítást). A tároló tartalma egyik esetben sem sérül,
a `deploy` ág és a munkafolyamat nyugodtan ottmaradhat kikapcsolva.

Egyik forgatókönyvben sem veszik el tartalom: a honlap forrása végig a
`main` ágon van, és ezen a folyamatok egyike sem változtat.

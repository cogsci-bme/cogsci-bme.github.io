# Levél az egyetemi IT-nek a honlap hosztolásáról

Ez a fájl egy elküldésre kész levéltervezet. Nem jelenik meg a honlapon
(a `_config.yml` `exclude:` listája kizárja). Küldés előtt töltsd ki a
`<...>` jelölésű helyeket.

---

**Tárgy:** A Kognitív Tudományi Tanszék honlapja — a `cogsci.bme.hu` cím
beállítása, illetve tükrözés egyetemi szerverre

Tisztelt Kollégák!

A BME TTK Kognitív Tudományi Tanszékének megújult honlapja ügyében keresünk
titeket. A jelenlegi helyzet és két lehetséges megoldás következik; a
kérdésünk a legvégén található.

## Jelenlegi helyzet

A tanszéki honlapot statikus oldalgenerátorral ([Jekyll](https://jekyllrb.com/))
készítjük, a forrása egy nyilvános Git-tárolóban van
(`https://github.com/cogsci-bme/cogsci-bme.github.io`). Az oldal jelenleg a
GitHub Pages szolgáltatásán érhető el, ezen a címen:

```
https://cogsci-bme.github.io
```

A hivatalos `cogsci.bme.hu` cím pillanatnyilag **átirányít** erre a címre.
Ez két okból nem szerencsés:

1. A látogató böngészőjének címsorában a `cogsci-bme.github.io` cím jelenik
   meg, ami egy hivatalos egyetemi tanszéki oldal esetében félrevezető.
2. A keresők és a hivatkozások is ezt a nem hivatalos címet rögzítik.

Szeretnénk, ha az oldal ténylegesen a `cogsci.bme.hu` címen szolgálna ki.
Erre két megoldást látunk. Az **1. változat** a lényegesen egyszerűbb, és
számunkra ez az elsődleges kérés; a **2. változatot** arra az esetre vázoljuk
fel, ha a külső hosztolás egyetemi szabályzatba ütközik.

## 1. változat: a `cogsci.bme.hu` cím a GitHub Pages-re mutat

Ebben a megoldásban az oldal továbbra is a GitHub Pages-en fut, de a
látogatók számára minden szempontból a `cogsci.bme.hu` címen érhető el.
Ehhez DNS-oldali beállításra van szükségünk tőletek.

Néhány megjegyzés, amelyek tapasztalataink szerint a beállítás során
kérdésként fel szoktak merülni:

- **A jelenlegi átirányítást meg kell szüntetni.** Ami most a
  `cogsci.bme.hu` nevet kiszolgálja (feltehetően egy webszerver-beállítás
  egy A rekord mögött), azt törölni kell. Egy hosztnévhez nem tartozhat
  egyszerre CNAME és A/AAAA rekord.
- **Az átállás napjára alacsony TTL-t kérnénk** (300 másodperc), utána
  visszaállítható a szokásos értékre. Így ha bármi gond adódik, gyorsan
  vissza tudunk állni.
- **Ha külső szolgáltatóra mutató CNAME rekord szabályzati okból nem
  engedélyezett**, alternatívaként A és AAAA rekordok is használhatók a
  GitHub Pages IP-címeire. A CNAME viszont megbízhatóbb: ha a GitHub
  megváltoztatja az IP-címeit, a CNAME automatikusan követi, míg a rögzített
  A rekordok észrevétlenül elavulnak. Ezért elsősorban a CNAME-et kérnénk.
- **A HTTPS-tanúsítványt a GitHub automatikusan kiállítja** (Let's Encrypt),
  ehhez tőletek nem kell semmi. A DNS-átállás után legfeljebb 24 órával lép
  életbe.
- A második, TXT rekord a domain tulajdonjogának igazolására szolgál. Ez
  akadályozza meg, hogy a hosztnevet később bárki más a saját GitHub-tárolójához
  rendelhesse. Nem kötelező, de biztonsági okból javasolt, és mivel szintén
  DNS-beavatkozás, célszerű egyszerre elvégezni az elsővel.

### Amit érdemes tudni a szolgáltatásról

A teljes kép kedvéért: a GitHub Pages a GitHub (Microsoft) szolgáltatása, a
kiszolgálás nem egyetemi infrastruktúrán történik. A látogatók IP-címei a
szolgáltató naplóiba kerülnek, ezekhez nekünk nincs hozzáférésünk, és a
szolgáltatás ingyenes szintjéhez nem tartozik adatfeldolgozói szerződés.
Az oldal maga nem használ analitikát és nem helyez el sütiket, a betűtípusokat
pedig szándékosan saját kiszolgálásban használjuk, hogy a betöltés ne
fedjen fel látogatói adatokat harmadik fél felé.

Ha ez így nem felel meg az egyetemi adatvédelmi vagy üzemeltetési
elvárásoknak, akkor a 2. változat jöhet szóba.

## 2. változat: tükrözés egyetemi szerverre

Ebben a megoldásban a honlapot **egyetemi szerver szolgálja ki**, a
szerkesztés viszont továbbra is a Git-tárolóban történik, és a kész oldal
automatikusan átkerül a szerverre. A szerkesztők munkamenete nem változik.

Két megvalósítási irányt látunk. Számunkra a firewall szempontjából
kedvezőbb az első.

### 2/a. Lehívásos megoldás (ezt javasoljuk)

A kész, legenerált HTML-oldal a Git-tárolóban egy külön ágra kerül. Az
egyetemi szerveren egy időzített feladat (cron) néhány percenként lefuttat
egy `git pull` parancsot, és ezzel frissül a kiszolgált tartalom.

Amire ehhez szükség van a szerveren:

- egy webkiszolgáló által kiszolgált könyvtár (pl. `/var/www/ktt`),
- `git` és `cron`,
- **kizárólag kimenő HTTPS-kapcsolat** a `github.com` felé.

Nincs szükség bejövő portnyitásra, nincs a szerverhez tartozó jelszó vagy
kulcs külső szolgáltatónál tárolva, és a szerveren nem kell semmilyen
oldalgeneráló szoftvert (Ruby, Jekyll) telepíteni és karbantartani, mert a
generálás a GitHub oldalán történik. A frissítés késleltetése az időzítés
gyakoriságától függ; öt perc bőven elegendő.

### 2/b. Kiküldéses megoldás

A másik lehetőség, hogy a GitHub `rsync`/SFTP segítségével közvetlenül
felmásolja a kész oldalt a szerverre. Ehhez viszont SSH-hozzáférés és
bejövő kapcsolat engedélyezése kellene a GitHub futtatókörnyezetének
IP-tartományaiból, ami igen széles és folyamatosan változó címtartomány.
Ezt csak akkor vetnénk fel, ha a 2/a valamiért nem járható.

### Kérdéseink a 2. változathoz

Ha ez az irány az elfogadható, a következőkben kérnénk a segítségeteket:

1. Van-e olyan egyetemi kiszolgáló, amelyen a fenti (2/a) feltételek
   teljesíthetők, és amelyen tanszéki statikus honlap elhelyezhető?
2. Ki tudná ezen a szerveren létrehozni és hosszú távon karbantartani a
   szükséges felhasználót és időzített feladatot?
3. Engedélyezett-e a szerverről a kimenő HTTPS-kapcsolat a `github.com` felé?
4. Ebben az esetben is a `cogsci.bme.hu` cím mutatna erre a szerverre,
   tehát a jelenlegi átirányítás itt is megszűnne.

## Összefoglalva, mit kérünk

- **Elsősorban:** a fenti két DNS-rekord beállítását (1. változat), és a
  jelenlegi átirányítás megszüntetését. Ez a mi oldalunkon néhány perc
  munka, és bármikor visszafordítható.
- **Ha az 1. változat szabályzati okból nem járható:** jelezzétek, és
  szívesen egyeztetünk a 2. változat részleteiről. Ebben az esetben az is
  segítene, ha megírnátok, pontosan melyik elvárásnak nem felel meg a külső
  hosztolás, mert ez befolyásolja, hogy melyik megoldás a megfelelő.

A honlap forrása nyilvános, bármikor megtekinthető a fenti GitHub-címen, és
szívesen bemutatjuk élőben is, ha az segít a döntésben.

Segítségeteket előre is köszönjük!

Üdvözlettel,

<Név>
<Beosztás>
BME TTK Kognitív Tudományi Tanszék
<e-mail cím> · <telefonszám>

# Git — mit tegyek, ha a push nem megy?

Ez a repó több szerkesztővel is bővül. Mivel mindenki a `main` ágon
dolgozik, előbb-utóbb mindenkivel megtörténik, hogy push közben hibaüzenetet
kap. A legtöbbször ez **nem jelent valódi problémát**, csak azt, hogy közben
más is pusholt. Az alábbi két eset fedi le a helyzetek nagy részét.

## 1. eset: a push elutasítva, de nincs valódi ütközés

Ez történik, ha **más fájlt** szerkesztettél, mint amit közben valaki más
módosított és pusholt (pl. te a `kutatas.md`-t írtad át, közben más a
`naptar.md`-t pusholta). Ilyenkor a hibaüzenet valami ilyesmi:

```
! [rejected]        main -> main (fetch first)
error: failed to push some refs to '...'
```

Ez azt jelenti: a `main` ág a szerveren előrébb jár, mint a te helyi
másolatod. Nincs ütközés, csak be kell húznod a közbeni változásokat:

```sh
git pull
git push
```

A `git pull` automatikusan összefésüli a két oldalt (mivel más fájlt
érintettetek), és utána a push simán lemegy. Ha a `git pull` egy
szerkesztőt nyit meg egy commit-üzenet miatt (merge commit), egyszerűen
mentsd el és zárd be (nem kell semmit átírnod benne).

## 2. eset: valódi ütközés (ugyanazt a fájlt szerkesztettétek)

Ez akkor fordul elő, ha ketten **ugyanabban a fájlban, ugyanazon a
részen** dolgoztatok egyszerre. Ilyenkor a `git pull` nem tudja magától
eldönteni, melyik verzió a jó, és ezt írja ki:

```
CONFLICT (content): Merge conflict in a.md
Automatic merge failed; fix conflicts and then commit the result.
```

Ez nem hiba, csak azt jelenti, hogy neked kell eldöntened, mi maradjon.

1. Nyisd meg az érintett fájlt (a hibaüzenet megmondja, melyiket). Az
   ütköző rész így néz ki benne:

   ```
   <<<<<<< HEAD
   Ez a te verziód.
   =======
   Ez a másik, közben pusholt verzió.
   >>>>>>> a1b2c3d (a másik commit üzenete)
   ```

2. Szerkeszd a szöveget úgy, ahogy véglegesen szerepeljen: tartsd meg az
   egyik verziót, a másikat, vagy fésüld össze a kettőt kézzel. Töröld ki
   a `<<<<<<<`, `=======` és `>>>>>>>` jelölő sorokat is — ezek csak a
   git jelölései, nem tartozhatnak a végleges szövegbe.
3. Mentsd el a fájlt, majd:

   ```sh
   git add a.md
   git commit
   git push
   ```

   (A `git commit` egy előre kitöltött "Merge branch..." üzenetet ajánl
   fel, azt simán elfogadhatod.)

Ha elakadsz, és vissza szeretnél állni a pull előtti állapotra (pl. mert
véletlenül elkezdted, de mégsem szeretnéd megcsinálni), ezzel meg lehet
szakítani:

```sh
git merge --abort
```

Ez visszaállítja a helyi állapotot pontosan olyanra, amilyen a `git pull`
előtt volt — semmi nem vész el.

## Hogyan előzhető meg

- **Pull, mielőtt nekiállsz szerkeszteni**: `git pull` a munka elején,
  még azelőtt, hogy bármit átírnál. Így ritkábban futsz bele a fentiekbe.
- **Kis, gyakori commitok**: ha valaki naponta többször pushol egy-egy
  kisebb módosítást ahelyett, hogy hetekig gyűjtené, kevesebb az esély
  ütközésre.
- Ha bizonytalan vagy egy adott helyzetben, és nem szeretnél kockáztatni:
  másold ki a saját, még nem mentett módosításaidat egy külön szövegfájlba,
  utána nyugodtan kísérletezhetsz a fentiekkel — a másolatból mindig
  visszaírhatod, amit esetleg elrontanál.

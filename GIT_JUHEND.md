# 9. seminar: Git merge-konflikti tekitamine ja lahendamine

**Esitada:** GitHubi repositooriumi link ja kuvatõmmis merge-konfliktist (Moodle'i ülesande lõpus nõutud).

**Eeltingimused:** Git on arvutisse paigaldatud ja seadistatud; GitHubi konto olemas; VS Code. Täida kõik käsud VS Code'i terminalis PowerShelli või Git Bashi abil, ükshaaval.

## 1. Loo GitHubi repositoorium

Ava https://github.com/new. Nimi: `marie-ilutuba`; Public; ära lisa GitHubi kaudu README-d. Ava allalaetud ZIP-ist lahtipakitud `marie-ilutuba` kaust VS Code'is ja sisesta:

```bash
git init
git branch -M main
git add .
git commit -m "Lisa Marie ilutoa veebileht"
git remote add origin https://github.com/KASUTAJANIMI/marie-ilutuba.git
git push -u origin main
```

Asenda `KASUTAJANIMI` enda GitHubi kasutajanimega.

## 2. Tee kaks klooni

Sama terminal on seni `marie-ilutuba` kaustas. Sisesta:

```bash
cd ..
git clone https://github.com/KASUTAJANIMI/marie-ilutuba.git tudeng1
git clone https://github.com/KASUTAJANIMI/marie-ilutuba.git tudeng2
```

## 3. Esimene tudeng

```bash
cd tudeng1
git checkout -b tudeng1
```

Ava VS Code'is `tudeng1` kaust. Failis `conflict.md` muuda *Valitud kujunduse värv: määramata.* kujule **Valitud kujunduse värv: roosa.** ja salvesta.

```bash
git add conflict.md
git commit -m "Tudeng 1 valis roosa varvi"
git push -u origin tudeng1
cd ..
```

## 4. Teine tudeng

```bash
cd tudeng2
git checkout -b tudeng2
```

Ava VS Code'is `tudeng2` kaust. Failis `conflict.md` muuda sama esialgne rida kujule **Valitud kujunduse värv: beež.** ja salvesta.

```bash
git add conflict.md
git commit -m "Tudeng 2 valis beezi varvi"
git push -u origin tudeng2
cd ..
```

## 5. Esimene tudeng ühendab haru

```bash
cd tudeng1
git checkout main
git merge tudeng1
git push origin main
cd ..
```

## 6. Teine tudeng proovib sama ja tekib konflikt

```bash
cd tudeng2
git checkout main
git pull origin main
git merge tudeng2
```

**Oodatud tulemus**: `CONFLICT (content): Merge conflict in conflict.md` ning `Automatic merge failed`. Ava `conflict.md`: peaksid nägema Git-konflikti markereid `<<<<<<< HEAD`, `=======`, `>>>>>>> tudeng2`.

**Tee sellel hetkel kuvatõmmis** (Windowsis `Win + Shift + S`), kus on näha terminal ja `conflict.md` konflikt. Ära lahenda konflikti enne kuvatõmmise tegemist!

## 7. Lahenda konflikt

Asenda `conflict.md` kogu sisu järgmisega:

```md
# Git merge-konflikti harjutus

Valitud kujunduse värv: roosa ja beež.
```

Salvesta ja käivita:

```bash
git add conflict.md
git commit -m "Lahenda merge konflikt"
git push origin main
git status
```

Kui näed `nothing to commit, working tree clean`, on kõik korras.

## 8. Esitamine

Kopeeri GitHubi repositooriumi link (näiteks `https://github.com/SINU-NIMI/marie-ilutuba`) Moodle'i seminaritöö vastusesse. Lisa samasse vastusesse tehtud kuvatõmmis merge-konfliktist.

**Küsimus 11. Miks tuleb merge-konflikte osata lahendada?**

Kui mitu arendajat muudavad sama faili samu ridu, ei saa Git alati automaatselt otsustada, milline muudatus alles jätta. Konflikti lahendamisel saavad arendajad muudatused teadlikult ühendada, säilitades vajaliku töö ja vältides vigu.

## Tüüpilised probleemid

- Kui `git` käsku ei tunta ära, paigalda Git for Windows ja ava VS Code uuesti.
- Kui `git commit` küsib nime ja meiliaadressi, seadista need `git config --global user.name "Sinu nimi"` ja `git config --global user.email "sinu-githubi-email"` abil.
- Kui `git push` vajab autentimist, logi GitHubi sisse avanud brauseriaknas.
- Kui `git merge tudeng2` **ei** tekita konflikti, kontrolli, et mõlemad tudengid muutsid `conflict.md` täpselt sama rida ja et tudeng 1 muudatus on juba `main` harusse push'itud.
- Veebilehe välised fotod, Google Fonts ja Google Maps vajavad internetiühendust. Õpetaja nõuetes on broneerimislehe sisu esialgu valikuline, seega on siin ainult ooteleht.

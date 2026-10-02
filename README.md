# Git + GitHub · hitri priročnik za delavnico

Predstavitev: [PREZENTACIJA_GIT_GITHUB.html](PREZENTACIJA_GIT_GITHUB.html) · Izziv: [izziv.md](izziv.md)

## 1. Pred prvo uporabo · nastavi Git

Git uporabniško ime in e-pošta sta podpis avtorja commitov; nista GitHub prijava. Uporabi ime ali vzdevek ter e-pošto, ki jo želiš povezati s svojim GitHub profilom.

```sh
git config --global user.name "Ime ali vzdevek"
git config --global user.email "tvoj-email@example.com"
git config --global --list
```

V Visual Studio Code odpri **Accounts → Sign in with GitHub** in prijavo potrdi v brskalniku. GitHub gesla ne vpisuj v Git ukaze, repo, commit ali chat. Git prek HTTPS uporablja varno prijavo/credential manager; GitHub account password ni način za Git push.

## 2. Kloniraj repozitorij in osveži `main`

Ukaze vnašaj v terminal VS Code brez znaka `$`.

```sh
git clone https://github.com/MatijaPI/git-github-delavnica.git
cd git-github-delavnica
git status
git pull --ff-only origin main
```

`clone` prenese repozitorij in nastavi povezavo `origin`. `pull` prenese nove spremembe v trenutno vejo; zato pred njim preveri `git status` in vejo. Po kloniranju preizkusi pull, ko je v `main` objavljena nova skupna sprememba.

## 3. Nagradna vaja · izziv

Odpri datoteko [izziv.md](izziv.md) v korenski mapi repozitorija. Rešitev vpiši neposredno v polje **Odgovor** v tej datoteki. Vsak dela na svoji veji. Ker vsi spreminjate isto polje, po tekmovanju združimo samo zmagovalni PR; ostale pregledamo in zapremo brez mergea, da ne pride do konflikta. Uporabi **unikaten vzdevek** samo z malimi angleškimi črkami, številkami in vezaji, npr. `ana-7`; v spodnjih ukazih zamenjaj `vzdevek` s svojim vzdevkom.

```sh
git switch main
git pull --ff-only origin main
git switch -c izziv/nlp-vzdevek
```

Odpri `izziv.md` v VS Code in v polje **Odgovor** zapiši rešitev. Ne spreminjaj drugih delov besedila.

Preglej in objavi samo svojo datoteko:

```sh
git status
git add izziv.md
git diff --staged
git commit -m "Rešitev roverjevega parkirnega izziva"
git push -u origin izziv/nlp-vzdevek
```

Na GitHubu izberi **Pull requests → New pull request**. Kot **base** izberi `main`, kot **compare** pa `izziv/nlp-vzdevek`. Preglej prikazani diff, vpiši naslov in kratek opis ter klikni **Create pull request**. Če po pregledu popraviš odgovor, committaj in pushaj na isto vejo:

```sh
git add izziv.md
git diff --staged
git commit -m "Popravek rešitve roverjevega izziva"
git push
```

PR se bo samodejno posodobil. Zmaga prvi pravilno rešen PR po času odprtja. Ekipa pregleda vse rešitve; združi se samo zmagovalni PR, ostale zapremo brez mergea, ker vsi spreminjajo isto vrstico.

## 4. Ukazi na kratko

| Ukaz | Pomen |
| --- | --- |
| `git status` | Pokaže trenutno vejo, spremenjene datoteke in kaj je pripravljeno za commit. |
| `git diff` | Pregleda spremembe spremljanih datotek, ki še niso v stagingu. |
| `git add <pot>` | Pripravi določeno datoteko za commit. Nove datoteke se pokažejo v `git diff --staged`. |
| `git diff --staged` | Pregleda točno vsebino naslednjega commita. |
| `git commit -m "Sporočilo"` | Shrani pripravljene spremembe v lokalno zgodovino. Commit še ni na GitHubu. |
| `git switch main` | Preklopi na lokalno vejo `main`. |
| `git pull --ff-only origin main` | Osveži `main`; se ustavi, če Git ne more varno zgolj premakniti veje naprej. |
| `git switch -c <ime-veje>` | Ustvari in izbere novo vejo iz trenutne veje. |
| `git checkout -b <ime-veje>` | Ustvari ali zamenja vejo iz trenutne veje. |
| `git push -u origin <ime-veje>` | Prvič objavi vejo na GitHubu in poveže lokalno vejo z oddaljeno. |
| `git push` | Pošlje nove commite trenutne povezane veje. |

Delovni ritem: `status → pull → switch -c → uredi → add → diff --staged → commit → push → PR`.

## Pravila za veje in varno delo

- Format veje: `tip/podsistem-kratka-naloga`, z malimi črkami in vezaji: `feature/drive-encoder-check`, `fix/imu-axis-sign`, `docs/power-pinout`.
- Za izziv uporabi `challenge/nlp-vzdevek`; vzdevek mora biti unikaten.
- `main` je skupna veja. Delo objavimo prek PR-ja, ne neposredno s push v `main`.
- Pred commitom preglej staging. Ne uporabljaj `git add .`, če nisi preveril vseh datotek.
- Ne committaj gesel, tokenov, ključev, osebnih ali občutljivih podatkov.
- Če push ne uspe ali se pojavi konflikt, ustavi se in preveri `git status`; ne uporabljaj `git push --force`, `reset` ali `restore` na slepo.

# Posmatrač

Tekstualna igra u kojoj si akreditovani posmatrač izbora u Srbiji. Kroz izborni dan, od dolaska na biračko mesto u 06:30 do slanja izveštaja u 22:15, rešavaš 21 situaciju i biraš kako posmatrač treba da reaguje.

Igra je par igri Kontrolor, u kojoj je igrač član biračkog odbora.

Posle svake odluke igra pokazuje da li je odluka ispravna, delimično ispravna ili pogrešna, zašto je tako i koje pravilo važi.

## Kako se igra

- Svaka situacija ima četiri opcije. Izabrana opcija se „zaokruži“ kao na glasačkom listiću.
- Tri merača prate tvoj rad: **nepristrasnost**, **beleške** i **odnos sa odborom**.
- Na kraju dobijaš izveštaj posmatrača sa svim odlukama, brojem ispravnih odluka i ocenom.
- Redosled opcija se meša u svakoj partiji.

Situacije obuhvataju, između ostalog: pravo na prisustvo pripremi, izbor mesta za posmatranje, ukazivanje odboru na propuste, odnos prema biračima, strankama i medijima, način beleženja, udaljavanje posmatrača, sumnju na kupovinu glasova, „bugarski voz“, deljenje podataka, praćenje brojanja, višak listića u kutiji, potpisivanje zapisnika i izveštaj organizaciji.

## Struktura projekta

```
index.html     cela aplikacija (HTML, CSS i JavaScript u jednom fajlu)
netlify.toml   podešavanja za Netlify (objava i bezbednosna zaglavlja)
CHANGELOG.md   spisak izmena po verzijama
README.md      ovaj fajl
```

Nema zavisnosti ni build koraka. Jedini spoljni resursi su fontovi sa Google Fonts (Bitter, Source Serif 4, IBM Plex Mono).

## Lokalno pokretanje

Otvori `index.html` direktno u pregledaču, ili pokreni lokalni server:

```sh
python3 -m http.server 8000
```

pa otvori http://localhost:8000.

## Objava na Netlify

**Preko Git repozitorijuma (preporučeno)**

1. Postavi projekat na GitHub, GitLab ili Bitbucket.
2. Na Netlify izaberi **Add new site → Import an existing project** i poveži repozitorijum.
3. Build command ostavi prazno, a publish directory je `.`. Ova podešavanja se čitaju iz `netlify.toml`.
4. Pokreni **Deploy**. Svaki novi push na glavnu granu automatski objavljuje novu verziju.

**Preko Netlify CLI**

```sh
npm install -g netlify-cli
netlify login
netlify deploy          # probna objava
netlify deploy --prod   # produkcija
```

**Bez naloga za Git:** prevuci folder projekta na https://app.netlify.com/drop.

## Izmena sadržaja

Sve situacije su u nizu `S` unutar `<script>` bloka u `index.html`. Svaka situacija ima ovaj oblik:

```js
{ t: "08:40",                       // vreme na satu
  title: "Komšija bez dokumenta",
  text: "Opis situacije…",
  opts: [
    { x: "Tekst opcije", v: "ok" },                 // ok | part | bad
    { x: "Tekst opcije", v: "bad", f: "Kratko objašnjenje zašto",
      fx: [-8, -10, -8] },                          // opciono: promena merača
    …
  ],
  why: "Pravilo koje se prikazuje posle odgovora." }
```

Ako opcija nema `fx`, koriste se podrazumevane promene merača iz objekta `DEF` (redom: nepristrasnost, beleške, odnos sa odborom). Ocene na kraju igre zavise od broja bodova i definisane su u funkciji `renderEnd`.

## Verzionisanje

Trenutna verzija je upisana na jednom mestu, u `index.html`:

```html
<meta name="version" content="1.0.0">
```

Broj verzije ima oblik `GLAVNI.SPOREDNI.ISPRAVKA`:

| Izmena | Primer | Nova verzija |
|---|---|---|
| Ispravka teksta, pravila ili greške u kodu | pogrešan rok u objašnjenju | 1.0.0 → 1.0.1 |
| Nove ili izmenjene situacije, nova funkcija | dodata situacija o glasanju van biračkog mesta | 1.0.1 → 1.1.0 |
| Veća promena igre ili usklađivanje sa novim zakonom | igra za lokalne izbore, novi sistem bodovanja | 1.1.0 → 2.0.0 |

Postupak za novu verziju:

1. Promeni `content` u `<meta name="version">`.
2. U `CHANGELOG.md` premesti stavke iz „Neobjavljeno“ pod novi naslov sa brojem verzije i datumom.
3. Napravi commit i Git tag, pa pošalji oba:

```sh
git commit -am "Verzija 1.0.1"
git tag -a v1.0.1 -m "Verzija 1.0.1"
git push && git push --tags
```

## Napomena o tačnosti

Igra je edukativna simulacija sa izmišljenim situacijama. Pravila su pojednostavljena prema Zakonu o izboru narodnih poslanika, uputstvima Republičke izborne komisije i uobičajenim pravilima ponašanja organizacija koje posmatraju izbore. Nisu pravni savet. Pravila o izjavama medijima, deljenju podataka i hitnom javljanju razlikuju se od organizacije do organizacije, a prava posmatrača (npr. prisustvo pripremi i upis primedbi u zapisnik) treba proveriti u važećem zakonu i uputstvu RIK pre korišćenja igre na obukama. Na stvarnim izborima uvek važe zakon i uputstvo tvoje organizacije.

# Izmene

Sve značajne izmene igre Posmatrač beleže se u ovom fajlu. Brojevi verzija prate pravila opisana u odeljku „Verzionisanje“ u README.md.

## [Neobjavljeno]

### Dodato
- Link „← Sve igre“ iznad zaglavlja, ka krovnoj aplikaciji Izborni dan (https://izborni-dan.netlify.app/).
- Ikonica u tabu pregledača (favicon): lupa sa kvačicom, ugrađena u `index.html` kao SVG.
- Slika za deljenje na društvenim mrežama (`og-image.png`, 1200 × 630) i Open Graph i Twitter meta tagovi.

### Promenjeno
- Slika za deljenje se u `og:image` i `twitter:image` navodi punom adresom (https://posmatrac.netlify.app/og-image.png), a dodat je i `og:url`.
- Meta opis stranice: „Akreditovani si posmatrač na biračkom mestu. Kroz 21 situaciju, od pripreme do izveštaja, odluči kada i kako da postupiš.“

## [1.0.0] - 2026-10-13

### Dodato
- Igra sa 21 situacijom tokom izbornog dana, iz uloge akreditovanog posmatrača, od dolaska na biračko mesto do slanja izveštaja.
- Tri merača: nepristrasnost, beleške i odnos sa odborom.
- Objašnjenje i pravilo posle svake odluke, izveštaj posmatrača i ocena na kraju igre.
- Mešanje redosleda opcija u svakoj partiji.
- Podešavanja za objavu na Netlify (`netlify.toml`) sa bezbednosnim zaglavljima.
- Oznaka verzije u `<meta name="version">`.

---
id: 004
tittel: Sett opp repo og publisering på GitHub Pages
rolle: utvikler
prioritet: høy
avhenger_av: []
kurator_kreves: false
---

## Hvorfor

Landingssiden ligger kun lokalt. Vi trenger en offentlig URL for å samle
e-postpåmeldinger via Tally, og for å kunne dele siden med testbrukere før
domenet er på plass.

## Hva

Publiser dagens `index.html` på GitHub Pages fra et offentlig repo, servert
på `<bruker>.github.io/<repo>` inntil domenet er registrert.

Merk: gratisplanen krever offentlig repo. Det er akseptabelt og ønsket for
dette prosjektet, men betyr at ingenting privat kan committes.

## Akseptansekriterier

- [x] `git init`, `.gitignore` og første commit med hele prosjektet inkludert `/board`
- [x] Repoet er offentlig
- [x] Pages aktivert, siden svarer på HTTPS på `github.io`-adressen
- [x] Hero-bildene (`bilder/hero.jpg`, `bilder/hero-mobil.jpg`) lastes korrekt,
      også på mobilbredde
- [x] Tally-embed (`LZ2Qjj`) laster og kan sendes inn fra den publiserte siden
- [x] Archivo fra Google Fonts laster uten blokkering
- [x] Ingen relative stier er brutt av at siden ligger i en undermappe
- [x] `README.md` i rota forklarer kort hva prosjektet er og at det er
      ikke-kommersielt

## Utenfor scope

Eget domene og DNS. Se oppgave 005.

## Logg

- 2026-09-09 PM: opprettet
- 2026-09-22 PM: eier prioriterte denne først. Fjernet duplikat i backlog.
  Status: git er allerede initialisert (commit `58db579`), ingen remote.
  Siden ligger i `site/`, ikke i rota. Pages fra branch støtter bare `/` eller
  `/docs`, så utvikler må løse det (f.eks. Pages via Actions). `gh` er ikke
  installert. Venter på at eier oppretter repo / oppgir GitHub-bruker.
- 2026-09-22 PM: eier opprettet tomt offentlig repo
  https://github.com/richardkarlsen/baksetet. Flyttet til doing, delegert til utvikler.
- 2026-09-22 utvikler: La til `.gitignore`, `README.md` og
  `.github/workflows/pages.yml` (kun offisielle actions/checkout,
  actions/configure-pages, actions/upload-pages-artifact, actions/deploy-pages;
  publiserer `site/` uendret). Byttet lokal branch til `main`, lagt til
  `origin` (https://github.com/richardkarlsen/baksetet.git), committet og
  pushet. Verifisert at stiene i `site/index.html` allerede er relative uten
  ledende skråstrek — ingen endring nødvendig der. Bekreftet at repoet er
  offentlig via API. Pages er ikke aktivert ennå (Settings → Pages → Source:
  GitHub Actions gjenstår, kun eier kan gjøre det) — se sammendrag til PM.
- 2026-09-22 PM: verifisert commit `bd72733`: workflow bruker kun offisielle
  actions og publiserer `site/`, README er OK, repoet er offentlig. Pages er ikke
  aktivert (404). Venter på at eier gjør klikket Settings → Pages → Source: GitHub Actions.
  Oppdaget: begge commits har jobb-e-post som forfatter, og den er
  nå offentlig. Spurt eier om det skal ryddes.
- 2026-09-22 PM: etter eiers godkjenning er forfatter-e-post byttet til privat
  adresse i hele historikken, og historikken er lagt ut på nytt (`fccb639`).
- 2026-09-22 PM: eier har aktivert Pages, workflow kjører grønt. Flyttet til review, sendt til tester.
- 2026-09-22 tester: Testet mot akseptansekriteriene, se rapport til PM. Alle
  kriterier oppfylt bortsett fra "kan sendes inn" (uklart — ikke testet reelt
  innsending, se anbefaling). Fant to funn utenfor oppgavens scope: (1)
  kritisk — demo-forhåndsvisningen av bilvelgeren i seksjonen "Kommer" viser
  oppdiktede, navngitte produkt-til-tillitsnivå-koblinger (f.eks. "Britax
  Römer Dualfix" → "Frarådes" med begrunnelse) som visuelt er identiske med
  ekte kompatibilitetsdata; (2) middels — de fire tillitsnivåfargene skiller
  seg for lite i lysstyrke/gråtone til å være tydelige i gråskala/for
  fargeblinde.
- 2026-09-22 PM: tester har godkjent 7 av 8 kriterier. Tally «kan sendes inn» er uklart
  fordi eier må sende inn én test selv. Står i review til det er gjort.
  Funn: 006 (kritisk, demodata), gråtonefunn lagt til 001, 007 (og:image).
- 2026-09-22 PM: eier sendte inn en test fra den publiserte siden. Den er registrert i Tally (innsending 1W5p9db, 22:32). Alle kriterier er oppfylt, flyttet til done.

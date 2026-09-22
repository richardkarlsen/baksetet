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

- [ ] `git init`, `.gitignore` og første commit med hele prosjektet inkludert `/board`
- [ ] Repoet er offentlig
- [ ] Pages aktivert, siden svarer på HTTPS på `github.io`-adressen
- [ ] Hero-bildene (`bilder/hero.jpg`, `bilder/hero-mobil.jpg`) lastes korrekt,
      også på mobilbredde
- [ ] Tally-embed (`LZ2Qjj`) laster og kan sendes inn fra den publiserte siden
- [ ] Archivo fra Google Fonts laster uten blokkering
- [ ] Ingen relative stier er brutt av at siden ligger i en undermappe
- [ ] `README.md` i rota forklarer kort hva prosjektet er og at det er
      ikke-kommersielt

## Utenfor scope

Eget domene og DNS. Se oppgave 005.

## Logg

- 2026-09-09 PM: opprettet

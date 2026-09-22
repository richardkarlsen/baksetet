---
id: 007
tittel: Absolutt URL for og:image
rolle: utvikler
prioritet: lav
avhenger_av: [005]
kurator_kreves: false
---

## Hvorfor

`og:image` er relativ (`bilder/hero.jpg`). Noen tjenester viser da ikke bildet
når lenken deles. Løses best når domenet er på plass.

## Akseptansekriterier

- [ ] `og:image` er absolutt URL på endelig domene
- [ ] Forhåndsvisningen ved deling viser bildet (sjekket i en debugger for deling)

## Logg

- 2026-09-22 PM: opprettet etter funn fra tester i 004.

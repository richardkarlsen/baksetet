---
id: 011
tittel: Implementer nye tokens og ikoner for tillitsnivåene på siden
rolle: utvikler
prioritet: høy
avhenger_av: [001]
kurator_kreves: true
---

## Hvorfor

001 er godkjent. Siden bruker fortsatt de gamle nivåfargene uten ikoner. De
kan ikke skilles i gråtone, og «Ikke testet» er den svakeste.

## Hva

Ta i bruk tokens, ikoner og anatomien for merkelappene fra
`board/done/001-designtokens-tillitsniva.md` (`## UX-leveranse`) i
`site/index.html`, også i demo-blokken. Juster `--dim` slik leveransen sier.

## Akseptansekriterier

- [ ] CSS-variablene fra 001 er brukt ordrett. Ingen improviserte farger.
- [ ] Hver merkelapp har riktig inline SVG-ikon. Bekreftet er en omriss-sirkel med hake, ALDRI fylt.
- [ ] Sannsynlig viser «Sannsynlig · utledet» i listen
- [ ] Ordet «utledet» blir aldri klippet eller kortet ned med «…» ved 360px bredde
- [ ] Haken finnes ikke noe annet sted på siden enn i Bekreftet. Unntak: logoen, som løses i 009.
- [ ] Tester har sett på en realistisk liste der de fleste radene er Ikke testet, i farger og i gråtone. Frarådes er fortsatt det første øyet fanger. Hvis ikke, går saken tilbake til UX (ringtykkelse).
- [ ] Kontrast for tekst ≥ 4,5:1 og for kanter ≥ 3:1 er kontrollert i ferdig side
- [ ] Mobil (~380px) fungerer, med tastaturfokus synlig
- [ ] Datakurator har godkjent

## Utenfor scope

Logoen (009). E-posttekst (010).

## Logg

- 2026-09-22 PM: opprettet etter at 001 ble godkjent. Kravene fra datakurator er tatt med.

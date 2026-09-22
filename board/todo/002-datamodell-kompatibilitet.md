---
id: 002
tittel: Datamodell for bil/sete-kompatibilitet
rolle: datakurator
prioritet: høy
avhenger_av: []
kurator_kreves: true
---

## Hvorfor

Vi skal inn med ~20 prioriterte biler og ~40 seter. Feil struktur nå betyr
manuell opprydding i hundrevis av rader senere.

## Hva

Definer skjema for bil, sete og kompatibilitetsrad, inkludert felt for
tillitsnivå, begrunnelse, kilde, dato og vurderer. Foreslå filformat
(JSON eller CSV) og mappestruktur.

## Akseptansekriterier

- [ ] Bil identifiseres med generasjon og årsintervall, ikke bare modellnavn
- [ ] Sete identifiseres med eksakt variant og installasjonsmetode
- [ ] Hver kompatibilitetsrad har nivå, begrunnelse, kilde, dato, vurderer
- [ ] Rad uten kilde og dato kan ikke være Bekreftet eller Frarådes
- [ ] Skjemaet takler at samme sete monteres på flere måter i samme bil
- [ ] Eksempel med minst tre utfylte rader

## Utenfor scope

Selve datainnsamlingen. Egen oppgave per bil.

## Logg

- 2026-09-08 PM: opprettet
- 2026-09-22 PM: føring fra datakurator (008): mål fra brukere kan ikke brukes før vi har
  en måleprotokoll og en kvalitetskontroll. Fram til da gir de ikke engang «Sannsynlig».
  Aldri «Bekreftet».

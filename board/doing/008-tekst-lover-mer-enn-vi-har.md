---
id: 008
tittel: Tekstene på landingssiden lover data og sikkerhet vi ikke har
rolle: ux
prioritet: høy
avhenger_av: []
kurator_kreves: true
---

## Hvorfor

Datakurator fant under 006 at flere tekster omtaler en database og åpne data
som om de finnes i dag. De lover også sikkerhet («slipper å gjette») og bruker
ja/nei-språk. Dette er en risiko for troverdigheten vår og strider mot
sikkerhetsprinsippet.

## Hva

Skriv om disse tekstene i `site/index.html`:
1. Hero (ca. linje 200): «kobler tallene mot hver bilstol som selges her. Så slipper du å gjette.»
2. Meta description (linje 7)
3. og:description (linje 9): «koblet mot hver bilstol solgt i Norge»
4. Stripen (linje 208–209): «Målt for hånd, bil for bil», «Åpne data, alle kan etterprøve»
5. Seksjonstittelen (linje 217–218): «få stolene som passer», «akkurat ditt baksete»
6. Påmeldingen (linje 266): mål fra brukere kan aldri gi mer enn «Sannsynlig»

## Akseptansekriterier

- [ ] Ingen tekst påstår at data, database eller åpne data finnes i dag
- [ ] Ingen tekst lover sikkerhet eller at brukeren «slipper å gjette»
- [ ] Ingen ja/nei-formuleringer om passform. De fire nivåene er ikke en ja/nei-vurdering.
- [ ] Bunnteksten «Vi erstatter ikke prøvemontering...» beholdes
- [ ] Datakurator har godkjent tekstene
- [ ] Mobil (~380px) fungerer

## Logg

- 2026-09-22 PM: opprettet etter funn fra datakurator i 006.
- 2026-09-22 PM: eier ba om å starte. Flyttet til doing, delegert til UX.

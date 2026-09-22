---
id: 006
tittel: Forhåndsvisningen viser oppdiktede vurderinger av ekte bil og ekte seter
rolle: datakurator
prioritet: høy
avhenger_av: []
kurator_kreves: true
---

## Hvorfor

Tester fant dette under 004 (alvorlighet: kritisk). Seksjonen «Kommer» i
`site/index.html` (ca. linje 221–256) viser Volvo XC90 2016 sammen med fire
navngitte, ekte seter med tillitsnivå. Blant annet står det «Britax Römer
Dualfix → Frarådes» med en teknisk begrunnelse. Ingen av disse vurderingene er
reelle, men de ser ut akkurat som ekte data. Siden er nå offentlig. En forelder
kan tro på dem, og en produsent kan med rette reagere på «Frarådes» uten kilde.

I tillegg står det i forklaringsteksten under at «Bekreftet betyr testet av
produsenten». Det stemmer ikke med definisjonen i CLAUDE.md (fysisk verifisert
i denne bilen, eller dokumentert av produsent).

## Hva

Datakurator avgjør hva forhåndsvisningen kan vise. Deretter skriver UX
teksten/markeringen, og utvikler implementerer. Hvilken retning vi velger
bestemmer eier (se logg).

## Akseptansekriterier

- [ ] Ingen ekte, navngitt kombinasjon av bil og sete vises med et tillitsnivå
      som ikke har en kilde i datagrunnlaget
- [ ] Hvis det fortsatt vises eksempler: de er entydig markert som oppdiktede
      eksempler, både med tekst og visuelt, og de vises aldri i samme
      presentasjon som ekte data
- [ ] Forklaringsteksten til tillitsnivåene samsvarer ordrett med definisjonene
      i CLAUDE.md, godkjent av datakurator
- [ ] Datakurator har godkjent endelig versjon før den går til review
- [ ] Mobil (~380px) fungerer

## Utenfor scope

Fargekodingen av nivåene (se 001).

## Logg

- 2026-09-22 PM: opprettet etter funn fra tester i 004. Spurt eier om retning.

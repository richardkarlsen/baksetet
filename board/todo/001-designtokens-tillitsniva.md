---
id: 001
tittel: Definer designtokens for de fire tillitsnivåene
rolle: ux
prioritet: høy
avhenger_av: []
kurator_kreves: true
---

## Hvorfor

Alt annet i produktet henger på at en forelder på tre sekunder ser forskjell
på Bekreftet og Sannsynlig. Uten faste tokens vil utvikler improvisere farger.

## Hva

Konkret tokensett for Bekreftet, Sannsynlig, Ikke testet og Frarådes:
farge, ikon/form, tekstetikett, og hvordan de ser ut i liste vs. detaljvisning.
Skal passe inn i den mørke koksgrå paletten uten å bli neon.

## Akseptansekriterier

- [ ] Hex-verdier oppgitt for bakgrunn, kant, tekst og ikon per nivå
- [ ] Alle fire skiller seg tydelig fra hverandre i gråtone
- [ ] Kontrast minst WCAG AA mot mørk bakgrunn
- [ ] Hvert nivå har form/ikon i tillegg til farge
- [ ] "Ikke testet" leses som nøytral, ikke som feil eller advarsel
- [ ] Levert som CSS-variabler utvikler kan lime rett inn

## Utenfor scope

Implementasjon i index.html. Egen oppgave.

## Logg

- 2026-09-08 PM: opprettet

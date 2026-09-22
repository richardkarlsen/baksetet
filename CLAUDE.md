# baksetet.no

Uavhengig, ikke-kommersiell norsk tjeneste som hjelper foreldre å finne ut
hvilke barneseter som passer i deres konkrete bil.

Ingen annonser. Ingen affiliate. Ingen sponsede plasseringer. Dette er ikke
forhandlingsbart og skal aldri foreslås av noen agent.

## Produktkjerne

Kompatibilitetsvurderinger bruker fire tillitsnivåer — aldri binært ja/nei:

| Nivå        | Betydning |
|-------------|-----------|
| Bekreftet   | Fysisk verifisert i akkurat denne bilen, eller dokumentert av produsent |
| Sannsynlig  | Utledet fra mål/plattformdeling. Ikke verifisert. Skal alltid merkes som utledet |
| Ikke testet | Vi vet ikke. Dette er et gyldig og viktig svar |
| Frarådes    | Kjent problem. Skal alltid ha begrunnelse og kilde |

"Ikke testet" skal aldri skjules, nedtones eller gjettes bort til "Sannsynlig".

## Sikkerhetsprinsipp

Feil kompatibilitetsdata kan skade et barn. Ved tvil: velg det mest
konservative nivået. En bruker som får "Ikke testet" er trygg. En bruker som
får feilaktig "Bekreftet" er det ikke.

## Teknisk

- Statisk nettsted. `index.html` er selvstendig, ingen byggesteg.
- Ingen eksterne avhengigheter utover Google Fonts (Archivo) og Tally-embed.
- Ny avhengighet krever eksplisitt godkjenning fra eier via prosjektleder.

## Visuell identitet

Mørk, kinematisk. Varm koksgrå palett, Archivo, redusert metning, hevet
kontrast, varme overlay-gradienter. Tillitsnivåene har fast fargekoding
definert av UX — den skal aldri improviseres av utvikler.

## Arbeidsform

- Eier snakker kun med **prosjektleder**. Andre agenter rapporterer til PM.
- All kommunikasjon til eier er på norsk, uten teknisk støy.
- Ingen oppgave går til utvikler uten akseptansekriterier.
- Den som skrev koden tester den ikke. Utvikler og tester er alltid ulike agenter.
- Tester fikser aldri selv — oppretter ny oppgave.
- Datakurator har veto på alt som viser eller utleder fit-data.
- Boardet i `/board` er sannheten om status. Oppdater det, ikke bare svar i chat.

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
- [ ] Forklaringsteksten til tillitsnivåene samsvarer i innhold med definisjonene
      i CLAUDE.md, godkjent av datakurator
- [ ] Datakurator har godkjent endelig versjon før den går til review
- [ ] Mobil (~380px) fungerer

## Utenfor scope

Fargekodingen av nivåene (se 001).

## Datakurators føringer

Gjelder forhåndsvisningen i seksjonen «Kommer» (`#kommer`). Tekst i
anførselstegn under er eksakt tekst. UX kan justere form og plassering, men ikke
endre betydningen i nivåtekstene eller begrunnelsene uten ny godkjenning fra
datakurator.

### 1. Regler for eksemplene

Eksemplene skal lære brukeren hvordan en vurdering ser ut. De skal aldri kunne
leses som en vurdering.

Ikke tillatt:

- Ekte bilmerker, modellnavn, generasjonskoder eller karosserinavn
  (for eksempel Volvo, XC90, «SPA», «stasjonsvogn XC»).
- Ekte setemerker, setemodeller eller deler av dem (for eksempel BeSafe, iZi,
  Minikid, Sirona, Dualfix).
- Oppdiktede navn som ser ut som ekte produkter («Nordic Safe 360», «Kombi X2»).
  Et oppdiktet navn som kan forveksles med et produkt, er like ille som et ekte.
- Navn som hinter mot et ekte produkt («svensk SUV», «kjent svensk
  bakovervendt»).
- Datoer, personnavn, organisasjonsnavn, lenker eller navngitte kilder
  (testorganisasjoner, blader, forhandlere). Oppdiktede datoer får eksemplet til
  å se ekte ut.
- Konkrete tall som ser ut som målinger (cm, vinkler, avstander).
- Godkjenningsmerker knyttet til et sete (i-Size, R129, R44). De tilfører ikke
  noe til eksemplet og kan leses som en påstand om godkjenning.

Tillatt:

- Generiske navn: «Eksempelbil», «Sete A», «Sete B» osv.
- Generiske beskrivelser av setetype og installasjonsmetode: bakovervendt,
  fremovervendt, ISOFIX, bilbelte, støtteben. Dette er informasjon hver ekte
  rad må ha, og eksemplet skal vise det.
- Generisk plassering i bilen («Bak, ytre»).
- Kildetype uten navn og dato («prøvemontert», «utledet fra mål»,
  «ingen data»).

Begrunnelse for «Frarådes»: kan nevne en mekanisme, men bare en som er et
problem i alle biler og med alle seter, slik at en forelder som kjenner seg
igjen ikke trekker en feil slutning om sin egen bil. «For lite plass
bakovervendt» er greit. «Støttebenet lander i gulvboksen» er ikke greit: noen
biler tillater støtteben på lokket, andre ikke, og det avhenger av bil og sete.
Mekanismen skal ikke knyttes til noe som ligner en ekte bil.

### 2. De fire eksempelradene

Hver rad skal vise «hvorfor» og kilde. Det er det viktigste eksemplet lærer
brukeren: at hvert nivå har en begrunnelse. Alle fire rader har samme oppbygning
og samme tekststørrelse. «Ikke testet» får en like lang og like synlig
forklaring som de andre, ikke en tom eller nedtonet linje.

| Navn | Undertekst | Nivå | Hvorfor |
|---|---|---|---|
| «Sete A» | «Bakovervendt · ISOFIX» | Bekreftet | «Prøvemontert i denne bilen, på denne plassen.» |
| «Sete B» | «Bakovervendt · bilbelte med støtteben» | Sannsynlig | «Utledet fra mål, ikke prøvemontert.» |
| «Sete C» | «Fremovervendt · ISOFIX» | Ikke testet | «Vi har ingen data om dette setet i denne bilen ennå.» |
| «Sete D» | «Bakovervendt · ISOFIX med støtteben» | Frarådes | «For lite plass bakovervendt: setet treffer forsetet. Kilde: prøvemontering.» |

Rekkefølgen over skal beholdes. Ingen rad skal skjules bak «vis mer», og «Ikke
testet» skal ikke plasseres sist eller skilles ut fra de andre.

### 3. Bilvelgeren

| Felt | Verdi |
|---|---|
| Merke | «Eksempelmerke» |
| Modell | «Eksempelbil» |
| Årsmodell | «20XX» |
| Plassering | «Bak, ytre» |

«20XX» er valgt med vilje: et ekte årstall gjør kombinasjonen mer troverdig
enn den skal være.

Merknad til senere (ikke denne oppgaven): i den ekte bilvelgeren må
«Årsmodell» kobles til generasjon og facelift. Årsmodell alene er ikke nok til
å gi en vurdering.

### 4. Forklaringstekst for nivåene

Erstatter hele teksten i `.legend`:

> «Merkelappene viser hvor sikre vi er, ikke bare om setet passer.
> **Bekreftet:** prøvemontert i akkurat denne bilen, eller oppført av produsenten
> i deres egen liste over biler setet passer i.
> **Sannsynlig:** utledet fra mål eller en nært beslektet bil, men ikke prøvd.
> Vi merker det alltid som utledet.
> **Ikke testet:** vi vet ikke. Det betyr verken at setet passer eller at det ikke
> passer.
> **Frarådes:** vi kjenner til et problem. Vi sier alltid hva problemet er og hvor
> vi har det fra.
> Uansett nivå: prøvemonter setet og følg bruksanvisningen.»

Til PM om akseptansekriteriet «samsvarer i innhold med definisjonene i
CLAUDE.md»: teksten over samsvarer i innhold med CLAUDE.md, men er ikke ordrett
(ord som «plattformdeling» og «fysisk verifisert» er ikke vanlig norsk for
foreldre). Jeg anbefaler at kriteriet endres til «samsvarer i innhold med
definisjonene i CLAUDE.md, godkjent av datakurator». Setningen «Vi gjetter
aldri» fjernes: den er et løfte om data vi ikke har ennå.

### 5. Krav til merkingen «Eksempel»

- Teksten «Eksempel – ikke en ekte vurdering» skal stå øverst i
  forhåndsvisningen, før bilvelgeren og radene, og være synlig uten hover,
  klikk eller rulling inne i boksen. Den erstatter eller står sammen med
  «Forhåndsvisning av bilvelgeren».
- Den skal ha minst samme kontrast og tekststørrelse som radtekstene. Den skal
  ikke bruke den nedtonede fargen (`--dim`), og ikke være mindre enn
  undertekstene i radene.
- «Kommer»-merket alene er ikke nok. «Kommer» sier noe om tid, ikke om at
  innholdet er oppdiktet.
- Hele forhåndsvisningen skal visuelt skille seg fra hvordan ekte resultater
  skal se ut, slik at den aldri kan forveksles med dem (UX velger virkemiddel).
- Et skjermbilde av én enkelt rad skal fortsatt vise at den er et eksempel.
  Navnene «Sete A–D» og «Eksempelbil» dekker dette, men bare hvis reglene i
  punkt 1 følges.
- Merkingen skal ligge i teksten, ikke bare i grafikk, slik at skjermlesere
  leser den opp før radene.
- På mobil (~380px) skal merkingen være synlig før første rad, uten
  avkutting.
- Nivåmerkene (Bekreftet osv.) i eksemplet skal ha samme farge og form som i
  det ekte produktet, siden eksemplet skal lære fargekodingen. Det er derfor
  merkingen av selve boksen må være tydelig.

Jeg vil nedlegge veto mot en løsning der merkingen bare er en liten eller
nedtonet tekst, bare vises i en tooltip, eller der «Ikke testet»-raden er mindre
synlig enn de andre.

### 6. Andre funn på siden (ikke rettet, til vurdering av PM)

Alle funn gjelder påstander som beskriver data og metode som om de allerede
finnes, eller som antyder mer sikkerhet enn nivåene gir.

1. Hero, `hero-sub` (linje 200): «Vi måler baksetet i norske familiebiler for
   hånd og kobler tallene mot hver bilstol som selges her. Så slipper du å
   gjette.» Presens om en database som ikke finnes. «Hver bilstol som selges
   her» er ikke realistisk. «Så slipper du å gjette» antyder sikkerhet, men mål
   alene gir aldri mer enn Sannsynlig. Mye vil være Ikke testet.
2. `meta description` (linje 7): «Uavhengig oversikt over bilstoler solgt i
   Norge, koblet mot ekte mål fra virkelige biler.» Presens, overdriver det som
   finnes i dag. Vises i søkeresultater.
3. `og:description` (linje 9): «Ekte mål fra virkelige biler, koblet mot hver
   bilstol solgt i Norge.» Samme problem. Vises når siden deles.
4. Tillitsstripen (linje 208–209): «Målt for hånd, bil for bil» og «Åpne data,
   alle kan etterprøve». Ingen data er publisert, så ingen kan etterprøve noe
   ennå. Bør være framtid eller et løfte, ikke en tilstand.
5. Seksjonstittel og ingress (linje 217–218): «Velg bilen din, få stolene som
   passer» og «En liste over det som går inn i akkurat ditt baksete». Dette er
   ja/nei-språk. Produktet gir fire nivåer, der Ikke testet er et vanlig svar.
   Teksten bør love å vise hva vi vet om hver stol, ikke hvilke som passer.
6. Påmelding (linje 266): «Vil du måle din egen bil? ... sender vi
   måleinstruksen.» Greit i seg selv, men føring for senere: mål fra brukere
   kan aldri gi mer enn Sannsynlig, og siden må ikke antyde at brukerens mål
   gir en bekreftet vurdering.
7. Fargen for «Ikke testet» (`--none`, grå) har lavere kontrast enn de andre
   nivåfargene og ser nedtonet ut ved siden av dem. Fargekoding er utenfor
   scope her (se 001), men det bør vurderes der: «Ikke testet» skal ikke se
   mindre viktig ut.
8. Bunnteksten «Vi erstatter ikke prøvemontering eller produsentens egen
   bruksanvisning.» er riktig og bør beholdes. Tilsvarende melding er nå lagt
   inn i nivåteksten (punkt 4).

## Logg

- 2026-09-22 PM: opprettet etter funn fra tester i 004. Spurt eier om retning.
- 2026-09-22 eier: valgte å bytte til eksempler som tydelig er oppdiktet (ikke fjerne
  seksjonen). Rekkefølge: datakurator (regler + nivåtekst) → ux (markering/tekst)
  → utvikler → datakurator godkjenner → tester.
- 2026-09-22 datakurator: skrev føringer (regler, fire eksempelrader, bilvelger,
  nivåtekst, krav til merking, 8 andre funn på siden). Anbefaler at AK
  «ordrett» endres til «samsvarer i innhold». Klar for UX.
- 2026-09-22 PM: godtok datakurators forslag. Kriteriet er endret fra «ordrett» til «i innhold».
  Datakurators funn 1–6 (lovnader i hero, meta, stripe og titler) er skilt ut i 008.
  Funn 7 er lagt til 001. Sendt til UX.

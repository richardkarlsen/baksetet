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

## UX-leveranse

Gjelder `site/index.html`. Linjenumre er dagens (før endring). Tekst i
anførselstegn under er eksakt — utvikler kan lime inn ordrett, inkludert
anførselstegn/guillemets der de forekommer. Jeg har ikke rørt `.demo`-blokken
(§221–256, godkjent i 006) eller bunnteksten.

| # | Sted (linje) | Nåværende tekst | Ny tekst | Begrunnelse |
|---|---|---|---|---|
| 1 | `hero-sub`, linje 224 | «Vi måler baksetet i norske familiebiler for hånd og kobler tallene mot hver bilstol som selges her. Så slipper du å gjette.» | «Vi måler baksetet i norske familiebiler for hånd, bil for bil. Svaret får alltid et tillitsnivå og en begrunnelse.» | Fjerner presens-påstand om en kobling som ikke finnes («hver bilstol som selges her») og løftet om å «slippe å gjette», som antyder sikkerhet ingen måling alene kan gi. Erstattet med hva brukeren faktisk får: et svar med nivå og begrunnelse — aldri et gjettefritt ja/nei. 114 tegn mot 123 i dag (kortere, ikke lengre). |
| 2 | `meta description`, linje 7 | «Uavhengig oversikt over bilstoler solgt i Norge, koblet mot ekte mål fra virkelige biler. Gratis, uten reklame og uten provisjon.» | «Uavhengig veileder for bilstoler i norske biler. Bygges med tillitsnivå og begrunnelse for hvert svar. Gratis, uten reklame og uten provisjon.» | Fjerner «koblet mot ekte mål fra virkelige biler» (presens om data som ikke finnes). Beholder «gratis, uten reklame og uten provisjon» uendret — det er sant i dag og en kjerneverdi. **142 tegn** (under ca. 155). |
| 3 | `og:description`, linje 9 | «Ekte mål fra virkelige biler, koblet mot hver bilstol solgt i Norge.» | «Vi bygger en uavhengig oversikt over bilstoler i norske biler — med tillitsnivå og begrunnelse for hvert svar.» | Samme problem som meta description, men delt separat siden den vises når siden deles i sosiale medier og bør stå på egne ben. «Vi bygger» er tydelig prosess/plan, ikke en påstand om et ferdig produkt. **110 tegn** (under ca. 155). |
| 4a | Tillitsstripen, linje 232 | «Målt for hånd, bil for bil» | «Skal måles for hånd, bil for bil» | Presens antyder en målejobb som allerede er gjort i stor skala. «Skal måles» gjør det til en plan, ikke en tilstand. |
| 4b | Tillitsstripen, linje 233 | «Åpne data, alle kan etterprøve» | «Målet: åpne data, alle kan etterprøve» | Ingen data er publisert ennå, så «alle kan etterprøve» er ikke sant i dag. Beholder løftet, men formulert eksplisitt som mål/intensjon slik oppgaven åpner for. |
| 5a | Seksjonstittel, linje 241 | «Velg bilen din, få stolene som passer» | «Velg bilen din, se hva vi vet om hver stol» | «Få stolene som passer» er et ja/nei-filter. Produktet gir fire nivåer der «Ikke testet» er et gyldig svar, ikke et filtrert bort resultat. Ny tittel lover informasjon, ikke en fasit. |
| 5b | Ingress under tittel, linje 242 | «Ikke en liste over alt som finnes. En liste over det som går inn i akkurat ditt baksete, med begrunnelse for hvert svar.» | «Ikke en liste over hva som passer eller ikke. En oversikt over hver stol i ditt baksete, med tillitsnivå og begrunnelse.» | Gjør ja/nei-avvisningen eksplisitt («ikke hva som passer eller ikke», i stedet for å selv antyde et pass/ikke-pass-filter). Legger til «tillitsnivå» så teksten speiler at hvert svar har et nivå, ikke bare en begrunnelse. **120 tegn, identisk lengde med dagens tekst.** |
| 6 | Påmelding, linje 314 | «Vil du måle din egen bil? Det tar fem minutter med målebånd og telefon. Meld deg på, så sender vi måleinstruksen.» | «Vil du måle din egen bil? Fem minutter med målebånd og telefon. Egne mål gir høyst «Sannsynlig». Meld deg på for måleinstruks.» | Oppfyller kravet: mål brukeren selv tar kan aldri gi «Bekreftet», og teksten sier det rett ut med samme ord som nivåtabellen bruker («Sannsynlig»), slik at forelderen ikke går ut fra at egen måling er nok til en bekreftet vurdering. 126 tegn mot 113 i dag: **12 % lengre** — vurdert som ikke vesentlig, men nevnes per krav. |

### Tillegg — samme problem funnet andre steder

Jeg gjennomgikk hele `site/index.html` for tilsvarende mønster (presens om
data/database som ikke finnes, løfte om sikkerhet, ja/nei-språk). Ingen flere
treff som krever endring:

- Linje 313, signup-avsnittet («Databasen bygges bil for bil...»): bruker
  presens, men om en pågående prosess («bygges»), ikke om et ferdig resultat.
  Det stemmer med situasjonen (arbeidet er i gang), så jeg lar den stå.
- Tittel og `h1` («... passer den i din bil?») er spørsmålsformulert, ikke en
  påstand om et ja/nei-svar som finnes i dag. Vurdert som utenfor problemet
  denne oppgaven retter opp, siden hele resten av siden nå tydeliggjør at
  svaret er et av fire nivåer. Foreslår ingen endring, men nevner det for
  datakurators vurdering ved godkjenning.
- `.kommer`-badgen, nav-lenken «Hva vi bygger», eyebrow-teksten og
  bunnteksten er allerede korrekte (framtid/plan eller sanne, uendrede fakta)
  og er ikke rørt.

### Merknader til utvikler

- Ingen nye CSS-klasser eller tokens. Alle endringer er ren tekst inni
  eksisterende elementer (`<p class="hero-sub">`, `<meta>`, `<span>` i
  `.strip-in`, `<h2>`/`<p>` i `.head`, `<p class="dim">` i signup).
  Tegnantallene over er tett nok på dagens til at layout ikke skal brekke
  ved 380px — ingen av tekstene bytter fra én til to linjer der de i dag
  har én, bortsett fra der de allerede brytes naturlig (hero-sub, ingress).
- Guillemets («Sannsynlig») skal limes inn som vist, ikke som rette
  anførselstegn.
- `.demo`-blokken (linje 245–304) skal ikke røres — den er ferdig behandlet
  i 006.

## Datakurators vurdering

**VETO** (2026-09-22). UX har gjort mye riktig. Løftet om å «slippe å gjette»
er borte, og det samme gjelder ja/nei-filteret. Punkt 3 og 4a godkjennes som
de står. Men flere av de nye tekstene bruker fortsatt presens om arbeid som
ikke har startet («Vi måler», «Databasen bygges»). Påmeldingsskjemaet i Tally
lover i tillegg å måle brukerens bil og bruker en ekte bil som eksempel. Alle
punktene under kan rettes i én runde. Tekst i «» er eksakt tekst. Legg den
inn ordrett.

Utgangspunkt: i dag har vi null målte biler, ingen database og ingen
publiserte data. Hver setning er vurdert opp mot det.

### 1. Hvert punkt 1–6

| # | Vurdering | Eksakt ny tekst |
|---|---|---|
| 1 hero-sub | **Veto.** «Vi måler» er presens, og vi har ikke målt en eneste bil. «Svaret får alltid» beskriver svar som ikke finnes. Teksten bør også si at «vi vet ikke» er et gyldig svar. Det er kjernen i produktet og det vanligste svaret i lang tid framover. «For hånd» er tatt ut fordi stripen rett under allerede sier det. | «Vi skal måle baksetet i norske familiebiler, bil for bil. Hvert svar skal få et tillitsnivå og en begrunnelse, også når svaret er at vi ikke vet.» (145 tegn. Lengre enn i dag, men hero-sub brytes uansett. UX må sjekke 380px.) |
| 2 meta description | **Veto.** «Uavhengig veileder for bilstoler» leses i et søkeresultat som en tjeneste som finnes og virker. «Bygges» er presens om en prosess som ikke har startet. Søkeresultatet er ofte det eneste folk leser, så det må stå tydelig at dette er under arbeid. | «Under arbeid: en uavhengig veileder for bilstoler i norske biler, med tillitsnivå og begrunnelse for hvert svar. Gratis, uten reklame og uten provisjon.» (152 tegn) |
| 3 og:description | **Godkjent.** «Vi bygger» er tydelig en plan. | Som UX foreslo. |
| 4a stripe | **Godkjent.** | «Skal måles for hånd, bil for bil» |
| 4b stripe | **Veto (språklig, men reelt).** I en stripe om måling leses «Målet:» lett som «målingen», altså som om målingen er åpne data. «Alle kan etterprøve» står også i presens. | «Dataene skal være åpne, så alle kan etterprøve dem» |
| 5a seksjonstittel | **Veto.** «Velg bilen din» er en oppfordring til noe man ikke kan gjøre i dag. «Hver stol» antyder en fullstendig oversikt over alle seter, som vi ikke har. Tittelen må vise at dette er slik det skal virke, ikke noe som finnes. | «Slik skal det virke: velg bilen din, se hva vi vet om stolene» |
| 5b ingress | **Veto.** «En oversikt over hver stol i ditt baksete» er presens om en oversikt som ikke finnes. Ingressen bør heller slå fast regelen om at stoler vi ikke vet noe om, vises som «Ikke testet» og ikke filtreres bort. | «Ikke en liste over hva som passer eller ikke. Hver stol skal vises med tillitsnivå og begrunnelse, også når svaret er «Ikke testet».» (132 tegn) |
| 6 påmelding | **Veto.** Se spørsmål 3 under. Og «Fem minutter» lover noe om en måleinstruks som ikke er skrevet. Måleprotokollen hører til datamodellen (002), som ikke er påbegynt. | «Vil du måle din egen bil? Meld deg på, så sender vi måleinstruksen når den er klar. Mål du tar selv, gir aldri mer enn «Sannsynlig», aldri «Bekreftet».» (151 tegn) |

### 2. De to stedene UX ikke endret

**(a) `<title>`, `og:title` og `h1` («Passer den i din bil?»).**

- `<title>` og `og:title`: **Veto.** De vises alene i søkeresultater, i
  nettleserfanen og når siden deles. Der kommer ingen forklaring etter, og et
  ja/nei-spørsmål løftes fram som det tjenesten svarer på. Ny tekst for begge:
  «Bilstolveileder — hva vet vi om bilstolen i din bil?»
  Spørsmålet kan også besvares med «ingenting ennå», og det er ærlig.
- `h1`: **Godkjent med vilkår.** Det er forelderens eget spørsmål, og det er
  legitimt å møte folk der. Vilkåret er at den nye hero-sub fra punkt 1 står
  rett under, slik at det første svaret er at det kommer et tillitsnivå og kan
  bli «vi vet ikke». Blir hero-sub endret eller flyttet senere, faller
  godkjenningen av h1 bort.

**(b) «Databasen bygges bil for bil, og vi starter med de bilene folk faktisk
har.»** **Veto.** Setningen er ikke sann i dag. UX begrunner den med at
«arbeidet er i gang», men ingen bil er målt, ingen database finnes og
datamodellen er ikke påbegynt. «Bygges» beskriver noe som skjer nå. I tillegg
kan «så havner den øverst i køen» ikke stemme for alle som melder seg på. Ny
tekst for hele avsnittet (`p.mid` i påmeldingen):

«Vi har ikke målt noen biler ennå. Vi begynner med de bilene folk faktisk har, så fortell oss hvilken du kjører. Det hjelper oss å velge hvilke biler vi måler først.»

### 3. Er «høyst Sannsynlig» riktig og tydelig?

Retningen er riktig. Et mål som en bruker tar selv, er aldri en fysisk
verifisering fra oss. Det gir derfor aldri «Bekreftet». Det gir heller ikke
automatisk «Sannsynlig», for det kan like gjerne ende i «Ikke testet» eller
«Frarådes». Et øvre tak er derfor riktig uttrykk. Men UX sin formulering er
ikke tydelig nok:

- «Egne mål» kan leses som *våre* mål, altså tjenestens egne målinger. Det må
  stå «Mål du tar selv».
- «Høyst» sier ikke med rene ord at «Bekreftet» er utelukket. Det er nettopp
  den misforståelsen vi må forhindre. Derfor står «aldri «Bekreftet»» med i
  teksten i punkt 6.

Føring til 002 (ikke denne oppgaven): mål fra brukere kan ikke brukes til
noe før vi har en måleprotokoll og en måte å kontrollere kvaliteten på. Fram
til da gir de ikke engang «Sannsynlig». Teksten over lover bare et tak, ikke
et nivå, og er derfor fortsatt sann.

### 4. Andre steder med samme problem

1. **Tally-skjemaet (LZ2Qjj) som er innebygd på siden. Veto, er en del av
   008.** Jeg har lest skjemaet uten å endre det. Det vises inne i siden og
   har samme problem:
   - Innledning: «Fortell hvilken bil du har, så måler vi den først.» Dette
     er et løfte vi ikke kan holde overfor alle. Ny tekst: «Fortell hvilken bil
     du har. Det hjelper oss å velge hvilke biler vi måler først.»
   - Plassholder i feltet «Bilen din»: «Volvo XC90 2016». Dette er nøyaktig
     den ekte bilen vi fjernet fra demoen i 006. I tillegg lærer den brukeren
     å oppgi bare årsmodell, mens vi trenger generasjon og karosseri. Ny
     plassholder: «Merke, modell, årsmodell og karosseri»
   - Takkesiden: «Bilen din står nå på listen over biler vi måler.» Dette
     antyder at bilen blir målt. Ny tekst: «Vi har notert bilen din. Du hører
     fra oss når tjenesten åpner.»
   Endringene gjøres i Tally, ikke i `site/`. PM avgjør hvem som gjør det.
   Det krever ingen ny avhengighet.
2. **Logoen i navigasjonen (skjold med hake, linje 192). Ikke veto på 008,
   men egen oppgave kreves.** Et skjold med hake leses som «godkjent» eller
   «sikkerhetssertifisert». Det overdriver sikkerheten visuelt og ligner på
   grafikken til testorganisasjoner og godkjenningsmerker. UX bør bytte til et
   nøytralt merke uten hake. Jeg vil nedlegge veto mot at ekte fit-data vises
   så lenge dette merket står der.
3. **Forklaringsteksten i demoen, «ikke bare om setet passer» (godkjent av meg
   i 006).** Ikke blokkerende. «Bare» antyder at merket også er et ja/nei. Kan
   vurderes senere, for eksempel «Merkelappene viser hvor sikre vi er, ikke om
   setet passer».
4. Følgende er gjennomgått og i orden: eyebrow, «Vi tjener ingenting på
   valget ditt», «Få beskjed når vi åpner», «Én e-post når vi åpner»,
   `.kommer`, nav-lenken «Hva vi bygger», alt-teksten på hero-bildet og
   bunnteksten, som skal beholdes.

### Hva som skal til for GODKJENT

Alle eksakte tekster over er lagt inn ordrett: punkt 1, 2, 4b, 5a, 5b og 6,
`<title>` og `og:title`, avsnittet i påmeldingen og de tre tekstene i Tally.
Da godkjenner jeg uten ny runde med tekst. Jeg vil likevel se den ferdige
siden og skjemaet før kortet går til done.

## Logg

- 2026-09-22 PM: opprettet etter funn fra datakurator i 006.
- 2026-09-22 PM: eier ba om å starte. Flyttet til doing, delegert til UX.
- 2026-09-22 UX: Skrevet nye tekster for punkt 1–6 (hero, meta description,
  og:description, tillitsstripe, seksjonstittel/ingress, påmelding). Fjernet
  presens-påstander om data/database/åpne data som ikke finnes, fjernet
  løftet «slipper å gjette», fjernet ja/nei-formuleringen «få stolene som
  passer», og lagt inn eksplisitt at egne mål høyst gir «Sannsynlig» i
  påmeldingsteksten. Meta description 142 tegn, og:description 110 tegn
  (begge under ca. 155). Signup-teksten (punkt 6) ble 12 % lengre — nevnt
  som ikke vesentlig. Øvrige tekster er lik eller kortere lengde enn i dag.
  Gjennomgikk resten av siden for samme mønster: fant ingen flere
  nødvendige endringer, men peker på tittel/h1 («passer den i din bil?»)
  til datakurators vurdering. Bunntekst og `.demo`-blokken er ikke rørt.
  Klar for datakurators godkjenning. Kortet ikke flyttet.
- 2026-09-22 datakurator: VETO. Punkt 3 og 4a godkjent. Veto på 1, 2, 4b, 5a,
  5b og 6 (fortsatt presens om arbeid som ikke har startet, «hver stol»,
  «egne mål» kan misforstås, «fem minutter» om en instruks som ikke finnes).
  Veto på `<title>`/`og:title`. `h1` godkjent på vilkår om at ny hero-sub står
  rett under. Veto på «Databasen bygges» (ikke sant, ingen bil er målt).
  Nytt funn: Tally-skjemaet lover å måle bilen, bruker «Volvo XC90 2016» som
  plassholder og lover på takkesiden at bilen blir målt. Veto, tas med i 008.
  Logo med skjold og hake bør få egen oppgave. Eksakt tekst for alt står under
  «Datakurators vurdering», så alt kan rettes i én runde. Tally lest, ikke
  endret. `site/` ikke rørt. Kortet ikke flyttet.
- 2026-09-22 PM: datakurator la ned veto og ga eksakt tekst. Datakurators tekst gjelder
  foran UX-forslaget der de er ulike. Scope er utvidet med `<title>`/`og:title`, avsnittet
  «Databasen bygges…» og Tally-skjemaet LZ2Qjj (tre tekster). Logo-funnet er skilt ut i 009.
  Føringen om brukermål er lagt i 002. Sendt til utvikler.
- 2026-09-22 utvikler: Lagt inn datakurators eksakte tekster i `site/index.html` ordrett
  (title/og:title, meta description, og:description, hero-sub, stripe 4a/4b,
  seksjonstittel/ingress 5a/5b, påmelding p.mid/p.dim). `h1` og `.demo`-blokken urørt.
  Hero-sub talt til 145 tegn nøyaktig som datakurator oppga; ingen fast høyde/overflow i
  CSS rundt `.hero-in`/`.rise`, så ekstra linje ved ~380px gir en høyere hero, ikke brukket
  layout. Committet lokalt, ikke pushet: commit `1ddc6031d4a9f9df9495d7199e0cfafff97ed02a`.
  Tally-skjema LZ2Qjj: lastet inn, alle tre gamle tekster stemte ordrett med det datakurator
  siterte. Endret og lagret (status PUBLISHED, uendret):
  1. Intro-tekst (blokk d211f53a…): «Fortell hvilken bil du har, så måler vi den først.» →
     «Fortell hvilken bil du har. Det hjelper oss å velge hvilke biler vi måler først.»
  2. Plassholder i «Bilen din» (blokk ecd02dfb…): «Volvo XC90 2016» →
     «Merke, modell, årsmodell og karosseri»
  3. Takketekst (blokk bdfc2573…): «Bilen din står nå på listen over biler vi måler. Du
     hører fra oss når tjenesten åpner.» → «Vi har notert bilen din. Du hører fra oss når
     tjenesten åpner.»
  Ingen felt, rekkefølge, logikk eller styling i Tally er endret. Kortet ikke flyttet,
  ingen kriterier krysset av. Klar for datakurators og testers gjennomgang.
- 2026-09-22 PM: lest diffen i 1ddc603. Tekstene står som datakurator ga dem. Flyttet til review. Datakurator (sjekker side + Tally) og tester jobber parallelt. Ikke pushet.

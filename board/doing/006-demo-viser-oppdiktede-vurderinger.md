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

## UX-spesifikasjon

Gjelder kun `#kommer`-seksjonen i `site/index.html` (dagens linjer ca.
115–146 CSS, 221–256 HTML). Ingen nye avhengigheter, ingen eksterne ikoner —
all grafikk er inline SVG. Ingen nye CSS-tokens (se begrunnelse i punkt 5).
Nivåfargene (`.tag`, `.t-ok`, `.t-maybe`, `.t-none`, `.t-no`) er **ikke**
endret — de skal se ut akkurat som i dag.

### 0. Prinsipp

Merkingen «Eksempel» løses med to virkemidler samtidig, ikke ett:

1. En egen, tydelig linje øverst i boksen (`.demo-flag`) med ikon + tekst,
   plassert **før** `.demo-bar` i DOM-rekkefølgen — altså det aller første
   skjermlesere og øyne møter i boksen.
2. Boksen som helhet får en annen kantfarge (varm/amber i stedet for nøytral
   `--line`), slik at hele forhåndsvisningen er visuelt forskjellig fra
   hvordan ekte resultatkort skal se ut, ikke bare merket i toppen.

Fargen som brukes til begge er `--amber`/`--amber-bg` — samme farge som
`.kommer`-merket allerede bruker for «ikke ferdig ennå». Det er ingen av de
fire tillitsnivå-fargene, så det er ingen fare for forveksling med
Bekreftet/Sannsynlig/Ikke testet/Frarådes.

### 1. HTML — full erstatning av `.demo`-blokken

Erstatt hele blokken fra `<div class="demo">` til dens lukkende `</div>`
(dagens linje 221–256) med:

```html
<div class="demo">
  <div class="demo-flag">
    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.7" aria-hidden="true" focusable="false">
      <circle cx="12" cy="12" r="9"/>
      <path d="M12 11v5"/>
      <circle cx="12" cy="8" r=".6" fill="currentColor" stroke="none"/>
    </svg>
    <p>Eksempel – ikke en ekte vurdering</p>
  </div>
  <div class="demo-bar">
    <p>Forhåndsvisning av bilvelgeren</p>
    <span class="kommer">Kommer</span>
  </div>
  <div class="demo-body">
    <div class="picker">
      <button class="pick inert" type="button"><small>Merke</small><b>Eksempelmerke</b></button>
      <button class="pick inert" type="button"><small>Modell</small><b>Eksempelbil</b></button>
      <button class="pick inert" type="button"><small>Årsmodell</small><b>20XX</b></button>
      <button class="pick inert" type="button"><small>Plassering</small><b>Bak, ytre</b></button>
    </div>

    <div class="row">
      <div class="fig"></div>
      <div class="txt">
        <b>Sete A</b>
        <small>Bakovervendt · ISOFIX</small>
        <small class="why">Prøvemontert i denne bilen, på denne plassen.</small>
      </div>
      <span class="tag t-ok">Bekreftet</span>
    </div>
    <div class="row">
      <div class="fig"></div>
      <div class="txt">
        <b>Sete B</b>
        <small>Bakovervendt · bilbelte med støtteben</small>
        <small class="why">Utledet fra mål, ikke prøvemontert.</small>
      </div>
      <span class="tag t-maybe">Sannsynlig</span>
    </div>
    <div class="row">
      <div class="fig"></div>
      <div class="txt">
        <b>Sete C</b>
        <small>Fremovervendt · ISOFIX</small>
        <small class="why">Vi har ingen data om dette setet i denne bilen ennå.</small>
      </div>
      <span class="tag t-none">Ikke testet</span>
    </div>
    <div class="row">
      <div class="fig"></div>
      <div class="txt">
        <b>Sete D</b>
        <small>Bakovervendt · ISOFIX med støtteben</small>
        <small class="why">For lite plass bakovervendt: setet treffer forsetet. Kilde: prøvemontering.</small>
      </div>
      <span class="tag t-no">Frarådes</span>
    </div>
  </div>
  <p class="legend">Merkelappene viser hvor sikre vi er, ikke bare om setet passer. <b>Bekreftet:</b> prøvemontert i akkurat denne bilen, eller oppført av produsenten i deres egen liste over biler setet passer i. <b>Sannsynlig:</b> utledet fra mål eller en nært beslektet bil, men ikke prøvd. Vi merker det alltid som utledet. <b>Ikke testet:</b> vi vet ikke. Det betyr verken at setet passer eller at det ikke passer. <b>Frarådes:</b> vi kjenner til et problem. Vi sier alltid hva problemet er og hvor vi har det fra. Uansett nivå: prøvemonter setet og følg bruksanvisningen.</p>
</div>
```

Merk til utvikler:

- Rekkefølgen `demo-flag` → `demo-bar` → `demo-body` → `legend` er bindende.
  `demo-flag` skal alltid stå først i markup, ikke bare visuelt plassert med
  CSS.
- `.kommer`-badgen («Kommer») beholdes i `demo-bar` som i dag — den fjernes
  ikke, men den er ikke lenger alene om å signalisere at innholdet ikke er
  ekte.
- Ingen `aria-*`-attributter er nødvendig utover `aria-hidden="true"
  focusable="false"` på SVG-ikonene (de er rent dekorative). DOM-rekkefølgen
  alene sikrer at skjermlesere leser «Eksempel – ikke en ekte vurdering» før
  bilvelgeren og radene.
- Innholdet i `<p class="legend">` er skrevet som én sammenhengende
  brødtekst med `<b>` rundt nivånavnene, i stedet for datakurators
  sitatoppsett med linjeskift. Dette er en ren markup-omforming for HTML —
  **ingen ord er endret, lagt til eller fjernet.**

### 2. CSS — nye og endrede regler

Legg til rett etter dagens `.kommer{...}`-regel (ca. linje 119):

```css
.demo{border:1px solid rgba(224,163,74,.35)}

.demo-flag{
  display:flex;align-items:flex-start;gap:9px;
  padding:14px 20px;
  background:var(--amber-bg);
  border-bottom:1px solid rgba(224,163,74,.35);
}
.demo-flag svg{flex:none;margin-top:2px;color:var(--amber)}
.demo-flag p{
  margin:0;
  font-weight:600;
  font-size:15.5px;
  line-height:1.35;
  color:var(--bone);
}
```

`.demo{border:...}` overstyrer det eksisterende `border:1px solid
var(--line)` i `.demo`-regelen (fjern `var(--line)`-verdien der, ikke legg
den varme kantfargen til som en ny regel ved siden av — det skal kun være én
`border`-verdi på `.demo`).

Endre disse to eksisterende reglene:

```css
.row .txt small{display:block;color:var(--mid);font-size:13px;margin-top:2px}
```
(var `color:var(--dim)` → `color:var(--mid)`, og lagt til `display:block` +
`margin-top:2px` for forutsigbar linjedeling nå som raden har tre
tekstlinjer i stedet for to.)

Legg til en ny regel for «hvorfor»-linjen:

```css
.row .txt .why{
  display:block;
  margin-top:4px;
  font-size:13px;
  font-weight:400;
  line-height:1.45;
  color:var(--bone);
}
```

Endre `.legend`:

```css
.legend{padding:16px 20px;border-top:1px solid var(--line);font-size:13.5px;color:var(--mid)}
.legend b{color:var(--bone);font-weight:600}
```
(var `color:var(--dim)` → `color:var(--mid)`. Se begrunnelse i punkt 6.)

Alt annet i disse selektorene (`.demo`, `.row`, `.legend`) er uendret.

### 3. Hvorfor disse fargevalgene (kontrast, gråtone, ikke `--dim`)

Beregnet mot `--ink-2` (#1D1A17), som er bakgrunnen i hele `.demo`-boksen.
WCAG AA for normal tekst krever 4.5:1.

| Tekst | Farge | Kontrast mot `--ink-2` | Bruk |
|---|---|---|---|
| `.demo-flag p` (Eksempel-linjen) | `--bone` | ≈15,3:1 | Lik kontrast som radnavn (`.row .txt b`) |
| `.row .txt b` (Sete A–D) | `--bone` | ≈15,3:1 | Uendret |
| `.row .txt .why` (hvorfor-linjen) | `--bone` | ≈15,3:1 | Minst like lesbar som navnet, aldri mer nedtonet |
| `.row .txt small` (undertekst type/montering) | `--mid` (endret fra `--dim`) | ≈6,3:1 | `--dim` ga bare ≈3,1:1, under AA-kravet for normal tekst |
| `.legend` | `--mid` (endret fra `--dim`) | ≈6,3:1 | Samme begrunnelse som over |

`--dim` (#6E665E) brukes ikke noe sted i denne spesifikasjonen, verken i
Eksempel-merkingen eller i radene, i tråd med kravet i føring 5.

Gråtonetest: Eksempel-linjen skiller seg fra ekte innhold uavhengig av farge
fordi (a) den ligger i en egen stripe med annen bakgrunnstetthet
(`--amber-bg`) og kantstrek enn resten av boksen, og (b) selve boksen har en
synlig lysere/varmere kant enn nøytrale innholdsbokser (f.eks. `.signup`,
som beholder `var(--line)`). Dette virker likt i gråtone siden det er en
form-/tetthetsforskjell (stripe + kant), ikke en fargeforskjell alene.
Nivåmerkene (`.tag`) er uendret og skal fortsatt suppleres med tekst og form
per oppgave 001 — det er ikke rørt her.

### 4. «Hvorfor»-linjen — oppsummert

- Plassering: tredje linje i `.row .txt`, under navn og undertype/montering,
  i alle fire rader.
- Typografi: 13px, vekt 400, linjehøyde 1.45 — samme størrelse i alle fire
  rader, ingen unntak for «Ikke testet».
- Farge: `--bone`, samme farge som radnavnet. Den er dermed **mer** synlig
  enn undertekst-linjen over den (som bruker `--mid`), aldri mindre. Dette
  er bevisst: føring 2 sier hvorfor-linjen er det viktigste eksemplet
  lærer bort.
- «Sete C» (Ikke testet) får nøyaktig samme markup, klasse og styling som de
  tre andre — ingen egen, kortere eller gråere versjon.

### 5. Tokens — ingen nye

Alt er bygget av eksisterende `:root`-tokens: `--bone`, `--mid`, `--amber`,
`--amber-bg`. `rgba(224,163,74,.35)` er ikke en ny farge — det er
`--amber`s egen RGB-verdi (224,163,74) med en annen alpha, samme mønster
som `.kommer` allerede bruker (`rgba(224,163,74,.28)` som kantfarge). Det
introduseres altså ingen ny hex-verdi i paletten.

### 6. Avvik fra datakurators ordlyd — til godkjenning

Ingen ord er endret, lagt til eller fjernet. To rene presentasjonsvalg
markeres likevel her siden føringen ber om at avvik synliggjøres:

1. **Legend-tekst som sammenhengende avsnitt.** Datakurators tekst er gitt
   som et sitat med linjeskift per nivå. Jeg har satt den som ett
   `<p>`-avsnitt med `<b>` rundt nivånavnene, siden HTML ikke har
   Markdown-fet skrift og linjeskift midt i et avsnitt gir dårligere
   flyt/lesbarhet på mobil enn naturlig tekstbryting. Ordlyden er identisk.
2. **`.legend`-farge endret fra `--dim` til `--mid`.** Dette er et
   kontrastvalg (se punkt 3), ikke en endring av teksten. Føring 5 forbyr
   `--dim` bare for selve Eksempel-merkingen, men jeg anbefaler samme fiks
   her siden avsnittet inneholder de fire nivånavnene i fet skrift og bør
   være lesbart.

### 7. Mobil (~380px)

- `.demo-flag` bruker samme sidepolstring som `.demo-bar` (14px 20px) og har
  ingen `white-space:nowrap` eller `text-overflow` — teksten brytes til to
  linjer ved behov, aldri avkuttet.
- `.picker` er allerede `repeat(auto-fit,minmax(150px,1fr))`, som ved 380px
  (etter `.wrap`- og `.demo-body`-polstring, ca. 280–290px igjen) gir én
  kolonne — uendret oppførsel, ingen endring nødvendig.
- Radenes flertekst (`b`, `small`, `small.why`) er alle blokk-elementer og
  stables uansett bredde. Eksisterende regel `@media(max-width:620px){.row
  {flex-wrap:wrap...}}` er uendret og påvirker ikke stablingen inni `.txt`.
- Ingen ny mediaquery er nødvendig for kravene i denne oppgaven.

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
- 2026-09-22 UX: Skrev spesifikasjon (HTML, CSS med eksakte verdier, kontrastberegninger).
  Løsning: egen `.demo-flag`-stripe øverst (ikon + «Eksempel – ikke en ekte vurdering», farge
  `--bone` på `--amber-bg`) pluss amber-tint kant på hele `.demo`-boksen, slik at hele
  forhåndsvisningen skiller seg fra ekte resultater, ikke bare toppen. «Hvorfor»-linjen får
  egen klasse `.why`, `--bone`, 13px, lik i alle fire rader inkl. «Ikke testet». Byttet
  `--dim` → `--mid` i radenes undertekst og i `.legend` (kontrast, ikke tekstendring). Ingen
  nye tokens — gjenbruker `--amber` sin RGB-verdi ved annen alpha, samme mønster som
  `.kommer` allerede bruker. To rene presentasjonsvalg (legend som sammenhengende avsnitt,
  og `--dim`→`--mid` i legend) er markert i eget punkt for datakurators godkjenning. Ordlyden
  ellers er ordrett. Klar for datakurator, deretter utvikler.
- 2026-09-22 PM: UX-spesifikasjonen er mottatt. Sendt til utvikler. Datakurator godkjenner resultatet etterpå, også UX sine to valg for presentasjonen.
- 2026-09-22 utvikler: Implementert UX-spesifikasjonen i `site/index.html`, kun `.demo`-blokken
  i `#kommer` og tilhørende CSS. HTML erstattet ordrett med spesifikasjonens markup
  (`demo-flag` → `demo-bar` → `demo-body` → `legend`, i den rekkefølgen). CSS lagt til/endret
  nøyaktig som spesifisert: `.demo-flag` (ny), `.demo`-kant endret til `rgba(224,163,74,.35)`
  (fjernet `var(--line)`, ingen dobbel border-regel), `.row .txt small` endret fra `--dim` til
  `--mid` + `display:block`/`margin-top:2px`, ny `.row .txt .why`-regel, `.legend` endret fra
  `--dim` til `--mid` og ny `.legend b`-regel. Ingen nye tokens brukt. Grep av hele filen etter
  ekte merker/modeller/godkjenningsmerker/årstall (volvo, xc90, besafe, izi, minikid, sirona,
  axkid, cybex, britax, dualfix, r129, r44, i-size, 20NN) ga ingen treff (ett falskt positivt:
  "izi" traff i "box-sizing"). Andre tekster på siden (hero, meta, stripe, seksjonstittel,
  påmelding) er ikke rørt — det er oppgave 008. Nivåfargene (`--ok/--maybe/--none/--no`, `.t-*`)
  er ikke rørt. Committet lokalt, ikke pushet. Klar for datakurators godkjenning og tester.

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

- [x] Hex-verdier oppgitt for bakgrunn, kant, tekst og ikon per nivå
- [x] Alle fire skiller seg tydelig fra hverandre i gråtone
- [x] Kontrast minst WCAG AA mot mørk bakgrunn
- [x] Hvert nivå har form/ikon i tillegg til farge
- [x] "Ikke testet" leses som nøytral, ikke som feil eller advarsel
- [x] Levert som CSS-variabler utvikler kan lime rett inn

## Utenfor scope

Implementasjon i index.html. Egen oppgave.

## UX-leveranse

**Revidert etter datakurators veto (K1–K5), oppdatert i denne seksjonen —
ingen ny seksjon lagt til ved siden av.** Fem endringer fra forrige versjon:
«Sannsynlig» får synlig «utledet»-tekst i selve merkelappen (K1), ikonene for
«Sannsynlig» og «Ikke testet» er tegnet om så de ikke flyter sammen ved 14px
(K2), kanttabellen er regnet på nytt med alfa inkludert og kantfargene er
justert til reelt ≥3:1 (K3), rendret gråtonebevis er lagt ved som PNG under
`board/assets/001/` (K4), og haken er skrevet inn som reservert for Bekreftet
alene (K5). I tillegg er ordet «trygg» fjernet fra begrunnelsen for Bekreftet.
Fargene, tekstkontrasten og `--dim` er uendret, jf. datakurators tilbakemelding.

**Feilen datakurator fant i K3:** kanttabellen i forrige versjon sammenlignet
den ugjennomsiktige HEX-fargen mot bakgrunnen, ikke fargen slik den faktisk
rendres med sin alfaverdi lagt over bakgrunnen. Det ga tall som var 2–3x for
høye (f.eks. 6,32:1 oppgitt mot reelt 2,83:1 for «Ikke testet»). Tabellen i
pkt. 4 under er nå regnet riktig: `rgba(nivåfarge, alfa)` komposittert i sRGB
over `--ink`/`--ink-2`, deretter WCAG-kontrast av det komposittérte resultatet
mot samme bakgrunn — samme metode som allerede ble brukt riktig for
tekst/ikon-kontrasten (som datakurator bekreftet stemte, ±0,03).

Kontrast for tekst/ikon er beregnet mot den faktiske renderte bakgrunnen
(nivåfargen lagt som `rgba(...)`-tone over `--ink-2`, slik merkelappene
faktisk vises i dag inni `.demo`), ikke mot `--ink-2` rått. Det er derfor
tallene her ikke er identiske med en enkel oppslag av tekstfarge mot
`--ink-2`. Alle beregninger er WCAG relativ luminans, alfa-komposittert i
sRGB (slik nettlesere komposittere enkel `rgba()`-blanding).

Grayton-testen viser at ren lysstyrke ikke skiller de fire nivåene godt nok —
det gjelder også dette forslaget (se pkt. 5). Derfor bærer **ikonets form og
tegn, sammen med kantens stil,** hovedansvaret for skillet, ikke
farge/lysstyrke. Fyllgrad er tatt ut som eget påstått signal (K3) bortsett
fra ett reelt tilfelle: Ikke testet har ingen fyll i det hele tatt, mens de
tre andre har det — det er en binær, synlig forskjell, ikke en gradering.
Sirkel vs. trekant, og hake vs. bølge vs. tom ring, skal kunne skilles selv
om skjermen er helt avmettet.

### 1. CSS-variabler

Direkte erstatning for dagens `--ok/--maybe/--none/--no` + tre nye
kant-variabler per nivå + justert `--dim`. Lim inn i `:root` i
`site/index.html` (linje ca. 16–34), i tillegg til det som står der (line/mid/
bone/amber beholdes uendret):

```css
/* Bekreftet */
--ok:        #7FD16A;
--ok-bg:     rgba(127,209,106,.16);
--ok-border: rgba(107,190,85,.55);   /* uendret — ga allerede ≥3:1 */

/* Sannsynlig */
--maybe:        #8FB4EA;
--maybe-bg:     rgba(143,180,234,.15);
--maybe-border: rgba(118,155,214,.65); /* K3: alfa opp fra .5 → reelt ≥3:1 */

/* Ikke testet */
--none:        #C2BBAF;
--none-bg:     rgba(194,187,175,.13);
--none-border: rgba(163,155,146,.65); /* K3: alfa opp fra .55 → reelt ≥3:1 */

/* Frarådes */
--no:        #F2937D;
--no-bg:     rgba(242,147,125,.16);
--no-border: rgba(228,115,90,.70);    /* K3: alfa opp fra .6 → reelt ≥3:1 */

/* Justert — se begrunnelse under */
--dim: #8F877C; /* var: #6E665E */
```

`--dim` foreslås hevet fra `#6E665E` til `#8F877C`. Det gir AA (≥4,5:1) mot
`--ink`, `--ink-2` og `--ink-3` samtidig (se tabell i pkt. 4), så regelen blir
enkel: **`--dim` er nå trygg å bruke som tekstfarge på alle tre
bakgrunnsvariantene** (`--ink`, `--ink-2`, `--ink-3`) uten unntak eller
spesialtilfeller. `.pick small` (som utløste funnet) trenger ingen egen
unntaksregel — den arver bare det oppdaterte tokenet.

### 2. SVG-ikon per nivå

`viewBox="0 0 20 20"`, `fill="none"` på `<svg>`, farge styres av `color` på
merkelappen (ikonet bruker `currentColor` — ingen egen ikonfarge-variabel
trengs, det arver nivåfargen).

**Bekreftet** — hel omriss-sirkel med hake. (Stødig, avsluttet.) Svakt fyll (0,18) er teknisk til stede, men leses ikke som fylt. Ikonet skal ALDRI gjøres om til en fylt sirkel.
```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <circle cx="10" cy="10" r="8" fill="currentColor" fill-opacity="0.18" stroke="currentColor" stroke-width="1.6"/>
  <path d="M6.4 10.3l2.5 2.4 4.7-5.4" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
</svg>
```

**Sannsynlig — revidert (K2)** — sirkel, stiplet kant, svakt fylt, tydelig
bølge ("omtrent"/"≈"). Forrige versjon hadde en bølge på ca. 1,65 enheter
topp-bunn i viewBox 20 — ved 14px ble det under 1,2px, og bølgen så ut som en
rett strek, umulig å skille fra «Ikke testet». Ny bølge går fra y=8 til y=15,
altså ca. 5,2 enheter mellom kurvetoppene i viewBox 20. Ved 14px blir det ca. 3,7px (kontrollert av datakurator)
topp-bunn — godt over K2s krav på ca. 2px. Strøket er også gjort tykkere
(1,6 → 2,0) for lik visuell tyngde som de andre ikonene.
```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <circle cx="10" cy="10" r="8" fill="currentColor" fill-opacity="0.12" stroke="currentColor" stroke-width="1.8" stroke-dasharray="2.8 2.4"/>
  <path d="M5 11.5C6.4 8 8.6 8 10 11.5S13.6 15 15 11.5" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round"/>
</svg>
```

**Ikke testet — revidert (K2)** — kraftig, HEL, tom ring. Ingen strek, ingen
prikker, ingen tegn inni. Forrige versjon (prikket kant + vannrett strek) er
forkastet av to grunner datakurator påpekte: (1) en sirkel med vannrett strek
gjenbruker formen til det norske skiltet «innkjøring forbudt» og kan derfor
leses som et negativt svar vi ikke har grunnlag for, og (2) tynn prikket kant
har minst "blekk" av de fire ikonene og kan se deaktivert/svak ut — stikk i
strid med at «Ikke testet» skal være nøytral, ikke dempet. Løsningen er en
tom ring uten tegn, men med kraftig strøk (stroke-width 2,8 — tykkere enn
noen av de andre ikonenes enkeltstrøk), slik at den ikke er "svakere" enn de
andre rent visuelt.

```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <circle cx="10" cy="10" r="7.6" fill="none" stroke="currentColor" stroke-width="2.8"/>
</svg>
```

**Frarådes** — trekant (eneste ikke-runde formen — kategorisk forskjellig
silhuett), fylt, tykkere kant, utropstegn.
```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <path d="M10 3.1L17.6 16.3A1 1 0 0 1 16.73 17.8H3.27A1 1 0 0 1 2.4 16.3Z" fill="currentColor" fill-opacity="0.18" stroke="currentColor" stroke-width="1.7" stroke-linejoin="round"/>
  <path d="M10 8v3.6" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/>
  <circle cx="10" cy="14.2" r="1" fill="currentColor"/>
</svg>
```

Alle ikoner er dekorative (`aria-hidden="true"`) — teksten i merkelappen
("Bekreftet" osv.) er det tilgjengelige navnet, ikke ikonet.

**K5 — krav: haken er reservert for Bekreftet, uansett ramme (sirkel, skjold eller ingen ramme).**
Ingen annet ikon, logo eller UI-element på baksetet.no skal bruke en hake i
lukket ramme i `currentColor`. Datakurator har påpekt at forslaget til logo i
oppgave 009 bruker nøyaktig samme form (enkel hake i en lukket ramme), noe
som ville gjort at hver side har et "Bekreftet"-merke i navigasjonen før
brukeren har valgt bil, og dermed svekket hakens verdi som eget signal i
tillitsnivåene. Dette kravet gjelder 009 og enhver senere oppgave, ikke bare
denne. 001 er ikke selv blokkert av logokonflikten.

### 3. Etiketter og merkelappens anatomi

Etikettekst uendret: **Bekreftet**, **Sannsynlig**, **Ikke testet**,
**Frarådes**. Nivånavnene endres ikke.

**K1 — «Sannsynlig» skal alltid vise at svaret er utledet, som synlig tekst i
selve merkelappen** (ikke tooltip), i tråd med CLAUDE.md («Sannsynlig ...
Skal alltid merkes som utledet»). Dette gjelder kun etiketten for Sannsynlig
— de tre andre er uendret:

| Visning | Etikettekst for Sannsynlig |
|---|---|
| Liste (`.tag`) | `Sannsynlig · utledet` |
| Detalj (`.tag-lg`) | `Sannsynlig – utledet, ikke verifisert` |

Hele etiketten (hovedord + tillegg) har samme farge og vekt — ingen del av
teksten er dempet eller mindre synlig enn resten, slik at kontrasttabellen i
pkt. 4 gjelder uendret for hele strengen. `.tag` sitt `white-space:nowrap`
bør revurderes av utvikler for `.t-maybe` spesifikt (lengre tekst), enten
ved å tillate linjebryting eller ved å teste at pillen ikke klipper teksten
på smale skjermer — dette er en implementasjonsdetalj, ikke et tokenvalg.

| Egenskap | Liste (`.tag`) | Detalj (`.tag-lg`) |
|---|---|---|
| Ikonstørrelse | 14×14px | 18×18px |
| Avstand ikon→tekst | 6px | 8px |
| Padding | 4px 10px 4px 8px | 8px 14px 8px 11px |
| Border-radius | 6px | 8px |
| Font-size | 12.5px | 14.5px |
| Font-weight | 600 (likt for alle fire — ingen nivå skal se "svakere" ut enn et annet pga. vekt) | 600 |
| Letter-spacing | .01em | .01em |
| Line-height | 1 | 1.1 |
| display | inline-flex, align-items:center | inline-flex, align-items:center |

Kantstil per nivå (bredde + stil er en egen ikke-farge-basert signal, i
tillegg til ikon):

| Nivå | border-width | border-style |
|---|---|---|
| Bekreftet | 1px | solid |
| Sannsynlig | 1px | dashed |
| Ikke testet | 1.5px | solid *(endret fra dotted, K2/K3 — se begrunnelse)* |
| Frarådes | 1.5px | solid |

«Ikke testet» sin pillkant er endret fra dotted til solid for å stemme
overens med det reviderte ikonet (kraftig, hel ring — pkt. 2) og for å ikke
motsi seg selv: en tynn prikket pillkant sammen med et kraftig ikon ville gitt
et blandet signal om hvor "tung" merkelappen skal oppleves. Solid kant med
0,5px mer bredde enn Bekreftet/Sannsynlig gir «Ikke testet» en tydelig egen
identitet (bredere, men uten stiplingsrytme) uten å bruke dotted/dashed to
ganger.

CSS-oppskrift for utvikler (erstatter dagens `.tag`/`.t-ok` osv.):

```css
.tag{display:inline-flex;align-items:center;gap:6px;font-size:12.5px;
  font-weight:600;letter-spacing:.01em;line-height:1;
  padding:4px 10px 4px 8px;border-radius:6px;white-space:nowrap}
.tag svg{flex:none;width:14px;height:14px}
.tag-lg{gap:8px;font-size:14.5px;padding:8px 14px 8px 11px;border-radius:8px}
.tag-lg svg{width:18px;height:18px}

.t-ok{color:var(--ok);background:var(--ok-bg);border:1px solid var(--ok-border)}
.t-maybe{color:var(--maybe);background:var(--maybe-bg);border:1px dashed var(--maybe-border)}
.t-none{color:var(--none);background:var(--none-bg);border:1.5px solid var(--none-border)}
.t-no{color:var(--no);background:var(--no-bg);border:1.5px solid var(--no-border)}
```

### 4. Kontrasttabell (WCAG relativ luminans, alfa-komposittert)

Tekst/ikon-farge mot merkelappens EGEN bakgrunn (nivåfarge lagt over
respektiv ink-tone med riktig alfa) — dette er det brukeren faktisk ser:

| Nivå | mot bg-på-`--ink` | mot bg-på-`--ink-2` | mot bg-på-`--ink-3` | AA (≥4,5:1)? |
|---|---|---|---|---|
| Bekreftet | 7,31:1 | 6,67:1 | 6,27:1 | Ja |
| Sannsynlig | 6,78:1 | 6,14:1 | 5,78:1 | Ja |
| **Ikke testet** | **7,69:1** | **6,99:1** | **6,56:1** | **Ja — høyest av de fire** |
| Frarådes | 6,25:1 | 5,72:1 | 5,32:1 | Ja (lavest av de fire, men fortsatt god margin over 4,5:1) |

Kravet fra datakurator — «Ikke testet» skal ha minst samme kontrast som de
andre — er oppfylt med god margin: den er nå den *høyeste*, ikke den laveste.
Avstanden mellom laveste (Frarådes, 5,72) og høyeste (Ikke testet, 6,99) er
liten nok til at ingen av de fire skal oppleves som synlig svakere trykt enn
de andre.

Merkelappens bakgrunnstone (den svake fargede tonen) mot sidebakgrunnen —
dette er *ikke* det som bærer synligheten (se merknad under tabellen):

| Nivå | bg mot `--ink-2` | bg mot `--ink` |
|---|---|---|
| Bekreftet | 1,39:1 | 1,37:1 |
| Sannsynlig | 1,33:1 | 1,30:1 |
| Ikke testet | 1,30:1 | 1,28:1 |
| Frarådes | 1,33:1 | 1,32:1 |

**K3 — rettet.** Forrige versjon av denne tabellen var feil: den sammenlignet
den ugjennomsiktige nivåfargen mot bakgrunnen og ignorerte at kanten faktisk
tegnes med `rgba(..., alfa)` — altså en annen, svakere farge enn den
ugjennomsiktige. Datakurators kontrollberegning (2,50–3,17:1) var riktig, min
opprinnelige tabell (5,7–8,1:1) var det ikke. Tallene under er kanten slik
den faktisk rendres — `rgba()`-verdien komposittert over sidebakgrunnen —
mot samme bakgrunn, med de justerte alfaverdiene fra pkt. 1 (K3, løsning a:
alle kanter løftet til reelt ≥3:1):

| Nivå | kant mot `--ink-2` (reell, med alfa) | kant mot `--ink` (reell, med alfa) | ≥3:1? |
|---|---|---|---|
| Bekreftet | 3,16:1 | 3,26:1 | Ja (alfa uendret, .55, var allerede over) |
| Sannsynlig | 3,35:1 | 3,46:1 | Ja (alfa løftet .5 → .65) |
| Ikke testet | 3,44:1 | 3,55:1 | Ja (alfa løftet .55 → .65) |
| Frarådes | 3,42:1 | 3,59:1 | Ja (alfa løftet .6 → .70) |

Alle fire kanter oppfyller nå WCAG 1.4.11 (ikke-tekst, ≥3:1) mot både `--ink`
og `--ink-2`, med 0,16–0,46 margin. Marginen er bevisst holdt liten (ikke
presset til 5–6:1 slik forrige, feilaktige tabell antydet) — å skru alfaen
mye høyere ville gjort kanten til en tydelig fargeflate og brutt med "ingen
neon"-kravet i CLAUDE.md. Kanten er dermed en reell, men behersket,
formavgrenser — ikke det primære skillesignalet. Det primære skillesignalet
er fortsatt ikonet (form/fyll/tegn), jf. pkt. 5.

Merkelappens bakgrunnstone (fyllet) er separat fra kanten og bæres ikke som
et eget kontrastsignal — den er en svak fargeforsterkning (~1,3:1 mot
sidebakgrunnen, tabellen over), ikke en avgrensning. Det er kanten (nå ≥3:1)
som avgrenser formen, og ikonet + teksten (5,7–7,7:1) som bærer lesbarheten.

`--dim` mot de tre bakgrunnene (erstatter dagens 3,3:1-avvik):

| | `--ink` | `--ink-2` | `--ink-3` |
|---|---|---|---|
| `--dim` #8F877C | 5,27:1 | 4,89:1 | 4,62:1 |

Alle ≥4,5:1 → AA på alle tre flater uten unntaksregel.

### 5. Gråtoneverifisering

Relativ luminans (WCAG, 0–1) og enkel gråtone-luma (0–255, samme metode
testeren brukte i 004) for hvert nivås tekst/ikon-farge:

| Nivå | WCAG-luminans | Gråtoneverdi (0–255) |
|---|---|---|
| Bekreftet | 0,512 | 173 |
| Sannsynlig | 0,444 | 175 |
| Ikke testet | 0,501 | 188 |
| Frarådes | 0,412 | 173 |

**Rettet (K3):** WCAG-luminanskolonnen over var feil i forrige versjon
(0,378/0,375/0,466/0,352). Datakurators kontrollberegning var riktig
(Bekreftet 0,512, Ikke testet 0,501); tallene over er nå kontrollregnet på
nytt og stemmer med det. Gråtoneverdiene (0–255) var allerede riktige og er
uendret.

**Ærlig vurdering:** disse ligger fortsatt tett (173–188 av 255) — å presse
lysstyrken lenger fra hverandre ville enten dratt en av fargene under AA-
kravet eller tvunget frem en falsk hierarki-følelse (som om ett nivå er
"viktigere" enn et annet rent visuelt, noe ingen av nivåene skal være).
Derfor skiller ikke dette forslaget nivåene primært på lysstyrke. Slik
skilles de i ren gråtone, i hovedsak via form/ikon, med kanten (nå reelt
≥3:1, pkt. 4) som sekundær forsterkning:

- **Bekreftet**: hel omriss-sirkel med hake.
- **Sannsynlig**: sirkel, stiplet kant, svakt fylt, tydelig bølge/"≈"
  (revidert i K2 — se pkt. 2 for hvorfor forrige bølge var for flat).
- **Ikke testet**: sirkel, hel kant men kraftigere strøk enn de andre, INGEN
  fyll, INGEN tegn inni (revidert i K2 — forrige prikkede kant + rett strek
  er forkastet, se pkt. 2 for begrunnelse).
- **Frarådes**: trekant — eneste ikke-runde silhuett — tykk kant, fylt,
  utropstegn.

**Om fyllgrad som signal:** datakurator påpekte at forskjellen i
fyll-opasitet mellom Bekreftet (0,18) og Sannsynlig (0,12) er reell i tall,
men ikke synlig nok ved 14px til å regnes som et eget skillesignal. Det
trekkes derfor ut av begrunnelsen: skillet mellom Bekreftet og Sannsynlig
bæres av **haken mot bølgen** (ulikt tegn) og heltrukket mot stiplet kant —
ikke av fyllgrad. Skillet mellom Sannsynlig og Ikke testet bæres nå av at
Ikke testet ikke har noe tegn inni i det hele tatt, mot Sannsynligs synlige
bølge, samt stiplet mot hel kant. Se K4-bildene under for hvordan dette
faktisk ser ut, ikke bare beskrivelsen.

**K4 — rendret bevis.** Skjermbilder av alle fire merkelapper, i gråtone
(CSS `filter:grayscale(1)`, ikke manuelt valgte gråtoner), i 14px (liste) og
18px (detalj), på både `--ink` og `--ink-2`, ved 1x og 2x pikseltetthet,
rendret med `msedge --headless --disable-gpu --force-device-scale-factor`:

- Kildefil: `board/assets/001/preview.html`
- 1x: `board/assets/001/graytone-1x.png`
- 2x: `board/assets/001/graytone-2x.png`

Begge bildene viser samtlige fire nivåer, begge størrelser og begge
bakgrunner i én fil. Datakurator bes godkjenne «skiller seg tydelig i
gråtone» ut fra disse bildene, ikke ut fra beskrivelsen over.

### 6. Begrunnelse per nivå mot kravene

**Bekreftet — stødig, ikke triumferende.** (Ordet «trygg» er tatt ut av denne
begrunnelsen på datakurators anmodning — Bekreftet betyr at setet er fysisk montert i bilen eller oppført i produsentens egen fit-liste,
ikke at barnet er trygt, og ordet skal ikke brukes om noe
tillitsnivå i grensesnittet.) Grønn, men avmettet og med moderat (ikke maks)
kontrast (6,67:1 — det laveste vi trengte var 4,5). Ingen glød, ingen stor
flate. Haken er liten og rolig, ikke et stort "suksess"-checkmark, og er nå
skrevet inn som reservert for dette nivået alene (K5). Formen (heltrukket,
omriss-sirkel med hake) signaliserer "avsluttet/dokumentert" uten å rope det.

**Sannsynlig — synlig usikker.** Stiplet kant, og nå en tydelig, større
bølge (K2 — se pkt. 2/5), er de to formsignalene. Etiketten sier det også
rett ut: «Sannsynlig · utledet» i listen, «Sannsynlig – utledet, ikke
verifisert» i detalj (K1) — dette var påkrevd av CLAUDE.md og manglet i
forrige versjon. Kontrasten er fortsatt høy (6,14:1) — usikkerhet skal vises
gjennom form og tekst, aldri gjennom å gjøre teksten vanskeligere å lese.
Fargen (blå) er valgt bevisst forskjellig fra både grønt og ravgult, slik at
den ikke kan forveksles med "kommer"-merket (`--amber`) andre steder på
siden.

**Ikke testet — nøytral, ikke negativ.** Høyest kontrast av de fire
(6,99:1), samme font-weight (600) som de andre — ingenting ved teksten er
dempet. Ikonet er nå en kraftig, tom ring uten noe tegn inni (K2) — den
forrige rette streken er tatt bort fordi den kunne leses som "forbudt" eller
"minus", altså et negativt svar vi ikke har grunnlag for. En tom form uten
tegn er den mest nøytrale måten å vise "ingen data" på, og strøket er gjort
tykt nok til at ringen ikke ser deaktivert ut. Fargen er en lys, varm
stein-/beige-tone hentet fra samme temperatur som `--mid`/`--bone`, ikke
gråbrunt-dempet som dagens `--none`.

**Frarådes — utvetydig advarsel.** Eneste nivå med trekant (kategorisk
formforskjell fra alle de tre sirkel-baserte nivåene), fylt flate og
utropstegn — et etablert varselsymbol. Rød-oransje med god kontrast (5,72:1,
det laveste av de fire tekst/ikon-verdiene, men fortsatt med solid margin
over 4,5:1-kravet). Skal alltid vises sammen med begrunnelse og kilde, jf.
kravet i CLAUDE.md — det er tekstinnhold, ikke et tokenspørsmål, men nevnes
her fordi merkelappen alene ikke er nok forklaring.

## Datakurators vurdering

### Runde 2 (2026-09-22, datakurator): GODKJENT, med tekstrettelser (R1–R3)

Tokensettet, ikonene og etikettene er godkjent. Vetoet fra runde 1 er
opphevet. R1–R3 under er rettelser i beskrivelsen, ikke i tokens eller
ikoner. PM kan kontrollere dem uten ny runde hos meg, men de skal være gjort
før kortet går til utvikler. Grunnen er at to av dem ellers kan føre utvikler
eller neste oppgave i feil retning.

**Kontrollberegning** med samme metode som i runde 1 (PowerShell, WCAG,
alfa-komposittert):

| Nivå | Tekst (ink / ink-2 / ink-3) | Kant ink-2 / ink | UX oppga for kant |
|---|---|---|---|
| Bekreftet | 7,34 / 6,65 / 6,24 | 3,17 / 3,24 | 3,16 / 3,26 |
| Sannsynlig | 6,75 / 6,13 / 5,75 | 3,34 / 3,46 | 3,35 / 3,46 |
| Ikke testet | 7,70 / 6,98 / 6,54 | 3,43 / 3,55 | 3,44 / 3,55 |
| Frarådes | 6,27 / 5,70 / 5,34 | 3,44 / 3,58 | 3,42 / 3,59 |

Alt stemmer innenfor ±0,03. Alle kanter er ≥3:1 mot `--ink` og `--ink-2`.
Tokens og SVG i `board/assets/001/preview.html` er identiske med leveransen,
så bildene viser det som faktisk er levert. Ett avvik: bølgen i Sannsynlig
er ikke ca. 4,9px høy. Kurvetoppene ligger på y≈8,9 og y≈14,1, altså ca. 5,2
enheter, som gir ca. 3,7px ved 14px. Det er fortsatt godt over kravet på
ca. 2px.

**K1–K5, kontrollert mot bildene** (`graytone-1x.png` og `graytone-2x.png`,
som jeg har sett selv):
- **K1 oppfylt.** «Sannsynlig · utledet» og «Sannsynlig – utledet, ikke
  verifisert» står i selve merkelappen med samme farge og vekt.
- **K2 oppfylt.** Ved 14px og 1x er bølgeikonet litt uklart, men det kan ikke
  forveksles med den tomme ringen. Stiplet kant mot hel kant og ordet
  «utledet» skiller også.
- **K3 oppfylt.** Se tabellen over.
- **K4 oppfylt.** Gråtonekriteriet er oppfylt i praksis. Alle fire kan
  skilles på ikonet alene ved 14px og 1x: hake, bølge, tom ring og trekant.
- **K5 oppfylt i regelteksten.** Parentesen må rettes, se R2.

**(a) Er det greit at «Ikke testet» er visuelt sterkest?** Ja, fra mitt
ståsted. En tydelig «vi vet ikke» fører brukeren mot forsiktighet. Den
overdriver ikke sikkerheten, og det er motsatt av problemet vi hadde i
runde 1. Det er også det vanligste nivået, siden alt starter der, så det skal
ikke kunne overses. En sterk ring overdriver ikke noe. Den eneste måten dette
kan trekke blikket feil vei på, er hvis Frarådes drukner. I gråtone er
Ikke testet noe tyngre enn Frarådes. Frarådes har likevel den eneste
trekanten og er i farger det eneste varme, mettede nivået. Det holder for
godkjenning av tokens. Det skal verifiseres i en realistisk liste, se
kravene til implementasjonen under.

**(b) Stemmer beskrivelsen av Bekreftet med bildet?** Nei. SVG-en har
`fill-opacity="0.18"`, men på bildet ser ikonet ut som en omriss-sirkel med
hake. Fyllet er ikke synlig, verken ved 1x eller 2x. Det samme gjelder
Sannsynlig (0,12) og Frarådes (0,18). Beskrivelsen sier likevel «fylt» flere
steder, og det må rettes (R1). Selve ikonet er godt slik det ser ut.

**Rettelser før overlevering til utvikler (PM kontrollerer):**
- **R1.** Bekreftet skal ikke beskrives som «fylt» (pkt. 2, K5-avsnittet,
  pkt. 5 og pkt. 6). Den skal beskrives som «hel omriss-sirkel med hake».
  Påstanden om at «fyll null er meningsbærende» for Ikke testet i
  innledningen og pkt. 2 fjernes, siden ingen av fyllene synes. Grunn: en
  utvikler som leser «fylt», kan «rette» ikonet til en fylt grønn sirkel, og
  da blir Bekreftet mer triumferende enn godkjent.
- **R2.** K5 skal definere det reserverte merket som *haken*, uansett ramme
  (sirkel, skjold eller ingen ramme), ikke som «fylt sirkel + hakemerke».
  Grunn: med dagens parentes kan logoen i 009 (skjold med hake) hevdes å falle
  utenfor. Setningen etter parentesen er riktig og beholdes.
- **R3.** Pkt. 6 sier «Bekreftet betyr at målene er verifisert». Det er feil
  mot definisjonen. Bekreftet betyr at setet er fysisk montert og verifisert
  i den konkrete bilen, eller oppført i produsentens egen fit-liste. At målene
  stemmer, er grunnlaget for **Sannsynlig**. Rett også tallet for bølgehøyden
  (ca. 3,7px, ikke 4,9px).

**Krav som skal inn i implementasjonsoppgaven (ikke blokkerende for 001):**
- Ordet «utledet» i Sannsynlig skal aldri klippes, skjules eller kortes ned
  med «…» på smal skjerm (360px). Heller linjebryting enn `nowrap` med
  klipping.
- Tester skal se på en realistisk liste der de fleste radene er
  «Ikke testet», med én «Frarådes» og én «Bekreftet», både i farger og i
  gråtone. Frarådes skal fortsatt være det første øyet fanger. Hvis ikke, går
  saken tilbake til UX for å justere ringtykkelsen i Ikke testet.
- Vetoet mot ekte fit-data på grunn av logoen (009) står fortsatt, uavhengig
  av denne godkjenningen.

### Runde 1 (historikk)

**2026-09-22, datakurator. Resultat: VETO.** Kontrasten på «Ikke testet» er
løst. Vetoet gjelder tre nye forhold: «Sannsynlig» er ikke merket som utledet,
«Sannsynlig» og «Ikke testet» flyter sammen i 14px-ikonet, og tabellen over
kantkontrast er feil. Alt kan løses i én runde (K1–K5 under).

Kontrollberegning: jeg har regnet tallene i pkt. 4 og 5 på nytt i PowerShell
(WCAG relativ luminans, alfa-komposittert mot `--ink` #141210, `--ink-2`
#1D1A17, `--ink-3` #231F1B). Det som står om 14px-gjengivelse er utledet av
SVG-geometrien. Jeg har ikke sett det rendret, og det skal heller ikke leses
som om jeg har.

| Nivå | Tekst mot egen bg (ink / ink-2 / ink-3) | Kant mot `--ink-2`, med alfa | UX oppga for kant |
|---|---|---|---|
| Bekreftet | 7,34 / 6,65 / 6,24 | **3,17:1** | 7,52:1 |
| Sannsynlig | 6,75 / 6,13 / 5,75 | **2,50:1** | 6,13:1 |
| Ikke testet | 7,70 / 6,98 / 6,54 | **2,83:1** | 6,32:1 |
| Frarådes | 6,27 / 5,70 / 5,34 | **2,86:1** | 5,69:1 |

Teksttallene stemmer med UX (avvik på ±0,03). Kanttallene stemmer ikke. UX har
tydeligvis regnet kantfargen som ugjennomsiktig og sett bort fra alfaen, selv
om leveransen sier «alfa-komposittert». Luminanskolonnen i pkt. 5 er også feil
(Bekreftet er 0,512, ikke 0,378; Ikke testet er 0,501, ikke 0,466), men
gråtoneverdiene 173–188 stemmer. `--dim` stemmer (5,27 / 4,89 / 4,62).

### 1. Er vetovarselet om «Ikke testet» løst?

**Ja, for det vetovarselet gjaldt.** Teksten og ikonet i «Ikke testet» har
6,98:1 mot `--ink-2`. Det er høyest av de fire, og tallet er kontrollert. Alle
nivåene har samme skriftvekt (600). Det opprinnelige kravet er oppfylt. Kanten
på «Ikke testet» (2,83:1) ligger midt i feltet og er ikke svakest. Det er
«Sannsynlig» som er svakest (2,50:1).

### 2. Leses «Ikke testet» som nøytral?

Fargen og teksten er nøytrale og ikke nedtonet. Det er riktig at ikonet ikke
bruker spørsmålstegn eller kryss. **Den rette streken i sirkelen er likevel
ikke nøytral nok:**
- En sirkel med vannrett strek er formen til skiltet «innkjøring forbudt», og
  vi kjenner den også som minus eller «fjern». Den kan leses som «passer ikke»,
  altså et negativt svar vi ikke har grunnlag for. Det strider mot
  akseptansekriteriet «ikke som feil eller advarsel». Siden har allerede et
  forbudsikon (sirkel med skråstrek, linje 234), og det gjør lesningen
  sterkere.
- Ikonet har minst «blekk» av de fire: tomt, prikket og tynt. Ved 14px blir
  prikkene ca. 1,1px med 2,4px mellomrom. Da kan ringen se blek ut, som et
  deaktivert element. Teksten veier opp for det, men ikonet skal ikke gjøre
  «Ikke testet» til det nivået øyet hopper over.

### 3. Kan Bekreftet og Sannsynlig forveksles? Overdriver Sannsynlig?

- **Bekreftet mot Sannsynlig:** Haken mot bølgen gir et reelt formskille, og
  grønt mot blått holder også ved rød-grønn fargesvikt. På et raskt blikk er
  jeg rimelig trygg på skillet mellom akkurat disse to. Men to av de tre
  signalene UX oppgir er svakere enn beskrevet. Fyllgraden er 0,18 mot 0,12.
  Det er ikke «fylt mot nesten tom», og forskjellen synes ikke. Kanten er
  heltrukket mot stiplet, men den stiplede kanten har 2,50:1, og en stiplet
  sirkel ved 14px (streker på ca. 1,8px) vil se nesten heltrukket ut. **Det
  som faktisk skiller, er haken.**
- **Sannsynlig mot Ikke testet (det egentlige problemet):** Bølgen har ca. 1,65
  enheter fra topp til bunn i viewBox 20. Ved 14px blir det ca. 1,15px, like
  mye som streken er tykk. Bølgen blir da en litt ujevn vannrett strek. Ved
  14px i gråtone er begge ikonene da «sirkel med brutt kant og vannrett strek»,
  med samme gråtone (175 mot 188). Et utledet svar og et manglende svar kan
  altså forveksles i listevisningen.
- **Overdriver Sannsynlig sikkerheten?** Utformingen gjør ikke det, men
  etiketten gjør det. CLAUDE.md sier at Sannsynlig *alltid* skal merkes som
  utledet. Ordet «Sannsynlig» alene leses lett som «ja, antakelig passer den».
  Leveransen har ingen synlig markering av at svaret er utledet.

### 4. Kan vi skille på form, kant og fyll i stedet for lysstyrke?

**Prinsippet er akseptabelt.** Jeg er enig med UX: å skille på lysstyrke ville
lage et falskt hierarki, og det er verre for tilliten. **I praksis er kriteriet
ikke oppfylt ennå.** Kantsignalet har under 3:1 på tre av fire nivåer.
Fyllsignalet er for svakt til å synes. Tegnene i Sannsynlig og Ikke testet
flyter sammen ved 14px. Det eneste som holder sikkert, er trekanten (Frarådes)
og haken (Bekreftet). Kriteriet er dessuten vurdert med argumenter, ikke med
et bilde.

### 5. Kan haken forveksles med logoen (009)?

Ja. Begge er en enkel hake i en lukket ramme i `currentColor`. Det har
betydning. Står logoen i navigasjonen, har hver side et «bekreftet»-merke før
brukeren har valgt bil. Da mister haken i Bekreftet også verdien som eget
signal. **Løsningen er å endre logoen i 009, ikke haken i 001.** Haken skal
tilhøre Bekreftet alene, og ingen annen hake skal brukes noe sted på siden.
Oppgave 001 blokkeres ikke av dette, men vetoet mot ekte data i 009 står.

### 6. Konflikt med definisjonene i CLAUDE.md?

- **Sannsynlig**, «skal alltid merkes som utledet»: dette er brudd, se K1.
- **Ikke testet**, «skal aldri skjules, nedtones»: teksten er i orden. Ikonet
  er i grenseland, se K2.
- **Frarådes**, «alltid begrunnelse og kilde»: UX har nevnt det. Det følges
  opp i implementasjonen.
- **Bekreftet**: UX kaller det «trygg» i begrunnelsen. Bekreftet betyr at
  setet er verifisert å passe, ikke at det er trygt. Ordet «trygg» skal aldri
  stå i grensesnittet om et nivå. Det er ikke et vetopunkt, men skal ikke
  følge med videre.

### Krav til UX (én runde)

- **K1. Sannsynlig skal vise at svaret er utledet.** Det skal stå som synlig
  tekst i selve merkelappen, både i listen og i detaljvisningen, ikke bare
  som tooltip. For eksempel «Sannsynlig · utledet» i listen og «Sannsynlig –
  utledet, ikke verifisert» i detaljen. UX velger ordlyden, men ordet
  «utledet», eller et like tydelig ord, skal stå der.
- **K2. Ikke testet og Sannsynlig skal ha tegn som ikke kan forveksles ved
  14px i gråtone.**
  - Ikke testet: ingen vannrett strek alene, ingen minus, ingen ?, × eller !.
    Ikonet skal ikke ha synlig mindre tyngde enn de tre andre. Tom ring uten
    tegn er akseptabelt for meg, hvis ringen er kraftig nok til å ikke se
    deaktivert ut.
  - Sannsynlig: tegnet skal være tydelig bølget ved 14px, med minst ca. 2px
    fra topp til bunn, eller et annet tegn, for eksempel «≈».
- **K3. Rett kanttabellen med alfa inkludert.** Løs det på en av to måter:
  (a) alle fire kantene får minst 3:1 mot `--ink` og `--ink-2`, eller
  (b) leveransen slutter å bruke kantstilen som bærende signal, og da skal
  ikonene alene skille nivåene i gråtone. Rett også luminanskolonnen i
  pkt. 5. Påstanden om «fylt mot nesten tom» fjernes, eller fyllforskjellen
  gjøres reell.
- **K4. Legg ved rendret bevis.** Bilde av de fire merkelappene side om side,
  helt i gråtone, i 14px (liste) og 18px (detalj), ved 1x og 2x
  pikseltetthet, på `--ink` og `--ink-2`. Akseptansekriteriet «skiller seg
  tydelig i gråtone» godkjennes på bildet, ikke på beskrivelsen.
- **K5. Ingen hake noe annet sted enn i Bekreftet.** Det står som krav i
  leveransen, slik at 009 og senere oppgaver kan vise til det.

Når K1–K5 er levert, vurderer jeg på nytt med én gang. Tekstkontrasten og
fargene i tokensettet kan stå som de er.

## Logg

- 2026-09-08 PM: opprettet
- 2026-09-22 PM: tester fant i 004 at dagens farger (--ok #8FB865, --maybe #7BA7D4,
  --none #8A827A, --no #D9796C) har nesten lik lysstyrke (~131–162 av 255 i gråtone).
  Uten fargesyn blir de vanskelige å skille. Kriteriet «skiller seg i gråtone» er
  altså ikke oppfylt i dag. Ta hensyn til dette.
- 2026-09-22 PM: datakurator påpeker (006) at «Ikke testet» (`--none`) ser nedtonet ut
  og har lavere kontrast enn de andre. Den skal være nøytral, ikke dempet.
- 2026-09-22 PM: datakurator varsler veto mot å vise ekte kompatibilitetsdata før
  «Ikke testet» har minst samme kontrast som de andre nivåene. I dag er merkelappen
  ca. 3,9:1, mot 4,8–6,0:1 for de andre. Oppgaven blokkerer altså ekte data.
- 2026-09-22 PM: tester (006) fant at `.pick small` (feltnavnene i bilvelgeren) bruker `--dim` på `--ink`,
  som gir ca. 3,3:1, under AA. Tokenet `--dim` bør vurderes samlet her.
- 2026-09-22 PM: eier ba om å starte. Flyttet til doing, delegert til UX.
- 2026-09-22 UX: levert tokensett, ikoner, anatomi, kontrasttabell og
  gråtoneverifisering under «UX-leveranse». «Ikke testet» er nå høyest i
  kontrast av de fire (6,99:1 mot 5,72–6,67:1), ikke lavest. `--dim` justert
  til `#8F877C` (≥4,5:1 mot ink/ink-2/ink-3). Skille i gråtone bæres av
  form/kantstil/fyllgrad/ikon, ikke lysstyrke alene — se pkt. 5 for ærlig
  vurdering av det. Klar for datakurator- og testervurdering. Kortet ikke
  flyttet.
- 2026-09-22 PM: UX-leveranse mottatt. Sendt til datakurator for vurdering.
- 2026-09-22 datakurator: VETO. Tidligere vetovarsel om «Ikke testet» er løst
  (6,98:1, kontrollert). Nytt veto: Sannsynlig er ikke merket som utledet
  (CLAUDE.md), tegnene i Sannsynlig og Ikke testet flyter sammen ved 14px, og
  «Ikke testet»-streken kan leses som minus eller forbud. Kanttabellen er feil
  fordi alfa er utelatt (reelt 2,50–3,17:1, ikke 5,7–8,1:1). Krav K1–K5 under
  «Datakurators vurdering». Kortet ikke flyttet.
- 2026-09-22 datakurator: runde 2 GODKJENT. K1–K5 er kontrollert mot
  gråtonebildene, og kontrasttallene er regnet på nytt (kanter 3,17–3,58:1,
  stemmer). Vetoet fra runde 1 er opphevet. Tre tekstrettelser (R1: Bekreftet
  er ikke «fylt», R2: K5 skal reservere haken uansett ramme, R3: Bekreftet er
  ikke «målene verifisert», og bølgen er 3,7px) skal være gjort før kortet går
  til utvikler. PM kontrollerer dem. To krav skal inn i
  implementasjonsoppgaven. Vetoet i 009 står. Kortet ikke flyttet.
- 2026-09-22 UX: rettet K1–K5 i «UX-leveranse» (oppdatert på stedet, ingen ny
  seksjon). K1: «Sannsynlig» viser nå «· utledet» (liste) / «– utledet, ikke
  verifisert» (detalj) i selve merkelappen. K2: ikonene for Sannsynlig
  (tydelig bølge, ≥2px topp-bunn ved 14px) og Ikke testet (kraftig tom ring,
  ingen strek/tegn) er tegnet om. K3: fant og rettet egen regnefeil — kanten
  ble sammenlignet ugjennomsiktig i stedet for med alfa. Kantalfa er løftet
  (Sannsynlig .5→.65, Ikke testet .55→.65, Frarådes .6→.70) slik at alle fire
  nå har reelt ≥3:1 mot `--ink` og `--ink-2` (3,16–3,59:1); luminanskolonnen i
  pkt. 5 er rettet til å stemme med datakurators kontrollberegning; påstanden
  om «fylt mot nesten tom» er fjernet. K4: gråtone-skjermbilder rendret med
  headless Edge (`--force-device-scale-factor`, `filter:grayscale(1)`), lagt
  i `board/assets/001/` (`preview.html`, `graytone-1x.png`, `graytone-2x.png`)
  — utenfor `site/`, ingen nye avhengigheter. K5: skrevet inn som krav at
  haken er reservert for Bekreftet, med henvisning til konflikten med 009.
  Ordet «trygg» er fjernet fra all omtale av Bekreftet. Fargene, tekst-
  kontrasten og `--dim` er ikke endret. `site/` ikke rørt, kortet ikke
  flyttet. Klar for ny vurdering fra datakurator.
- 2026-09-22 PM: datakurator GODKJENT i runde 2. PM har gjort rettelsene R1–R3 i UX-leveransen (beskrivelsen av Bekreftet er nå «hel omriss-sirkel med hake», K5 reserverer haken uansett ramme, definisjonen av Bekreftet er rettet, bølgehøyden er 3,7px). Kriteriene er verifisert av datakurator (kontrast regnet på nytt, gråtonebilder vurdert). Flyttet til done. Implementasjonen er oppgave 011.

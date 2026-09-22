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

## UX-leveranse

Kontrast er beregnet mot den faktiske renderte bakgrunnen (nivåfargen lagt som
`rgba(...)`-tone over `--ink-2`, slik merkelappene faktisk vises i dag inni
`.demo`), ikke mot `--ink-2` rått. Det er derfor tallene her ikke er identiske
med en enkel oppslag av tekstfarge mot `--ink-2`. Alle beregninger er WCAG
relativ luminans, alfa-komposittert i sRGB (slik nettlesere komposittere enkel
`rgba()`-blanding).

Grayton-testen viser at ren lysstyrke ikke skiller de fire nivåene godt nok —
det gjelder også dette forslaget (se pkt. 5). Derfor bærer **form, kantstil og
fyllgrad hovedansvaret** for skillet, ikke farge/lysstyrke. Sirkel vs. trekant
og heltrukket vs. stiplet vs. prikket kant skal kunne skilles selv om skjermen
er helt avmettet.

### 1. CSS-variabler

Direkte erstatning for dagens `--ok/--maybe/--none/--no` + tre nye
kant-variabler per nivå + justert `--dim`. Lim inn i `:root` i
`site/index.html` (linje ca. 16–34), i tillegg til det som står der (line/mid/
bone/amber beholdes uendret):

```css
/* Bekreftet */
--ok:        #7FD16A;
--ok-bg:     rgba(127,209,106,.16);
--ok-border: rgba(107,190,85,.55);

/* Sannsynlig */
--maybe:        #8FB4EA;
--maybe-bg:     rgba(143,180,234,.15);
--maybe-border: rgba(118,155,214,.5);

/* Ikke testet */
--none:        #C2BBAF;
--none-bg:     rgba(194,187,175,.13);
--none-border: rgba(163,155,146,.55);

/* Frarådes */
--no:        #F2937D;
--no-bg:     rgba(242,147,125,.16);
--no-border: rgba(228,115,90,.6);

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

**Bekreftet** — sirkel, heltrukket kant, fylt indre, hake. (Trygg, avsluttet.)
```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <circle cx="10" cy="10" r="8" fill="currentColor" fill-opacity="0.18" stroke="currentColor" stroke-width="1.6"/>
  <path d="M6.4 10.3l2.5 2.4 4.7-5.4" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round" stroke-linejoin="round"/>
</svg>
```

**Sannsynlig** — sirkel, stiplet kant, svakt fylt, bølgelinje ("omtrent").
```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <circle cx="10" cy="10" r="8" fill="currentColor" fill-opacity="0.12" stroke="currentColor" stroke-width="1.6" stroke-dasharray="2.6 2.2"/>
  <path d="M5.7 10.6c.9-1.1 1.9-1.1 2.8 0s1.9 1.1 2.8 0 1.9-1.1 2.8 0" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round"/>
</svg>
```

**Ikke testet** — sirkel, prikket kant, IKKE fylt, rett strek ("ingen verdi
registrert" — bevisst nøytral, ikke spørsmålstegn som kan lese som forvirring).
```html
<svg viewBox="0 0 20 20" width="14" height="14" aria-hidden="true">
  <circle cx="10" cy="10" r="8" fill="none" stroke="currentColor" stroke-width="1.6" stroke-dasharray="0.2 3.4" stroke-linecap="round"/>
  <path d="M6.8 10h6.4" fill="none" stroke="currentColor" stroke-width="1.8" stroke-linecap="round"/>
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

### 3. Etiketter og merkelappens anatomi

Etikettekst uendret: **Bekreftet**, **Sannsynlig**, **Ikke testet**,
**Frarådes**.

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
| Ikke testet | 1.5px | dotted |
| Frarådes | 1.5px | solid |

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
.t-none{color:var(--none);background:var(--none-bg);border:1.5px dotted var(--none-border)}
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

Kanten (border) mot sidebakgrunnen, som er det som faktisk avgrenser
merkelappen som form (WCAG 1.4.11, ikke-tekst, krav ≥3:1):

| Nivå | kant mot `--ink-2` | kant mot `--ink` |
|---|---|---|
| Bekreftet | 7,52:1 | 8,12:1 |
| Sannsynlig | 6,13:1 | 6,61:1 |
| Ikke testet | 6,32:1 | 6,82:1 |
| Frarådes | 5,69:1 | 6,14:1 |

**Merknad:** den svakt fargede fyll-tonen alene skiller seg lite fra
sidebakgrunnen (rundt 1,3:1) — det er bevisst, for å unngå fargede "klosser"
som bryter med den mørke, rolige paletten. Det er **kanten** som avgrenser
formen (5,7–8,1:1, godt over AA-kravet på 3:1) og **ikonet + teksten** som
bærer lesbarheten (5,7–7,7:1, godt over 4,5:1). Fyll-tonen er en svak
signal-forsterkning, ikke en bærende kontrastkilde.

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
| Bekreftet | 0,378 | 173 |
| Sannsynlig | 0,375 | 175 |
| Ikke testet | 0,466 | 188 |
| Frarådes | 0,352 | 173 |

**Ærlig vurdering:** disse ligger fortsatt tett (173–188 av 255) — å presse
lysstyrken lenger fra hverandre ville enten dratt en av fargene under AA-
kravet eller tvunget frem en falsk hierarki-følelse (som om ett nivå er
"viktigere" enn et annet rent visuelt, noe ingen av nivåene skal være).
Derfor skiller ikke dette forslaget nivåene primært på lysstyrke. Slik
skilles de i ren gråtone, kun via form:

- **Bekreftet**: sirkel, heltrukket tynn kant, fylt midtflate, hake-tegn.
- **Sannsynlig**: sirkel, stiplet kant (segmenter), svak fyll, bølgelinje.
- **Ikke testet**: sirkel, prikket kant (tette prikker — annen rytme enn
  Sannsynlig sin stipling), ingen fyll (tom), rett vannrett strek.
- **Frarådes**: trekant — eneste ikke-runde silhuett — tykk kant, fylt,
  utropstegn.

Bekreftet og Sannsynlig kan ikke forveksles selv i gråtone: heltrukket kant +
fylt + hake vs. stiplet kant + nesten tom + bølgelinje er to helt ulike
strekmønstre på nært hold, og formen er sirkel i begge, så det er kantstil +
fyllgrad + tegn som gjør jobben, ikke fargen.

### 6. Begrunnelse per nivå mot kravene

**Bekreftet — trygg, ikke triumferende.** Grønn, men avmettet og med
moderat (ikke maks) kontrast (6,67:1 — det laveste vi trengte var 4,5).
Ingen glød, ingen stor flate. Haken er liten og rolig, ikke et stort
"suksess"-checkmark. Formen (heltrukket, fylt sirkel) signaliserer
"avsluttet/dokumentert" uten å rope det.

**Sannsynlig — synlig usikker.** Stiplet kant er det klareste "dette er ikke
ferdig verifisert"-signalet vi har i grensesnittsspråk, og bølgelinjen leses
som "omtrent/utledet". Kontrasten er fortsatt høy (6,14:1) — usikkerhet skal
vises gjennom form, aldri gjennom å gjøre teksten vanskeligere å lese.
Fargen (blå) er valgt bevisst forskjellig fra både grønt og ravgult, slik at
den ikke kan forveksles med "kommer"-merket (`--amber`) andre steder på
siden.

**Ikke testet — nøytral, ikke negativ.** Høyest kontrast av de fire
(6,99:1), samme font-weight (600) som de andre — ingenting ved teksten er
dempet. Ikonet er tomt (ufylt sirkel) og bruker en rett strek, ikke et
spørsmålstegn eller kryss, for å unngå at "vi vet ikke" leses som et
problem. Fargen er en lys, varm stein-/beige-tone hentet fra samme
temperatur som `--mid`/`--bone`, ikke gråbrunt-dempet som dagens `--none`.

**Frarådes — utvetydig advarsel.** Eneste nivå med trekant (kategorisk
formforskjell, ikke bare kantstil), tykkere kant (1,5px mot 1px), fylt
flate og utropstegn — et etablert varselsymbol. Rød-oransje med god
kontrast (5,72:1, det laveste av de fire, men fortsatt trygt over
4,5:1-kravet). Skal alltid vises sammen med begrunnelse og kilde, jf.
kravet i CLAUDE.md — det er tekstinnhold, ikke et tokenspørsmål, men nevnes
her fordi merkelappen alene ikke er nok forklaring.

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

# baksetet.no

Uavhengig, ikke-kommersiell norsk tjeneste som hjelper foreldre å finne ut
hvilke barneseter som passer i deres konkrete bil.

Ingen annonser. Ingen affiliate. Ingen sponsede plasseringer.

Kompatibilitetsvurderinger bruker fire tillitsnivåer — aldri binært ja/nei:
**Bekreftet**, **Sannsynlig**, **Ikke testet**, **Frarådes**. "Ikke testet"
er et gyldig og viktig svar, og skjules aldri.

## Status

Landingsside publisert via GitHub Pages fra `site/`. Foreløpig adresse:
https://richardkarlsen.github.io/baksetet/ — eget domene kommer senere.

## Teknisk

- Statisk nettsted i `site/`. `site/index.html` er selvstendig, ingen
  byggesteg.
- Ingen eksterne avhengigheter utover Google Fonts (Archivo) og Tally-embed.
- Publisering skjer med en GitHub Actions-workflow
  (`.github/workflows/pages.yml`) som laster opp `site/` som Pages-artefakt.

Se `CLAUDE.md` for produktprinsipper og `board/` for oppgavestatus.

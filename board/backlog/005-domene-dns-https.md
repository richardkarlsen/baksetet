---
id: 005
tittel: Koble baksetet.no til GitHub Pages med HTTPS
rolle: utvikler
prioritet: middels
avhenger_av: [004]
kurator_kreves: false
blokkert_av: eier må registrere domenet først
---

## Hvorfor

`github.io`-adressen fungerer teknisk, men et eget domene er nødvendig for at
siden skal oppleves som en troverdig, uavhengig kilde.

## Hva

Peke `baksetet.no` mot GitHub Pages og få automatisk SSL på plass.

`baksetet.no` er et apex-domene, og apex kan ikke bruke CNAME. Det betyr
A-records mot GitHubs IP-adresser, eller ALIAS/ANAME hvis registraren støtter
det. Sjekk hva registraren tilbyr før du velger.

## Akseptansekriterier

- [ ] Apex `baksetet.no` peker mot GitHub Pages (A-records eller ALIAS)
- [ ] `www.baksetet.no` er CNAME mot `<bruker>.github.io` og redirecter til apex
- [ ] `CNAME`-fil i repoet med domenet
- [ ] Sertifikat utstedt og "Enforce HTTPS" er huket av
- [ ] Eventuelle CAA-records tillater Let's Encrypt
- [ ] Hvis Cloudflare brukes: proxy er slått AV på recordene mot GitHub
- [ ] Både `http://` og `www` ender på `https://baksetet.no`

## Kjente fallgruver

- Sertifikat kan henge. Fiks: fjern domenet i Pages-innstillingene og legg det
  inn på nytt for å trigge ny provisjonering.
- Lang TTL forsinker feilsøking. Sett lav TTL mens du jobber.

## Utenfor scope

Selve domeneregistreringen. Eier gjør det.

## Logg

- 2026-09-09 PM: opprettet, blokkert på domeneregistrering

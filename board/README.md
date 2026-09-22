# Board

Kortene er filer. Mappen kortet ligger i, er statusen. Flytt filen for å
endre status:

    backlog/  ikke prioritert ennå
    todo/     klar, har akseptansekriterier, kan startes
    doing/    en agent jobber på den nå
    review/   levert, venter på test eller kurator-godkjenning
    done/     verifisert ferdig

Kun prosjektleder flytter kort. Git gir historikken.

Filnavn: `<id>-<kort-slug>.md`, f.eks. `004-filter-paa-bilmodell.md`

# Dose Daemon — contentfeed

Deze repo serveert de dynamische content van [Dose Daemon](https://github.com/ogerik/dose-daemon):
tips, daemon-zinnen, aankondigingen, feature-vlaggen en vertaal-overrides.

**Live op:** https://dose.ogerik.io/content-v1.json

## Waarom een aparte, publieke repo

De app-repo is privé. `raw.githubusercontent.com` weigert daardoor elk verzoek
zonder token, en de app kreeg dus stelselmatig een 404 op zijn contentfeed —
maandenlang onopgemerkt, omdat hij netjes terugvalt op de gebundelde kopie in
`assets/content/`.

Een medicatie-app hoort geen API-sleutel mee te dragen om zijn eigen teksten op
te halen, en de content bevat niets vertrouwelijks. Dus staat hij hier: publiek,
zonder authenticatie, geserveerd door GitHub Pages over hun CDN.

## Iets wijzigen

Bewerk `content-v1.json`, commit, push. Pages publiceert binnen een minuut.

De app haalt de feed op bij het opstarten en bij terugkeer uit de achtergrond,
cachet het resultaat lokaal, en valt bij twijfel terug op de gebundelde kopie.
Een fout in dit bestand maakt de app dus niet stuk — hij negeert het en gebruikt
wat hij al had.

**Let op:** houd de sleutelstructuur intact. `test/` in de app-repo bewaakt dat de
vijf talen dezelfde sleutelset houden en dat er geen schuld-taal in de teksten
sluipt; die tests draaien op de gebundelde kopie, niet op deze.

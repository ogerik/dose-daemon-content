# Dose Daemon — contentfeed en publieke pagina's

Deze repo serveert twee dingen voor [Dose Daemon](https://github.com/ogerik/dose-daemon):

1. **De contentfeed** — tips, daemon-zinnen, aankondigingen, feature-vlaggen en
   vertaal-overrides, in `content-v1.json`.
2. **De publieke documenten** die Apple en Google voor een gezondheidsapp
   verlangen, en waar de app zelf naar verwijst.

**Live op:**

| URL | Bestand |
|---|---|
| https://dose.ogerik.io/ | `index.html` |
| https://dose.ogerik.io/privacy | `privacy/index.html` |
| https://dose.ogerik.io/voorwaarden | `voorwaarden/index.html` |
| https://dose.ogerik.io/support | `support/index.html` |
| https://dose.ogerik.io/content-v1.json | `content-v1.json` |

De pagina's zijn losse HTML-bestanden met één gedeelde `stijl.css`. Geen build,
geen framework, geen afhankelijkheden: `.nojekyll` staat aan, dus GitHub Pages
serveert ze zoals ze hier staan.

## De voorwaarden zijn nog concept

`voorwaarden/index.html` draagt bovenaan een zichtbare melding dat de tekst nog
niet door een jurist is nagekeken. **Die melding blijft staan tot dat gebeurd is.**
Vóór de eerste publieke uitgave moeten de voorwaarden, de medische positionering
en de aansprakelijkheidsclausule beoordeeld zijn op consumentenrecht en op de
vraag of deze dienst onder regelgeving voor medische hulpmiddelen valt.

## Als je de teksten aanpast

De privacyverklaring beschrijft wat de app **werkelijk** doet, tot op het niveau
van welke velden er in de telemetrie-payload zitten. Verandert
`lib/model/telemetry_service.dart` in de app-repo, dan verandert deze pagina mee.
Loopt dat uit de pas, dan staat er een privacyverklaring die niet klopt, en dat is
erger dan geen.

De voorwaarden dragen een heel versienummer. Verhoog het bij elke inhoudelijke
wijziging: de app blokkeert de medicatiebediening tot de gebruiker opnieuw
akkoord is gegaan, en dat werkt alleen als het nummer meebeweegt.

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

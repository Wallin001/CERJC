# RJC Fleet Availability — KLM Cityhopper E175/E190

Dit is een compact analysescript dat de "fleet availability" laat zien van
een klein aantal Embraer E175/E190-toestellen van KLM Cityhopper. Deze
specifieke toestellen krijgen line- en hangaaronderhoud bij **Regional Jet
Center (RJC)** op Schiphol — door hun vluchtgeschiedenis te volgen,
analyseren we vliegtuigen die letterlijk bij RJC langskomen voor onderhoud.

**Databron:** [OpenSky Network REST API](https://opensky-network.org/apidoc/)
(gratis). Het endpoint `/flights/aircraft` vereist sinds 2025 een gratis
OAuth2-account (client_id + client_secret, aan te vragen via de OpenSky
account-pagina).

**Waarom relevant voor RJC:** fleet availability (grondtijd vs. vliegtijd)
hangt direct samen met RJC's onderhoudsplanning en -capaciteit. Hoe meer een
toestel vliegt, hoe minder tijd er overblijft voor gepland onderhoud, en hoe
krapper RJC de hangaarcapaciteit moet inplannen rond de operationele vloot
van KLM Cityhopper.

## Gebruik

```bash
pip install -r requirements.txt

# Optioneel maar aanbevolen voor echte data (anders wordt voorbeelddata gebruikt):
cp .env.example .env
# open .env in een editor en vul je eigen client_id/secret in (nooit committen!)

python fleet_availability.py
```

Credentials aanvragen: log in op [opensky-network.org](https://opensky-network.org),
ga naar je Account-pagina, en maak rechtsonder bij "API Client" een nieuwe
client aan. De Client ID staat op de pagina; de Client Secret wordt gedownload
als `credentials.json` (wordt maar één keer getoond). Zet beide waarden in je
lokale `.env`-bestand — dat staat al in `.gitignore` en wordt dus nooit
gecommit of gedeeld.

Dit genereert `fleet_availability.html` — een los, interactief HTML-bestand
met een bar chart van vliegtijd/grondtijd/utilisatie per toestel per dag
(afgelopen 7 dagen), met hover-tooltips die elk cijfer uitleggen. Open het
bestand direct in een browser; er is geen notebook of server nodig.

## Toestellen

| ICAO24 | Registratie | Type |
|---|---|---|
| 485206 | PH-EXE | Embraer E190 |
| 485875 | PH-EXY | Embraer E190 |
| 48548c | PH-EXK | Embraer E175 |

Hex-codes geverifieerd via de OpenSky/hexdb.io vliegtuigregisterdatabase.

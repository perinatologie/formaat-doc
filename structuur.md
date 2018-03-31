---
id: structuur
---

# VEROUDERDE INFORMATIE

## Structuur

Dit formaat bevat 1 client element, met daarbinnen een reeks ‘value’ elementen, welke informatie over de client bevatten.

Elke value element bevat een `label` attribuut (tbv eenvoudige weergave), een daadwerkelijke `value` attribuut, en in veel gevallen een “keyid”.

Om de informatie te tonen volstaat het dus om door de value elementen te lopen, en ovv label en value de informatie aan de gebruiker te tonen.

Voor verdere integratie is er de mogelijkheid om de labels te negeren, en te kijken naar de keyids. Obv de keyid kan er een mapping worden gemaakt daar velden in het ontvangende systeem, om hiermee de locale informatie bij te werken.

Binnen elk client element zit 1 `eocs` element, met hier binnen een of meerdere `eoc` (episode of care) elementen.

Binnen deze eoc elementen zitten binnen het forms element weer een of meerdere form elementen. Deze form elementen worden gebruikt om de data per onderwerp te groeperen.

Ook hier kan ter weergave het label attribuut worden gebruikt, en optioneel voor verdere integratie obv keyid een mapping worden gedaan.


In de volgende hoofdstukken worden de volgende concepten toegelicht:

* resource: Elk bestand bevat 1 resource (document, dossier, zwangerschap).
* section: Een resource bevat 1 of meerdere sections
* value: Elke section bevat 1 of meerdere values

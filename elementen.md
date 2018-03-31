---
id: elementen
---

## Elementen

### Het `resource` element
Binnen dit element bestaan de volgende attributen:
* type (verplicht): het type resource. Meest voorkomende waarde `hub/dossier`

Dit element is het root element van een hub resource document.

### Het `section` element
Binnen het root `resource` element bestaan een of meerdere `section` elementen.
Dit wordt gebruikt om een document onder te verdelen in logische onderdelen.

Enkele voorbeeld section types:
* client: client informatie zoals naam, adres, woonplaats
* intake: uitgebreide intake gegevens
* zwangerschap.consult: een zwangerschaps consult, kan 0, 1 of meerdere keren voorkomen.
* baring.consult: baring consult gegevens, kan 0, 1 of meerdere keren voorkomen.

Waar nodig kunnen deze typen na overeenkomst deelnemers worden aangevuld.

Dit element bevat de volgende attributen

* Id (verplicht): unieke id voor deze section binnen 1 resource.
* type (optioneel): het type section. Voor weergave is dit attribuut niet vereist. Wanneer gegevens overgenomen of “inline” in een dossier getoond dienen te worden, dan is dit attribuut wel nodig.
* label (verplicht): Tbv weergave doeleinden.
* uuid (optioneel): Wanneer het record binnen het systeem van de verzender een eenduidige unieke identificatie heeft kan dit attribuut worden ingevuld. Alleen nodig igv van overname gegevens, om duplicatie tegen te gaan.
* createStamp (verplicht): wanneer het record is aangemaakt in betreffend record/section in bron systeem. Tbv weergave doeleinden. Bevat een unix timestamp.
* updateStamp (optioneel): laatste wijziging van betreffende record/section in bron systeem. Bevat een unix timestamp.
* effectStamp (optioneel): moment waarop deze section betrekking heeft. Bij een consult is dit bijvoorbeeld de consult-datum. Bevat een unix timestamp.

### Het `value` element

Binnen de `section` elementen bestaan een of meerdere `value` elementen.
De value elementen bevatten de daadwerkelijke gegevens.

Dit element bevat de volgende attributen
* label (verplicht): Label voor weergave doeleinden.
* value (verplicht): De waarde zoals geregistreerd in het bronsysteem. Wanneer het om een codelijst gaat staat hier de code (niet de tekst representatie).
* displayValue (optioneel): Waarde tbv weergave eindgebruiker. Wanneer de value een code betreft staat hier de voluit geschreven waarde. Wanneer dit attribuut leeg is zal de originele `value` worden getoond. In geval van tekst values kan dit veld daarom ook worden leeg gelaten.
* concept (optioneel): verwijzing naar gestandaardiseerd data element. Vul hier bv `peri22-dataelement-10030` in wanneer er een BSN gecommuniceerd wordt. Alleen nodig indien het doel is om gegevens over te nemen/verwerken. Voor dossier weergave is dit veld niet vereist.
* keyid (optioneel): verwijzing naar key id’s in spreadsheet “Dataset overzicht aansluting Hub”. Wij proberen de keyid’s uit te faseren en in plaats hiervan alleen gebruik te maken van het concept attribuut.

## concept, keyid, of allebij?
Het doel van de `concept` en `keyid` attributen zijn vergelijkbaar. Deelnemers volgen zoveel mogelijk gestandaardiseerde data elementen door gebruik te maken van het `concept` attribuut en hier `peri-dataelement-*` id’s in te geven.

Tbv flexibele uitwisseling zijn er binnen het samenwerkingsverband in een vroeger tijdstip ook `keyid`s afgesproken. Wanneer het voor beide leveranciers eenvoudiger is om een `keyid` te communiceren ipv (of naast) een `concept`, dan blijft deze optie bestaan.

Maar het advies is om vooral gebruik te maken van het `concept` attribuut. Zowel `keyid` als `concept` kunnen worden ingegeven wanneer deze bekend zijn, en aansluiten.

Er wordt gewerkt aan een mapping tabel tussen keyids en elementen uit de peri22- dataset waar een een-op-een mapping mogelijk is.


## Repeat IDs
Er zijn situaties te bedenken waarin een value binnen 1 section meerdere malen voorkomt. Denk bijvoorbeeld aan een section `zwangerschap.consult` bij een meerling. Dan kan de value voor ligging 2 keer voorkomen (1 per foetus). Voeg in dat geval een attribuut `repeatid` toe aan elk betreffend value element, beginnend bij 0, oplopend per value element van zelfde type (obv keyid of element attribuut).

Bijvoorbeeld zwangerschaps consult voor een meerling:

```xml
<section type=”zwangerschap.consult”>
  <value
    label=”AM duur”
    value=”20+3”
    concept=”peri22-dataelement-82316”
    keyid=”amduur” />
  <value
    label=”IUVD”
    value=”nee”
    concept=”peri22-dataelement-20410”
    repeat=”0” />
  <value
    label=”IUVD”
    value=”nee”
    concept=”peri22-dataelement-20410”
    repeat=”1” />
</section>
```

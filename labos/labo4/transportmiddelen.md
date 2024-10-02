# Transportmiddelen

Maak een nieuw project aan met de naam `transportmiddelen` .

**Gebruik voor deze oefening class en interface, geen object literals!**

Maak een interface Voertuig, deze bevat:

* property naam (string)
* property brandstof (Brandstof)
* methode rijden()

Maak voor de brandstof property een nieuwe `type Brandstof` aan met types : BENZINE, ELEKTRISCH, GEEN :  zie naar de [String union](../../cursus/wat-is-nodejs/type-systeem/basic-types.md#union-types) .

Maak vervolgens twee classes aan : Auto en Fiets en implementeer de Voertuig interface.

De methode rijden() toont volgende tekst:

* bij auto : ${naam} rijdt op de weg met brandstof ${brandstof}
* bij fiets : ${naam} rijdt op het fietspad met brandstof ${brandstof}

Maak vervolgens meerdere instanties aan van beide classes bv: bmw, tesla, koersfiets, speedelec en toon voor elke instantie de rijden() methode in de console.

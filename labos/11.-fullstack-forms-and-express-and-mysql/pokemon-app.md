# Pokémon app

Het doel van deze oefening is een app te maken die bijhoudt welke Pokémon je gevangen hebt. Hiervoor maken we eerst een overzicht van alle Pokémon. Je kan op een Pokémon aanduiden dat je deze gevangen hebt. Deze actie wordt doorgegeven aan de server die dit in de database bijhoudt. Op een ander scherm kunnen we dan het overzicht van alle Pokémon die je al gevangen hebt opvragen. Hier kan je dan aanduiden dat de Pokémon terug vrijgelaten wordt.

Maak nieuwe projecten poke-client en poke-server aan.

De client is een VITE app, de server is een node.js / express app.

Op de server voorzie je get , post en delete routes:

* GET : vraag alle Pokémon op vanuit je database en geef het resultaat terug in JSON
* POST : voeg één Pokémon toe aan je database
* DELETE : verwijder één Pokémon uit je database

In de client maak je twee overzichten : overview en owned

De externe API om Pokémon op te vragen is deze:

[https://pokeapi.co/api/v2/pokemon?limit=\<pageSize>\&offset=\<pageOffset](https://pokeapi.co/api/v2/pokemon?limit=%3cpageSize%3e\&offset=%3cpageOffset)>

Je hebt dus twee variabelen nodig : pageSize en pageOffset.

* pageSize = het aantal resultaten dat je terug wil krijgen, bv 20
* pageOffset = vanaf welke rij wil je de resultaten terug.

Met die pageOffset kan je paging bouwen. Bijvoorbeeld voor een pageSize van 20 geef het volgende offsets door:

* pagina 1 => offset = 0
* pagina 2 => offset = 20
* pagina 3 => offset = 40
* pagina X => offset = (pageSize \* (page – 1))

Het antwoord van deze API bevat o.a. elementen count en results.

* count = totaal aantal records in de online database
* results = een lijst van Pokémon, enkel name en url

In de afhandeling van het antwoord van deze API zal je opnieuw een fetch request moeten doen met de url van het antwoord uit de eerste request.

De url is bijvoorbeeld :

[https://pokeapi.co/api/v2/pokemon/1](https://pokeapi.co/api/v2/pokemon/1)

Die ‘1’ is de index van de Pokémon.

Deze request geeft héél véél data terug. Belangrijke onderdelen van het antwoord zijn: id, name en sprites.

* id : de volgnummer van de Pokémon
* name : de naam
* sprites : afbeeldingen van de Pokémon

Je kan er uiteraard nog veel meer gegevens uithalen. Kies maar wat je nog nuttig lijkt.

Om dit dan uiteindelijk op het scherm te krijgen, gebruik je bijvoorbeeld cards ([https://www.w3schools.com/howto/howto\_css\_cards.asp](https://www.w3schools.com/howto/howto_css_cards.asp))

Zet op je card ook nog een knop 'gevangen'. Deze knop stuurt dan (minstens) de ‘id’ van de Pokémon naar de server. Eventueel nog extra gegevens, zoals bv naam. Dit stockeer je in de database

De owned tabel toont alle Pokémon die je al gevangen hebt. Je zal van de server de id’s, en eventueel nog extra info die je hebt doorgestuurd, terug krijgen. Met die id’s kan je opnieuw de GET request van hierboven uitvoeren : [https://pokeapi.co/api/v2/pokemon/\<id](https://pokeapi.co/api/v2/pokemon/%3Cid)> , je moet enkel de ‘id’ invullen. Nadien kan je het antwoord op dezelfde manier als het vorige scherm afhandelen om de gevangen Pokémon op je scherm te tonen.

In de owned cards zet je dan een knop 'vrij laten' die de Pokémon terug los laat (= delete in database).



**Extra:**

Zorg ervoor dat de 'gevangen' knop niet zichtbaar is in het overzicht van alle Pokémon als je deze al eens gevangen hebt.

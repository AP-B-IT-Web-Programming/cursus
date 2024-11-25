# Reiskosten server

Maak een toepassing om de kosten van je reizen te noteren.&#x20;

Je wilt elke reis die je maakt in kunnen voeren en nadien aan deze reis kosten koppelen.

Maak om te beginnen een nieuwe class Reis aan. Een reis heeft vier velden : id, bestemming, jaar en kosten. Bij aanmaken van een Reis object moet je de velden id, bestemming en jaar verplicht meegeven. Het veld kosten is bij aanmaak een lege array.

Maak vervolgens een nieuwe class Kost aan. Een kost heeft twee velden : uitgave en prijs. Beide velden moeten verplicht ingevuld worden bij aanmaak van de kost.

Voorzie een extra functie op je Reis en Kost class : toJSON() . Deze functie maakt een JSON object aan met de waardes in de Reis / Kost class.

We werken zonder database dus voorzie een interne array om je reis object in te bewaren.

Maak volgende routes aan. Gebruik een router class : reizen\_api.ts om onderstaande routes in samen te brengen.

* .get “/reizen” : deze route geeft alle reizen uit de database in JSON formaat terug
* .post “/reis” : deze route maakt één reis aan in de database. De reis wordt in JSON formaat doorgestuurd: {“bestemming” : “Londen”, “jaar” : 2024}\
  Zet deze JSON gegevens om naar een Reis object. Hou er rekening mee dat je een id moet meegeven aan de reis. Voorzie hiervoor een oplossing via een teller.
* .get “/reis/:reisid” : deze route vraagt één reis op adhv de request parameter ‘reisid’.
* .post “/reis/:reisid/kost” : deze route maakt één kost aan voor een reis met de reisid. De kost wordt in JSON formaat doorgestuurd: {“uitgave”: “treintickets”, “prijs” : 100}. Zet deze JSON gegevens om naar een Kost object en voeg dit object toe aan de kosten array van het reisobject.
* .get “/reis/:reisid/kosten” : deze route berekent het totaal aan kosten voor de reis met de reisid. Tel voor de betreffende reis de prijs van alle kosten op en geef enkel dat totaal bedrag terug als antwoord.

Test je server via Postman.


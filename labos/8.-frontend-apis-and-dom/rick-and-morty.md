# Rick and Morty

Het doel van deze oefening is om een applicatie te bouwen voor het tonen van alle personages uit de tekenfilmserie ‘Rick and Morty’.

Hiervoor gebruiken we de externe API : [https://rickandmortyapi.com/api/character?page=${page}\&name=${name}](https://rickandmortyapi.com/api/character?page=$%7bpage%7d\&name=$%7bname%7d)

De API heeft 2 parameters: page (default = 1) en name (default = “”).

De API antwoordt met volgende JSON:

{

"info":{"count": 826,"pages": 42},

"results":

\[

{"id":1, "name":"Rick Sanchez", "status":"Alive", "species":"Human", "gender":"Male", "image":"https://rickandmortyapi.com/api/character/avatar/1.jpeg", "created":"2017-11-04T18:48:46.250Z"},

{"id":2, "name":"Morty Smith", "status":"Alive", "species":"Human", "gender":"Male", "image":"https://rickandmortyapi.com/api/character/avatar/2.jpeg", "created":"2017-11-04T18:50:21.651Z"},

…

]

}

&#x20;

&#x20;

Opdrachten:

1\.    Toon de resultaten van de API in een lijst.

2\.    Voeg filtering toe:

a.    voorzie een invulveld

b.    voeg een zoeken knop toe

c.     als je op de zoeken knop drukt, dan voer je de API opnieuw uit en geeft de ingevulde waarde mee in ‘name’

3\.    Voeg paginering toe:

a.    toon het aantal resultaten

b.    toon de huidige pagina

c.     toon het max aantal paginas

d.    voeg knoppen vorige / volgende toe

e.    telkens dat op de knop gedrukt wordt, voer je de API opnieuw uit met de aangepaste pagina in ‘page’

f.      zorg ervoor dat je knoppen actief/inactief worden als er geen vorige/volgende pagina is

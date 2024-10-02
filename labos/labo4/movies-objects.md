# Movies

Maak een nieuw project aan met de naam `movies`.

**Voor deze opdracht kies je zelf of je met object literal / interface of class werkt.**

Maak een `Movie` object (class of interface) met volgende properties:

* title (string)
* year (number)
* actors (string\[])
* metascore (number)
* seen (boolean)

Maak een instantie aan myFavoriteMovie en gebruik het object Movie. Geef de informatie over jouw favoriete film.

Maak een tweede instantie aan myWorstMovie en geef de info over jouw meest gehate film.

Print beide films af in de console.

## Voorbeeld interactie

```bash
My favorite movie:
The Empire Strikes Back (1980)
Actors: Mark Hamill, Harrison Ford, Carrie Fisher
Metascore: 82
Seen: YES

My worst movie:
The Rise of Skywalker (2019)
Actors: Daisy Ridley, Adam Driver, John Boyega
Metascore: 53
Seen: YES
```

Maak nog een derde film `myLastMovie` aan met de informatie over je laatst bekeken film.

Schrijf nu volgende drie functies:

1. de functie `wasMovieMadeInThe90s`:

* met de parameter movie van het type Movie
* met return waarde true als de film in de jaren 90 gemaakt is, anders false

Voer deze functie uit voor je drie films

2. de functie `averageMetaScore`

* met de parameter movies die een array van het type Movie bevat
* met return waarde de gemiddelde score van alle films in die array

Maak een array aan met jouw drie films en voer deze functie uit

3. de functie `fakeMetaScore`

* met de parameters
  * movie van het type Movie
  * newscore die een nieuwe score bevat
* met return waarde een nieuw Movie object met de nieuwe score


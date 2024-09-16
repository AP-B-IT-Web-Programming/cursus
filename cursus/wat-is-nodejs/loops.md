# Loops

Van zodra eenzelfde stuk code meermaals uitgevoerd moet worden spreken we over een loop.

Er zijn twee soorten loops die we hier zullen bespreken : for loop en while loop

## for loop

```javascript
for (let index : number = 0 ; index < 10 ; index++) {
    console.log(index);
}
```

Typisch aan een for loop is dat we met een index werken. De loop bestaat uit drie onderdelen

* initialisatie : let index : number = 0 -> het beginpunt van onze loop wordt vastgelegd
* conditie : index < 10 -> zolang de conditie waar is, blijft de loop verder uitgevoerd worden
* iteratie : index++ -> deze operatie wordt uitgevoerd op het einde van elke iteratie

In bovenstaand voorbeeld zal de loop 10x uitgevoerd worden. In de console zullen we nummers 0 tot en met 9 zien. Dit komt omdat het verhogen van de index (index++) pas op het einde , dus na de console.log, wordt uitgevoerd.

## for of loop

Dit is een variant van de for loop die we vooral bij het verwerken van Arrays terug zien komen.

```javascript
const planets : string[] : ['Mercury', 'Venus', 'Earth', 'Mars'];
for (let planet : string of planets) {
    console.log(planet);
}
```

De for of loop wordt uitgevoerd voor elk element van de array. Er is geen initialisatie, conditie of iteratie.

Deze loop is zeer handig om snel over alle elementen van de array te gaan als de index niet belangrijk is.

## while loop

De while loop gedraagt zich op een zelfde manier als de for loop, maar we hebben zelf meer controle over de drie elementen : initialisatie, conditie en iteratie.

```javascript
let counter : number = 0;
while (counter < 10) {
    counter++;
    console.log(counter);
}
```

Initialisatie van onze loop zal buiten de loop gebeuren.

De conditie controleren we bij het begin van elke iteratie. Indien de conditie onwaar wordt , zal de loop eindigen.

De iteratie (counter++) kunnen we eender waar in de code blok zetten.

In bovenstaand voorbeeld zal in de console de nummers 1 tot en met 10 getoond worden omdat we hier gekozen hebben om de iteratie al uit te voeren bij begin van de code blok. Dit hoeft uiteraard niet, als we kiezen om de iteratie als laatste uit te voeren, dan zal het resultaat exact hetzelfde zijn als het voorbeeld van de for loop.

## do while loop

Een variant op de while loop is de do while loop.

```javascript
let counter : number = 0;
do {
    counter++;
    console.log(counter);
} while (counter < 10)
```

Het grote verschil tussen while en do while is dat bij do while de conditie pas wordt gecontroleerd **nadat** de code blok is uitgevoerd. Dit maakt dat de code blok steeds minstens één keer uitgevoerd zal worden voor de conditie wordt gecontroleerd.

## Oneindige lussen

Door een programmeerfout in de conditie van de for of while loop kan je een oneindige lus maken. Als de conditie zal nooit onwaar kan worden, dan zal je lus nooit kunnen eindigen en spreken we van een oneindige lus.

#### Voorbeeld for loop

```javascript
for (let index : number = 0 ; index >= 0 ; index++) {
    console.log(index);
}
```

In dit voorbeeld hebben we een conditie gemaakt die niet onwaar kan worden. De index zal steeds groter of gelijk aan nul zijn en de loop zal nooit kunnen eindigen.

#### Voorbeeld while loop

```javascript
let counter1 : number = 0;
let counter2 : number = 0
while (counter1 < 10) {
    counter2++;
    console.log(counter1);
}
```

In dit voorbeeld werken we met twee counters. Door een programmeerfout verhogen we de counter2 in de code blok van de loop, maar in de conditie wordt counter1 nagekeken. De conditie kan nooit onwaar worden en bijgevolg zal de loop nooit eindigen.

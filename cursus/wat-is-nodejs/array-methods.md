# Array methods

Bij het datatype Array hebben we gezien dat we de lengte van een array kunnen opvragen en met een for en for ... of loop de gegevens van de array kunnen opvragen.

Er zijn echter nog een hele reeks handige functies die we kunnen gebruiken voor het manipuleren van een array.

## Basis methodes

### concat

Met de concat methode voegen we de elementen van twee arrays samen tot één array.

```typescript
const lst1 : number[] = [1, 2, 3];
const lst2 : number[] = [4, 5, 6];
const result : number[] = lst1.concat(lst2);
console.log(result); //[1, 2, 3, 4, 5, 6]
```

### join

De join methode maakt een string van een lijst van elementen. Tussen elk element wordt een teken of delimiter gezet.

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
let result : string = lst.join(",");
console.log(result); //"1,2,3,4,5,6"
```

### reverse

De reverse methode zet alle elementen in de array in omgekeerde volgerde.

{% hint style="danger" %}
Opgelet ! De originele array wordt aangepast!
{% endhint %}

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
lst.reverse();
console.log(lst); //[6, 5, 4, 3, 2, 1]
```

### push / pop

Met de push en pop methodes voegen we respectievelijk een element **achteraan** de array toe of verwijderen we een element **achteraan** de array.

De push en pop methodes laten ons toe om een LIFO (last in first out) queue te maken.

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
let last : number = lst.pop();
console.log(last); //6
console.log(lst); //[1, 2, 3, 4, 5]
lst.push(7);
console.log(lst); //[1, 2, 3, 4, 5, 7]
```

### unshift / shift

Met de unshift en shift methodes voegen we respectievelijk een element **vooraan** de array toe of verwijderen we een element **vooraan** de array.

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
let first : number = lst.shift();
console.log(first); //1
console.log(lst); //[2, 3, 4, 5, 6]
lst.unshift(7);
console.log(lst); //[7, 2, 3, 4, 5, 6]
```

De combinatie van push en unshift laat ons toe een FIFO (first in first out) queue te maken.

### slice

De slice methode maakt een nieuwe array aan op basis van elementen van een array. Aan de slice methode geef je begin en eind index van de array mee. De originele array blijft ongewijzigd.

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
const result : number[] = lst.slice(2, 4);
console.log(result); //[3, 4]
console.log(lst); //[1, 2, 3, 4, 5, 6]
```

### splice

De splice methode verwijdert elementen uit een array en maakt een nieuwe array van deze elementen. Aan de splice methode geef je begin index en aantal elementen mee. Pas op, dit is anders als bij de slice methode!

{% hint style="danger" %}
Opgelet ! De originele array wordt aangepast!
{% endhint %}

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
const result : number[] = lst.splice(2, 2);
console.log(result); //[3, 4]
console.log(lst); //[1, 2, 5, 6]
```

### indexOf / lastIndexOf

Met deze methodes gaan we op zoek naar de eerste of de laatste index van een element in de array.

Denk eraan: de index van een array begint te tellen bij 0 (nul).

```typescript
const lst : number[] = [1, 2, 3, 1, 2, 3];
console.log(lst.indexOf(2)); //1
console.log(lst.lastIndexOf(2)); //4
```

### includes

De includes methode gaat nakijken of een element onderdeel is van de array, ongeacht waar in de array dit element zou staan. De methode geeft true of false terug.

```typescript
const lst : number[] = [1, 2, 3, 4, 5, 6];
console.log(lst.includes(2)); //true
console.log(lst.includes(7)); //false
```

## Uitgebreide methodes met functie argument

De volgende methodes zijn krachtiger in gebruik omdat ze een functie als argument nemen en we bijgevolg zelf de werking kunnen bepalen.

Als functie argument gebruiken we de **arrow function**. \[TODO : link leggen met uitleg]

### find / findIndex

Met de find of findInde methode zoeken we het eerste element in de array dat voldoet aan de conditie. De conditie moet true of false teruggeven.

In geval van de find methode krijgen we het element zelf terug, in geval van de findIndex de index van het element.

De find methode zal undefined teruggeven als het element niet gevonden wordt, bijgevolg moet je steeds " | undefined" ook toevoegen aan het datatype van het resultaat.

```typescript
const planets : string[] =  [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

let result : string | undefined = planets.find((p: string) => p.startsWith('E'));
console.log(result); //Earth
let index : number = planets.findIndex((p: string) => p.startsWith('E'));
console.log(index); //2
```

Merk op dat volgens de arrow function notatie het niet nodig is om het return keyword te gebruiken.&#x20;

### filter

De filter methode maakt een nieuwe array aan die enkel de element bevat die voldoen aan de conditie. De conditie moet true of false teruggeven.

```typescript
const planets : string[] =  [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

let result : string[] = planets.filter((p: string) => p.startsWith('M'));
console.log(result); //['Mercury', 'Mars']
```

### every / some

Zowel de every als de some methodes gaan alle elementen van de array toetsen aan een conditie. Deze conditie moet true of false teruggeven.

De every methode geeft true terug als alle elementen aan de conditie voldoen, de some methode geeft true terug als minstens één element aan de conditie voldoet.

```typescript
const planets : string[] =  [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

let result1 : boolean = planets.every((p: string) => p.startsWith('M'));
console.log(result1); //false
let result2 : boolean = planets.some((p: string) => p.startsWith('M'));
console.log(result2); //true
```

### forEach

De forEach methode past de functie toe op elk element van de array.

Bijvoorbeeld onderstaande code zal elk element van de array afprinten in de console.

```typescript
const planets : string[] =  [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

planets.forEach((p: string) => console.log(p));
```

Een forEach kan meestal perfect vervangen worden door een gewone for / for ... of loop.

```typescript
const planets : string[] =  [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

for(let p of planets) {
    console.log(p)
}
```

Echter de moderne JavaScript / TypeScript programmeur zal de nieuwere forEach methode prefereren boven een standaard loop.

### map

Met de map methode maken we een nieuwe array aan. De functie in de map zal toegepast worden op elk element van de oorspronkelijke array en de return value van die functie wordt in de nieuwe array gezet.

{% hint style="danger" %}
Opgelet! Het is perfect mogelijk dat het type van de array wijzigt door de map methode.
{% endhint %}

```typescript
const planets : string[] =  [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

const result1 : string[] = planets.map((p: string) => p.toUpperCase());
console.log(result1); //[‘MERCURY’, ‘VENUS’, ‘EARTH’, ‘MARS’, ‘JUPITER’, ‘SATURN’, ‘URANUS’, ‘NEPTUNE’]

const result2 : number[] = planets.map((p: string) => p.length);
console.log(result2); //[7, 5, 5, 4, 7, 6, 6, 7]
```

### reduce

De reduce methode wordt gebruikt om de elementen van een array samen te voegen tot één resultaat. De functie verwacht voor deze methode twee parameters : accumulator en current. De accumulator bevat het resultaat van alle vorige iteraties van deze functie, de current is het huidige element in de array.

Voorbeeld : tel alle elementen in een numerieke array op

```typescript
const lst : number[] = [1, 2, 3];
let result : number = lst.reduce((accumulator:number, current:number) => accumulator + current);
console.log(result); //6
```

De werking ziet er als volgt uit:

1ste run: accumulator = 0 , current = 1     ->    0 + 1 = 1    ->    accumulator wordt 1

2de run: accumulator = 1 , current = 2     ->    1 + 2 = 3    ->    accumulator wordt 3

3de run: accumulator = 3, current = 3     ->    3 + 3 = 6   ->    accumulator wordt 6

Alle elementen zijn behandeld, laatste accumulator waarde wordt teruggeven = 6

## Sorteren

Het sorteren van arrays kan al snel erg ingewikkeld worden wat maakt dat dit een apart hoofdstuk mag zijn.

Sorteren doen we met de sort methode van de array. In de meest basis vorm wordt deze gebruikt als volgt:

```typescript
const planets : string[] = [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

planets.sort();
console.log(planets); // [‘Earth’, ‘Jupiter’, ‘Mars’, ‘Mercury’ , ‘Neptune’, ‘Saturn’, ‘Uranus’ , ‘Venus’];
```

De standaard sortering is alphanumeriek. Voor string arrays is deze standaard voldoende. Echter als we numerieke arrays gaan sorteren, voldoet de standaard niet meer.

```typescript
const numbers : number[] = [3, 8, 12, 1, 15, 2, 23];

numbers.sort();
console.log(numbers); // [1, 12, 15, 2, 23, 3, 8];
```

De standaard alphanumerieke sortering wordt op de array toegepast en geeft een fout resultaat. Volgens deze sortering liggen alle elementen die met een '1' beginnen voor de elementen die met een '2' beginnen.

Alvast voor nummers, maar in veel andere gevallen ook, zullen we een eigen sortering moeten schrijven en hiervoor gebruiken we een functie argument. Deze functie volgt de regels van een sorteerfunctie zoals ze ook in andere talen gebruikt wordt.

### Sorteerfunctie

Een sorteerfunctie vergelijkt twee waardes a en b

* Indien a voor b moet zijn , dan geeft de functie een negatief getal terug - meestal -1
* Indien a na b moet zijn, dan geeft de functie een positief getal terug - meestal 1
* Indien a en b gelijk zijn, dan geeft de functie de waarde nul terug ( 0 )

Toegepast op het numeriek voorbeeld

```typescript
const numbers : number[] = [3, 8, 12, 1, 15, 2, 23];

numbers.sort((a:number, b:number) => {
    if ( a < b ) {
        return -1;
    } else if ( a > b ) {
        return 1;
    } else {
        return 0;
    }
});
console.log(numbers); // [1, 2, 3, 8, 12, 15, 23];
```

Specifiek voor nummers is er een truukje om dit korter te schrijven

```typescript
const arr: number[] = [3, 8, 12, 1, 15, 2, 23];

arr.sort((a: number, b: number) => a - b);

console.log(arr); // [1, 2, 3, 8, 12, 15, 23];
```

## Method chaining

Ook wel genoemd een ketting van methodes maken.

Met deze techniek gaan we meerdere array methods achter elkaar plaatsen waarbij elke methode zijn resultaat doorgeeft aan de volgende methode in de ketting tot er aan het uiteindelijke resultaat wordt gekomen.

Method chaining is enorm krachtig om met zeer weining code ingewikkelde manipulaties op arrays toe te passen.

```typescript
const planets : string[] = [‘Mercury’, ‘Venus’, ‘Earth’, ‘Mars’, ‘Jupiter’, ‘Saturn’, ‘Uranus’, ‘Neptune’];

const result : string[] = planets
		.filter((p: string) => p.startsWith(‘M’))
		.map((p: string) => p.toUpperCase());

console.log(result); // [‘MERCURY’, ‘MARS’]
```

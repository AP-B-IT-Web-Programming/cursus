# Class

## Object Oriented Programming ( OOP )

OOP is een manier van programmeren waarbij je werkt met objecten in plaats van alleen functies en gegevens. Elk object is gemodelleerd op de realiteit en heeft eigenschappen (properties) en methodes (methods). Bijvoorbeeld: een object 'planeet' zou als eigenschappen kunnen hebben 'naam' en 'radius' en als methode 'toonNaam()'.

Deze programmeerstijl helpt bij het organiseren van code, zodat deze makkelijker is om te begrijpen en te hergebruiken. Het maakt grote programma's overzichtelijker door de code op te delen in kleinere stukjes die dan objecten worden genoemd.

De belangrijkste eigenschappen van OOP zijn :

* overerving (inheritance)
* inkapselen (encapsulation)
* polymorfisme (polymorphism)

Wij zullen vooral aan de slag gaan met inkapselen en overerving.

Als we zeggen dat een object eigenschappen heeft ingekapseld, dan wil dat zeggen dat het object:

* deze eigenschappen beheert
* bepaalt welke eigenschappen nodig zijn om correct te werken
* regelt welke eigenschappen mogen wijzigen

Als we zeggen dat een object overerft van een ander object, dan wil dat zeggen dat het object;

* de eigenschappen van het andere object gebruikt
* deze eigenschappen eventueel kan overschrijven

{% hint style="danger" %}
Belangrijk !&#x20;

TypeScript / JavaScript is géén OO taal ! De technieken die in dit hoofdstuk worden uitgelegd  doen vermoeden dat dit wel het geval is maar in de achtergrond wordt steeds prototyping gebruikt.

Alle onderstaande keywords zijn slechts "syntactic sugar" rond het JS prototype.
{% endhint %}

## Class

```typescript
class Planet {
    #name: string;
    constructor(name: string) {
        this.#name = name;
    }
}
```

Met het class keyword maken we een object in TypeScript / JavaScript.

De naam van het object moet steeds met een hoofdletter beginnen. We gebruiken dus PascalCase voor de naamgeving van het object.

De eigenschappen de class zitten tussen accolades.

Een class kan een constructor hebben. De constructor is een speciale soort functie die éénmalig uitgevoerd wordt bij aanmaken van de class. De constructor kan eveneens argumenten hebben, bij het aanmaken van de class moeten deze argumenten dan verplicht meegegeven worden.

## Een class gebruiken

Als we een class hebben gedefinieerd hebben we eigenlijk een nieuw soort data type aangemaakt dat we kunnen gebruiken om nieuwe variabelen aan te maken.

```typescript
let earth: Planet = new Planet("Aarde");
```

Net zoals bij andere datatypes zijn er twee onderdelen: declaratie en initialisatie.

De declaratie `let earth: Planet` zorgt ervoor dat we een nieuwe variabele met naam 'earth' aanmaken en deze is van het type 'Planet'.

Met initialisatie `= new Planet("Aarde");` wordt het object effectief aangemaakt en zijn de eigenschappen van het object beschikbaar. Gebruik het keyword **new** om aan te geven dat je een nieuw object aanmaakt. Het keyword new wordt gevolgd door de naam van de class en haakjes.

Tussen de haakjes geef je de waardes mee om de argumenten van de constructor op te vullen. Heeft de constructor geen argumenten of is er geen constructor, dan laat je de haakjes leeg. Als er wél argumenten op de constructor staan dan moet er tussen de haakjes exact het juiste aantal argumenten van het correcte type worden meegegeven.

## Eigenschappen (properties)

Een object heeft typisch één of meerdere eigenschappen.

Volgens het inkapselen principe moeten deze eigenschappen beheerd worden door het object. Het mag dus niet zijn dat een gebruiker rechtstreeks een interne eigenschap kan aanpassen. Dit gedrag dwingen we af door de interne eigenschap privaat te zetten waardoor een gebruiker deze niet kan aanpassen.

Een variabele privaat maken doen we in TypeScript door een # voor de variabele naam te zetten.

### get / set

Om deze private eigenschap beschikbaar te maken voor de gebruiker moet deze openbaar gemaakt worden met specifieke methodes : get en set.

```typescript
class Planet {
    #name: string;
    constructor(name: string) {
        this.#name = name;
    }
    get name(): string {
        return this.#name;
    }
    set name(value: string) {
        this.#name = value;
    }
}
```

Bij gebruik van get en set moet de naamgeving conventie gevolgd worden:

* get of set gevolgd door een spatie
* de naam van private variabele zonder de #&#x20;
* bij get lege haakjes '()' gevolgd door het return type van de variabele
* bij set exact 1 argument tussen de haakjes met het type van de variabele én géén return type

### this

Methodes in een class kunnen geen andere methodes of variabelen zien (scoping). Om toch de waarde van een interne variabele te kunnen lezen of overschrijven moet het keyword **this** gebruikt worden. Met this leg je een referentie naar naar een variabele of methode en kan je deze gebruiken.

## Methodes (methods)

Naast eigenschappen kan een class ook methodes definiëren. Deze methodes zullen functionaliteit van het object aanbieden.

```typescript
class Planet {
    #name: string;
    constructor(name: string) {
        this.#name = name;
    }
    displayName(): void {
        console.log("De naam van de planeet is " + this.#name);
    }
}
```

Methodes volgen de regels van functies maar dan zonder het keyword **function**.

## Overerving

Bekijken we volgende classes :&#x20;

```typescript
class Cat {
    #name: string;
    #sound: string = “meows”;
    constructor (name: string) {
        this.#name = name;
    }
    makeSound(): void {
        console.log(this.#name + “ “ + this.#sound);
    }
}

let mycat: Cat = new Cat(“Sylvester”);
mycat.makeSound(); // Sylvester meows
```

```typescript
class Dog {
    #name: string;
    #sound: string = “barks”;
    constructor (name: string) {
        this.#name = name;
    }
    makeSound(): void {
        console.log(this.#name + “ “ + this.#sound);
    }
}

let mydog: Dog = new Dog(“Spike”);
mydog.makeSound(); // Spike barks
```

De classes Cat en Dog hebben best wel wat gedeelde eigenschappen. Als we nu ook nog een ander dier willen, bv een aap, dan zal waarschijnlijk deze er eveneens hetzelfde uitzien.

Als we duplicate eigenschappen opmerken dan kunnen we best de overerving techniek toepassen. Bij overerving zullen we een parent class maken die de gedeelde eigenschappen bevat.

```typescript
class Animal {
    #name: string;
    constructor (name: string) {
        this.#name = name;
    }
}
```

Passen we deze parent class toe op de Cat en Dog zien we dit:

```typescript
class Cat extends Animal {
    #sound: string = “meows”;
    constructor (name: string) {
        super(name);
    }
    makeSound(): void {
        console.log(super.name + “ “ + this.#sound);
    }
}

let mycat: Cat = new Cat(“Sylvester”);
mycat.makeSound(); // Sylvester meows
```

```typescript
class Dog extends Animal {
    #sound: string = “barks”;
    constructor (name: string) {
        super(name);
    }
    makeSound(): void {
        console.log(super.name + “ “ + this.#sound);
    }
}

let mydog: Dog = new Dog(“Spike”);
mydog.makeSound(); // Spike barks
```

Het keyword **extends** geeft aan dat de class overerft van een parent class. De eigenschap 'name' zal m.a.w. door de Animal class beheerd worden. Echter bij aanmaak van de Cat of Dog wordt de naam met de constructor meegegeven. Om deze naam naar de parent door te geven gebruiken we het keyword super. Het keyword **super** geeft de class toegang tot de eigenschappen van de parent class. De methode **super()** zal de constructor van de parent class oproepen.

In bovenstaande voorbeelden zien we nog duplicate code, de makeSound() methode is in beide gevallen hetzelfde en kan dus best ook naar de parent class Animal. Maar dan moeten we oplossen dat '#sound' op één of andere manier kan geconfigureerd worden, want het geluid is voor elk dier anders. De oplossing is als volgt:

```typescript
class Animal {
    #name: string;
    #sound: string;
    constructor (name: string, sound: string) {
        this.#name = name;
        this.#sound = sound
    }
    makeSound(): void {
        console.log(this.#name + “ “ + this.#sound);
    }
}

class Cat extends Animal {
    constructor (name: string) {
        super(name, “meows”);
    }
}

class Dog extends Animal {
    constructor (name: string) {
        super(name, “barks”);
    }
}
```

We voorzien op de Animal class een extra argument in de constructor waardoor we het geluid mee kunnen geven vanuit de Cat of Dog constructor.

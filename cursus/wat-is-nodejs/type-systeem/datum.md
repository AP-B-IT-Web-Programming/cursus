# Datum

## Introductie

Als we willen werken met datums hebben we nog een extra datatype nodig: **Date** .

In JavaScript en TypeScript is het Date object standaard ingebouwd, we hebben geen extra libraries of imports nodig om met Date aan de slag te gaan. Een datum maken we als volgt aan:

```typescript
let date: Date = new Date();
```

Het Date object bevat datum én tijd, er is geen apart object voor tijd.&#x20;

Bij initialisatie, new Date() , wordt de huidige datum mét tijd in de variabele gestockeerd. Merk op dat dit geen klok is. Van zodra de variabele geïnitialiseerd is blijft de datum / tijd van initialisatie in de variabele zitten. Deze past zich niet aan aan de klok.

### Initialisatie

Met new Date() neem je de huidige datum / tijd. Het is uiteraard mogelijk om te initialiseren op een bepaald moment.

```typescript
let date: Date = new Date(year, month, day, hours, minutes, seconds, milliseconds);
```

Door gebruik te maken van de constructor parameters, kan je je datum vastzetten op een bepaald moment. Je hoeft niet alle parameters mee te geven, je mag van rechts naar links parameters weglaten en dan worden die automatisch met '0' geïnitialiseerd.

Volgende twee lijnen code zijn bijgevolg hetzelfde:

```typescript
let d1: Date = new Date(2025, 4, 15, 9, 15);
let d2: Date = new Date(2025, 4, 15, 9, 15, 0, 0);
```

Beide datums zijn geïnitialiseerd op 15 mei 2025 09u15.

Opgelet dus, de maand (month) waarde is een zero-based index. De maand januari heeft index 0, de maand december heeft index 11. In bovenstaand voorbeeld is dus de index 4 = mei, alhoewel mei eigenlijk de vijfde maand van het jaar is.

Je mag ook de day waarde weg laten, deze wordt op '1' geïnitialiseerd. Maand en jaar mogen niet leeggelaten worden.

Als er slechts één nummer wordt meegegeven als constructor parameter, dan is dit niet het jaar maar het aantal milliseconds sinds epoch. Bijvoorbeeld:

```typescript
let date: Date = new Date(1747120500000);
```

Dit geeft als resultaat 13 mei 2025 09u25.

Een laatste manier om de datum te initialiseren is via een datum string.

```typescript
let date: Date = new Date("2025-05-13");
```

De constructor parameter is in dit geval een datum in ISO formaat. Het ISO formaat van datum tijd is "yyyy-MM-ddTHH:mm:ssZ".

Een datum met tijd initialiseren is dus op volgende manier:

```typescript
let date: Date = new Date("2025-05-13T09:15:00Z");
```

Merk op dat de 'Z' op het einde van de ISO datum wilt zeggen dat de tijd in UTC staat. UTC is een andere tijdszone dan wij hier zijn. Tijdszones vallen buiten de scope van deze cursus, dat is een cursus op zich. Onthou vooral dat een tijd met 'Z' niet lokaal is. Als je de 'Z' weg laat zal de datum in sommige gevallen de lokale tijd pakken, maar dit werkt niet op alle toestellen dus wees daar voorzichtig mee.

### Epoch

Een datum wordt in het geheugen steeds nummer opgeslagen. Deze nummer is het aantal milliseconden sinds epoch.

Epoch is het datum nul punt van waar men begint te tellen.

JavaScript, TypeScript en nog veel andere talen zoals C#, C, Java en Python gebruiken de Unix Epoch als nul punt. Unix Epoch is 1 januari 1970, deze datum werd gekozen omdat Unix uit kwam in 1971 dat was dus makkelijk voor de ontwikkelaars van Unix.

Niet alle talen gebruiken het Unix Epoch, zo gebruikt .NET een ander epoch: 1 januari 0001.

In de Unix Epoch zit echter een probleem. Initieel werd de Unix Epoch in een 32bit variabele gestockeerd, maar daar zit een limiet op. We gaan op 19 januari 2038 deze limiet overschreiden. Datums die daarna vallen kunnen niet in de 32bit en geven een overflow fout. De meeste systemen hebben dit al aangepast door datums in een 62bit variabele te steken, maar sommige systemen zijn nog niet geupgrade....

### Output

We kunnen nu datums aanmaken, maar we willen ook dat de inhoud van de datum variable kan getoond worden. Dit kan op twee manieren:

```typescript
let date: Date = new Date("2025-05-13T09:15:00Z");
console.log(date.toString()); //Tue May 13 2025 09:15:00 GMT+0200 (Central European Summer Time)
console.log(date.toISOString()); //2025-05-13T07:15:00.000Z
```

De toString() methode op date zal de datum volledig uitgeschreven tonen, inclusief de tijdszone waar het systeem zich momenteel in bevindt.

De toISOString() methode toont de datum in ISO formaat (zie hierboven bij initialisatie). Deze datum wordt met 'Z' geschreven en is dus in UTC tijdszone. Merk op in voorbeeld hierboven dat de 9u in UTC 7u wordt.

Je kan de output verder verfijnen door mee te geven in welke taal het moet zijn en welke opties je wenst. Dit geef je mee aan de toLocaleString() methode en je krijgt een gepersonaliseerde output.

```typescript
const date: Date = new Date("2025-05-13T09:15:00Z");

const options: Intl.DateTimeFormatOptions = {
    weekday: 'long',
    year: 'numeric',
    month: 'long',
    day: 'numeric',
    hour: 'numeric',
    minute: 'numeric'
}
console.log(date.toLocaleString('nl-BE', options)); //dinsdag 13 mei 2025 om 09:15
```

### Getters

Elke waarde van de datum kan opgevraagd worden via een get methode.

We zien volgende getters:

```typescript
const date: Date = new Date("2025-05-13T09:15:00Z");
console.log(date.getFullYear());    //2025
console.log(date.getMonth()); 	    //4
console.log(date.getDate()); 	    //13
console.log(date.getHours()); 	    //11
console.log(date.getUTCHours());    //9
console.log(date.getMinutes());     //15
console.log(date.getSeconds());     //0
console.log(date.getMilliseconds());//0
```

Opgelet voor getDay() ! Deze gaat niét de dag van de maand geven, dat doet de getDate() methode, maar de dag in de week. Waarbij 0 = zondag en 6 = zaterdag.

Eveneens opgelet voor getHours() en getUTCHours(). Let goed op wat je nodig hebt. De getHours() methode geeft lokale tijd en getUTCHours() methode geeft UTC tijd.

Naast deze getters kunnen we ook de milliseconds sinds epoch opvragen en dat is met de getTime() methode.

```typescript
const date: Date = new Date("2025-05-13T09:15:00Z");
console.log(date.getTime()); //1747127700000
```

### Setters

Op dezelfde manier kunnen we ook waardes gaan zetten op de datum. Hiervoor gebruiken we set methodes.

```typescript
const date: Date = new Date();
date.setFullYear(2025);
date.setMonth(4);
date.setDate(13);
date.setHours(9);
date.setMinutes(15);
date.setSeconds(0);
date.setMilliseconds(0);
console.log(date.toISOString()); //2025-05-13T07:15:00.000Z
```

Let ook hier op dat de setDay() de dag in de week zet en niet de dag in de maand.

Elke set methode heeft ook een UTC variant, hier is vooral de setUTCHours() methode interessant als je het uur in UTC tijd wenst te zetten.

En net zoals bij de get methodes kan je ook via setTime() de milliseconden sinds epoch ingeven.

```typescript
const date: Date = new Date();
date.setTime(1747127700000);
console.log(date.toISOString()); //2025-05-13T09:15:00Z
```

### Rekenen met datums

Door de nuttige combinatie van get en set methodes kan je rekenen met datums.

Stel dat je bij een bepaalde datum 20 dagen moet tellen, dat los je op op deze manier:

```typescript
const date: Date = new Date("2025-05-13T09:15:00Z"); 

date.setDate(date.getDate() + 20);

console.log(date.toISOString()); // 2025-06-02T09:15:00Z
```

Wat hier staat is hetvolgende : neem de dagen in de maand, tel er daar 20 bij en set dit op de datum.&#x20;

Dus: dagen in de maand = 13 , tel er 20 bij = 33 en zet dan dagen in de maand om 33. Mei heeft echter maar 31 dagen, er is dus overflow. Wat er dan gebeurd is dat er verder wordt geteld in de volgende maand. 33 - 31 = 2, dus we tellen 2 dagen in juni. Eindresultaat : 2 juni.

Stel dat je het aantal dagen tussen twee datums wilt berekenen, dan ga je als volgt aan de slag:

```typescript
const d1: Date = new Date("2025-05-13T09:15:00Z"); 
const d2: Date = new Date("2025-05-31T09:15:00Z"); 

let diffInMillis: number = d2.getTime() - d1.getTime();  	//1555200000
let diffInDays: number = diffInMillis / (1000 * 60 * 60 * 24); 	//18
```

We nemen twee datums en trekken de milliseconden sinds epoch van elkaar af. Nu hebben we het aantal milliseconden tussen de twee datums. Vervolgens moeten we dat eindresultaat delen door 1000 om naar seconden te gaan, delen door 60 om naar minuten te gaan, nogmaals delen door 60 om naar uren te gaan en dan delen door 24 om naar dagen te gaan. Het eindresultaat is het aantal dagen tussen de twee datums.

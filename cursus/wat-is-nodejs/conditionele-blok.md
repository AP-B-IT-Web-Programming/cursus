# Conditionele blok

Wanneer we logica inbouwen om te bepalen of een stuk code onder bepaalde voorwaarden / condities mag uitgevoerd worden, spreken we over een conditionele blok.

We bekijken twee manieren : de if / else structuur en de switch / case structuur.

## if / else

In de meest simpele vorm controleren we één conditie die bepaalt of een stuk code mag uitgevoerd worden.

```javascript
const dayInWeek : string = readline.question("Welke dag is het vandaag?");
if (dayInWeek == "zondag") {
    console.log("Uitslapen!");
}
```

Meestal zal bij de conditie ook een alternatief code blok worden meegegeven : wat als het niét waar is.

```javascript
const dayInWeek : string = readline.question("Welke dag is het vandaag?");
if (dayInWeek == "zondag") {
    console.log("Uitslapen!");
} else {
    console.log("Om 7u00 opstaan...");
}
```

Belangrijk in de if / else structuur is dat je de blokken code die bij de conditie horen tussen accolades zet.

Het is ook mogelijk om meerdere if / else condities te combineren op deze manier:

```javascript
const dayInWeek : string = readline.question("Welke dag is het vandaag?");
if (dayInWeek == "zondag") {
    console.log("Uitslapen!");
} else if (dayInWeek == "zaterdag") {
    console.log("Om 9u00 opstaan en studeren");
} else if (dayInWeek == "woensdag") {
    console.log("Om 8u00 opstaan en naar school gaan");
} else {
    console.log("Om 7u00 opstaan en naar school gaan");
}
```

Alhoewel het perfect mogelijk is om tot in het oneindige if / else if / else condities te blijven schrijven, begint dit al snel heel onoverzichtelijk te worden.

Om dit op te lossen hebben we onze tweede conditionele structuur.

## switch / case

De switch / case structuur komt het best tot zijn recht als we voor één conditie meerdere mogelijkheden hebben, zoals in het voorbeeld hierboven.

```javascript
const dayInWeek : string = readline.question("Welke dag is het vandaag?");
switch (dayInWeek) {
    case "zondag":
        console.log("Uitslapen!");
        break;
    case "zaterdag":
        console.log("Om 9u00 opstaan en studeren");
        break;
    case "woensdag":
        console.log("Om 8u00 opstaan en naar school gaan");
        break;
    default:
        console.log("Om 7u00 opstaan en naar school gaan");
        break;
}
```

Door deze structuur is de leesbaarheid van de code sterk verbeterd én het is ook veel makkelijker om een extra conditie toe te voegen.

{% hint style="warning" %}
Opgelet ! Je kan de switch / case structuur enkel gebruiken indien de conditie met de 'gelijk aan' operator vergeleken wordt.
{% endhint %}

{% hint style="info" %}
Belangrijk ! Het keyword break zorgt ervoor dat een case eindigt. Zet je geen break, dan zal de volgende case ook nog uitgevoerd worden.
{% endhint %}

## Logische operatoren

Om condities op te stellen hebben we beschikking over logische operatoren. Denk eraan dat bij switch / case enkel de gelijk aan operator gebruikt wordt.

| Betekenis             | Operator | Voorbeeld |
| --------------------- | -------- | --------- |
| Gelijk aan            | ==       | a == b    |
| Ontkenning (not)      | !        | !(a == b) |
| Niet gelijk aan       | !=       | a != b    |
| Kleiner dan           | <        | a < b     |
| Groter dan            | >        | a > b     |
| Kleiner of gelijk aan | <=       | a <= b    |
| Groter of gelijk aan  | >=       | a >= b    |
| Logische AND          | &&       | a && b    |
| Logische OR           | \|\|     | a \|\| b  |

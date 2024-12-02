---
description: >-
  MySQL is een open-source relationeel database management systeem, of ook wel
  RDBMS genoemd.
---

# MySQL

*   open source, maar wel eigendom van Oracle

    Fun fact: de oorspronkelijke bedenker van MySQL heeft een variant uitgebracht MariaDB o.a. uit protest tegen de overname door Oracle.
* relationele database : werkt met tabellen en de query taal SQL.
* database management systeem : ook alle software die nodig is om de database aan te spreken wordt in het MySQL ecosysteem aangeleverd.

## Installatie

Om met MySQL aan de slag te gaan moet je deze installeren. Kies voor de MySQL community edition. Je kan je het leven makkelijker maken door ook de MySQL workbench te installeren. Met de workbench kan je makkelijk je schema's en tabellen opvragen.

En dan moeten we uiteraard in ons node project ook nog MySQL installeren. Dit doe je met het command:

```bash
npm install mysql2
```

{% hint style="danger" %}
**Opgelet !** Gebruik de **mysql2** library en niét de mysql library. De mysql library is verouderd !!
{% endhint %}

## Connecteren

De eerste stap is connecteren vanuit je node server naar je database.

Hier moeten we twee zaken voor doen: connectie opties definiëren en de connectie aanmaken.

### Connection options

Om de connectie op te zetten moeten we weten waar je database draait en met welke gegevens we kunnen aanloggen.

```typescript
import mysql, {ConnectionOptions} from ‘mysql2’;

const access: ConnectionOptions = {
    connectionLimit	: 10,
    host		: "localhost",
    user		: "root",
    password		: "<jouwrootwachtwoord>",
    database		: "<jouwdatabasenaam>"
};
```

We beginnen met de connection options aan te maken. ConnectionOptions is een datatype dat je importeert van de mysql2 library. Dit datatype bevat de mogelijke opties voor de connectie. Enkele belangrijke opties zijn:

* host : de URL waar je database server draait. In development zal dat waarschijnlijk je eigen machine zijn, dus 'localhost'.
* user : de gebruiker waarmee je connecteert. In development is dat meestal de 'root' user.
* password : het wachtwoord waarmee die user connecteert.
* database : de database waarnaartoe je connecteert, dit is de schema naam die je hebt aangemaakt in MySQL. Let op dat je user rechten moet hebben om dit schema aan te spreken.
* connectionLimit : hoeveel connecties simultaan naar je database kunnen.

De volgende stap is de connectie aanmaken met deze opties.

```typescript
import mysql, {ConnectionOptions, Connection} from 'mysql2';

const access: ConnectionOptions = { ... };

const conn: Connection = mysql.createConnection(access);

```

Met het createConnection commando maak je een connectie van datatype Connection aan. Merk op dat je je ConnectionOptions als parameter mee geeft aan deze functie.

Er zijn nu twee manieren om verder te werken : via callback of promise

### Query met callback

Na het aanmaken van de connectie, kunnen we deze gebruiken om queries uit te voeren.

Een select query met callback, wordt als volgt opgezet:

```typescript
import mysql, {ConnectionOptions, Connection} from 'mysql2';
const access: ConnectionOptions = { ... };
const conn: Connection = mysql.createConnection(access);

conn.query("SELECT * FROM planet", (error, results) => {
    if(error) throw error;
    console.log(results);
});

```

Gebruik de query functie van de connection en geef twee parameters mee: de query en een callback function. De callback function heeft twee parameters: error en results.

Als eerste lijn zet je best een controle op je error. Er kan best wel wat mislopen bij het query-en van je database dus deze controle is nodig om die fouten op te vangen.

Het results object zal het resultaat van je query bevatten. In geval van een select is dit een array van records.

Andere soorten query, zoals insert of delete, worden op dezelfde manier uitgevoerd.

### Query met promise

De ondersteuning voor promise (async / await) werd pas later toegevoegd aan de mysql2 library. Hierdoor moeten we een andere import gebruiken als we met promise willen werken

De select query schrijven we dan als volgt:

```typescript
import mysql, {ConnectionOptions, Connection} from 'mysql2/promise';
const access: ConnectionOptions = { ... };

async function run() {
    try {
        const conn: Connection = await mysql.createConnection(access);
        const [results, fields] = await conn.query("SELECT * FROM planet");
    } catch (error) {
        console.log(error)
    }
}
run();

```

{% hint style="danger" %}
Opgelet ! Gebruik de import _**mysql2/promise**_ om met async / await aan de slag te gaan !
{% endhint %}

Als we met promise werken zorgen we uiteraard eerst voor een async function waar de await statements in kunnen gezet worden.

Een query via promise geeft een tuple terug van results en fields. Je kan ook de fields weg laten zodat je enkel \[results] opvangt. Maar het is steeds een tuple, zelfs als je enkel interesse hebt in de results.

De results bevatten, net zoals bij de callback, de resultaatslijnen van je query.

Errorhandling dienen we bij de promise te doen via de try / catch methode want in tegenstelling tot de callback krijgen we daar geen error object terug. De promise query zal een throw doen van de error die we dus opvangen met een try / catch.

### SELECT met WHERE clause

In veel gevallen zal je SELECT query een WHERE clause bevatten en dit kunnen we op twee manieren oplossen: string interpolatie of prepared statement.

#### WHERE clause met string interpolatie

```typescript
async function run(myname: string) {
    try {
        const conn: Connection = await mysql.createConnection(access);
        const[results] = await conn.query(´SELECT * FROM planet WHERE name = ${myname}´);
    } catch(error) {
        console.log(error);
    }
}
run("Earth");

```

Door string interpolatie kunnen we de parameters van de clause makkelijk toevoegen aan de query.

#### WHERE clause met prepared statement

```typescript
async function run(myname: string) {
    try {
        const conn: Connection = await mysql.createConnection(access);
        const[results] = await conn.query("SELECT * FROM planet WHERE name = ?", [myname]);
    } catch(error) {
        console.log(error);
    }
}
run("Earth");

```

Bij de prepared statement methode plaatsen we in de where clause een "?" op de plaats waar een parameter ingevuld dient te worden. Vervolgens wordt een array van waardes meegegeven en deze waardes worden ingevuld op de plaats van het "?". Heb je meer dan één "?" in de where clause staan, dan wordt in het eerste "?" de eerste waarde van array gezet en in het tweede "?" de tweede van de array enzovoort.

### INSERT

Een INSERT query kan eveneens en dit volgt hetzelfde stramien als een SELECT query. Ook hier kunnen we kiezen voor string interpolatie of prepared statement voor het doorgeven van de parameters.

Voorbeeld met string interpolatie

```typescript
async function run(myname: string) {
    try {
        const conn: Connection = await mysql.createConnection(access);
        const[results] = await conn.query(´INSERT INTO planet VALUES (${myname})´);
    } catch(error) {
        console.log(error);
    }
}
run("Mars");

```

Voorbeeld met prepared statement

```typescript
async function run(myname: string) {
    try {
        const conn: Connection = await mysql.createConnection(access);
        const[results] = await conn.query("INSERT INTO planet VALUES (?)", [myname]);
    } catch(error) {
        console.log(error);
    }
}
run("Mars");

```

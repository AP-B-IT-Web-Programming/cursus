# Basis

### Express

Express is een populair Web Application Framework gebaseerd op Node.js waarmee we web applicaties en APIs kunnen bouwen.

Aan de hand van Express kunnen we onze applicaties als een full TypeScript (of JavaScript) stack schrijven, m.a.w. onze code op de backend en de code in de client is allemaal TypeScript.

Dit type frameworks laat ons ook toe de client pagina"s dynamisch te genereren. Dit wil zeggen dat de finale HTML/CSS/TS pagina niet bestaat tot een gebruiker de server raadpleegt. Express zal deze pagina aanmaken met alle nodige data (bv. data uit de database).

Fictief voorbeeld: De gebruiker gaat naar http://webontwikkeling.ap/. Express herkent dat de gebruiker de homepagina wil (omdat er na de laatste slash niets volgt). De ontwikkelaar heeft gezorgd dat Express hier een mooie hoofdpagina toont met de laatste 3 nieuwtjes (die uit een database komen) over Webontwikkeling. Onderdelen van deze pagina bestonden (bv. de CSS, wat HTML en een stukje client script) maar Express vult de ontbrekende data in en stuurt mooie volledige HTML/CSS/TS naar de client.

#### Express hello world

We starten met het installeren van Express.

```
npm install express
```

In deze module gebruiken we TypeScript dus we moeten ook de types installeren

```
npm install --save-dev @types/express
```

De Hello World applicatie. We lichten hieronder toe hoe deze werkt:

```typescript
import express, {Express, Request, Response} from "express";

const app: Express = express();

const hostname: string = "127.0.0.1";
const port: number = 3000;

app.get("/", (req: Request, res: Response) => {
  res.type("text/html");
  res.send("Hello <strong>World</strong>");
});

app.listen(port, hostname, () =>
  console.log(´[server] http://${hostname}:${port}/´);
);
```

Sla dit bestand op als `server.ts` en start het op met `ts-node server.ts`. Je kan nu naar `http://localhost:3000` surfen en je ziet de tekst `Hello World` verschijnen.

Laten we elke lijn bekijken

```typescript
import express, {Express, Request, Response} from "express";

const app: Express = express();
```

We importeren de express module en de nodige types en voeren `express()` uit. Het resultaat hiervan is een `Express` object dat de Express applicatie voorstelt. Dit object wordt meestal 'app' genoemd

We kunnen dit object gebruiken om een aantal settings aan te passen, te beslissen welke url welke data (HTML, JSON, etc.) laadt en de applicatie te starten.

```typescript
const hostname: string = "127.0.0.1";
const port: number = 3000;
```

Het is belangrijk om te definiëren op welke poort onze webapplicatie gaat luisteren. Een typische keuze tijdens ontwikkeling is de poort 3000. Tijdens ontwikkeling willen we ook meestal op localhost (127.0.0.1) werken. Dit wil zeggen dat we lokaal naar `http://localhost:3000` zullen moeten gaan.

Laten we nu eerst de laatste lijnen bekijken:

```typescript
app.listen(port, hostname, () =>
  console.log(´[server] http://${hostname}:${port}/´);
);
```

`app.listen` zorgt dat onze web applicatie start met luisteren op de meegegeven poort en hostname. De derde parameter is een callback die wordt uitgevoerd wanneer het luisteren succesvol is opgestart. Hier printen we gewoon de url en port uit op de console ter info.

#### Express routes

Web applicaties en websites bevatten meestal meer dan 1 pagina. Tot nu toe zie je het path in een URL als een locatie op een webserver. Bv. `localhost:3000/index.html` zou de file `index.html` zijn die zich bevindt in de root folder. `localhost:3000/profile/addPicture.html` zou een file `addPicture.html` zijn die zich in `/profile/` bevindt.

Express laat ons toe zelf te bepalen welke data wordt teruggestuurd aan de hand van de URL. In ons voorbeeld zal `localhost:3000/` op het scherm de tekst "Hello World" en in de console de volledige url tonen.

```typescript
app.get("/",(req: Request,res: Response)=>{
    console.log(req.baseUrl);
    res.type("text/html");
    res.send("Hello <strong>World</strong>")
})
```

Express werkt met routes. Een route kan je ook een API endpoint noemen.

Een route heeft steeds een method, dit is get, post, put of delete. Dat komt overeen met de standaard HTTP methods GET , POST , PUT en DELETE. Elke method heeft een doel, deze zijn standaard in HTTP communicatie dus hou je aan deze standaarden!

* GET : vraag data op, dit kan een HTML pagina zijn of gegevens in JSON formaat of ...
* POST : maak een nieuwe data aan
* PUT : wijzig data
* DELETE : verwijder data

Een route heeft 2 parameters:

* het pad, dit is alles dat na de host:port komt
* een callback functie met 2 parameters: request en response

Het pad hier is "/". Dit komt overeen met `localhost:3000/`, omdat het relatief is ten opzichte van het adres van de server. Vervang je dit door bv "/helloworld", dan zal je naar `localhost:3000/helloworld` moeten gaan. localhost:3000 zal niet meer werken.

De functie parameter zijn:

* het **request** object. Dit object heeft informatie over de request die de client heeft gedaan. Denk bv. aan de headers, de body, de query parameters, etc. Het is een object van het type Request.
* het **response** object. Het response object bevat informatie die we terug naar de client sturen. Dit object is van het type Response.

Met response object sturen we een antwoord terug naar de client. We gebruiken hier 2 functies:

```typescript
res.type("text/html");
```

`type()` laat ons toe het Content-type van de response te bepalen. Een volledige lijst van types vind je hier. De belangrijkste die we gaan gebruiken zijn `"text/html"` en `"application/json"`.

```typescript
res.send("Hello <strong>World</strong>")
```

Om data terug te sturen gebruiken we de `send()` functie. Omdat we HTML willen terugsturen, vullen we de parameter met een string in HTML formaat.

#### Multiple routes

Verschillende routes toevoegen is makkelijk:

```typescript
app.get("/",(req: Request,res: Response)=>{
    res.type("text/html");
    res.send("Yet another hello world app...")
});
app.get("/helloworld",(req: Request,res: Response)=>{
    res.type("text/html");
    res.send("Hello World")
});
app.get("/goodbye",(req: Request,res: Response)=>{
    res.type("text/html");
    res.send("Later <strong>World</strong>")
});
```

Voor elke route roepen we `app.get` op met het path dat we willen instellen en de data die we willen terugsturen.

We kunnen ook verkeerde paths opvangen. Als de gebruiker naar een path gaat dat niet bestaat, kunnen we ze bv. een foutmelding geven.

```typescript
app.use((req, res) => {
    res.type("text/html");
    res.status(404);
    res.send("404 - Not Found");
    }
);
```

Merk op dat we een nieuwe lijn hebben toegevoegd:

```typescript
res.status(404);
```

Dit geeft een custom status code terug. 404 laat jouw browser weten dat de pagina niet gevonden werd. Standaard zal 200 worden teruggegeven, als alles ok is (en als je dus zelf geen status meegeeft).

{% hint style="danger" %}
Opgelet: De volgorde is hier belangrijk. Zet je deze app.use bovenaan in de applicatie, dan zal geen enkele route meer werken. Plaats die onderaan (maar boven app.listen).
{% endhint %}

#### Een simpele API

Tot nu toe stuurden we html terug. Maar we kunnen ook data terugsturen. Dit verandert onze web applicatie in een echte API.

<pre class="language-typescript"><code class="lang-typescript"><strong>import express, {Express} from "express";
</strong>
const app: Express = express();

const hostname: string = "127.0.0.1";
const port: number = 3000;

interface Planet {
    name: string;
    radius: number;
}

const data : Planet[] = [
    {   
        name: "Mercury",
        radius: 2439
    },
    {   
        name: "Venus",
        radius: 6051
    },
    {   
        name: "Earth",
        radius: 6378
    },
];

app.get("/getData",(req,res)=>{
    res.type("application/json");
    res.json(data);
})

app.listen(post, hostname, async ()=>{
    console.log(´[server] http://${hostname}:${port}/´);
});
</code></pre>

We hebben een variabele data aangemaakt die een array van objecten bevat. Om deze data te sturen gebruiken we een ander type: application/json.

```typescript
res.type("application/json");
```

Dit zorgt ervoor dat de client weet dat het om json gaat. De Content-type in de header zal dan ook "application/json" zijn.

```typescript
res.json(data);
```

Om de JSON data terug te sturen, gebruiken we res.json.

{% hint style="danger" %}
Eigenlijk moeten we het type hier niet definieren. res.json zal zelf de content-type van de header aanpassen naar "application/json".
{% endhint %}

#### Async routes

We kunnen ook async routes maken. Dit is handig als we bv. data moeten ophalen uit een API.

```typescript
app.get("/planets",async (req: Request,res: Response) =>{
    let response = await fetch("https://theorie-webprogramming.surge.sh/planets.json");
    let data = await response.json();
    res.type("application/json");
    res.json(data);
});
```

Deze route zal dus eerst de data ophalen van de API en pas daarna terugsturen. De response zal dus niet onmiddellijk terugkomen. De snelheid van de API zal dus ook de snelheid van onze applicatie bepalen.

Wil je niet afhankelijk zijn van de snelheid van een externe API, dan kan je ook bij het opstarten van de server de data ophalen en opslaan in een variabele. Deze variabele kan je dan gebruiken in je routes. Vaak word dit gedaan in de `app.listen` functie. Deze moet dan ook async zijn.

```typescript
let data : Planet[] = [];

app.get("/getData",(req,res)=>{
    res.type("application/json");
    res.json(data);
});

app.listen(post, hostname, async ()=>{
    let response = await fetch("https://theorie-webprogramming.surge.sh/planets.json");
    data = await response.json();
    console.log(´[server] http://${hostname}:${port}/´);
});
```

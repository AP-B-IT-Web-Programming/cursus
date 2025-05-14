# Van Form tot Database

Als sluitstuk van deze cursus gaan we de volledige communicatie opzetten van HTML form naar MySQL database. Hiervoor gebruiken we alle technologieën die we het voorbije semester hebben gezien :

* VITE
* Dom manipulatie
* Fetch
* JSON
* Node.js
* Express
* MySQL

### Stap 1 : VITE project opzetten

Maak een nieuw VITE project voor je front end

```
npm create vite@latest
```

We maken een project demo-client aan.

Kuis het VITE project op zodat enkel wat je nodig hebt over blijft.

Heb je meer info nodig, kijk dan even terug naar [de uitleg over VITE](../frontend/vite.md).

### Stap 2 : HTML form aanmaken

Maak in je index.html een formulier aan:

```html
<form id="myForm">
  <label for="name">Naam:</label>
  <input type="text" id="name" name="name" required />
  <br />
  <label for="email">E-mail:</label>
  <input type="email" id="email" name="email" required />
  <br />
  <button type="submit">Verzenden</button>
</form>
<div id="responseMessage"></div>
```

### Stap 3 : Formulier info doorsturen via fetch

In deze stap lezen we de informatie van het formulier uit en sturen we dit door via fetch naar onze server. We gebruiken bijvoorbeeld async / await.

```typescript
interface MyFormData {
  name: string;
  email: string;
}

const formElement = document.querySelector('#myForm');
const formMessage = document.querySelector('#responseMessage');

formElement.addEventListener("submit", async (event) => {
  event.preventDefault(); // Voorkom standaard formulierverzending

  // Formuliergegevens ophalen  
  const formData = new FormData(formElement);
  const data: MyFormData = Object.fromEntries(formData.entries()) as unknown as MyFormData;

  try {
    const response = await fetch("http://localhost:3000/sendData", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(data),
    });

    const message = await response.text();

    formMessage.textContent = message; // Antwoord weergeven
  } catch (error) {
    console.error("Er is een fout opgetreden:", error);
    formMessage.textContent = "Er is een fout opgetreden. Probeer het later opnieuw.";
  }
});

```

Als eerste stap zetten we een eventlistener op de submit van het formulier. Van zodra je gebruiken op de verzenden knop van het formulier druk, zal deze listener uitgevoerd worden.

We maken de callback function van de eventlistener **asynchroon** door er **async** voor te zetten. Dit hebben we nodig om in de callback fetch te kunnen gebruiken met het **await** keyword.

Vervolgens willen we het standaard gedrag van het formulier tegen houden. We gaan een eigen implementatie voorzien dus we zetten als eerste lijn in de event handler callback de lijn **event.preventDefault();** : dit houdt de verwerking van het formulier tegen.

In de volgende stap halen we de gegevens van het formulier op. In dit voorbeeld hebben we een html form gebruikt en kunnen we de ingebouwde eigenschappen van het formulier gebruiken. Via FormData halen we de formuliergegevens op en met de .entries() function maken we een object van het interface type MyFormData aan.

Het is uiteraard ook mogelijk om elk veld apart in te lezen van de html via querySelector en deze velden dan bijvoorbeeld mee te geven aan de constructor van een class. Deze techniek heb je sowieso nodig als je niet met een html form werkt.

Als laatste gaan we ons object (interface of class) via fetch versturen naar de express server. Tijdens het coderen gaan we er even vanuit dat we een express server zullen hebben draaien op localhost poort 3000 en dat we daar een route hebben voorzien POST sendData die json aanvaardt.

Na het versturen vangen we het antwoord van de server op en dit wordt op de html pagina getoond.

### Stap 4 : Express server aanmaken

Maak een nieuwe node project aan voor je back end en noem deze demo-server en voeg de nodige npm libraries toe voor express.

Als je dit even niet goed meer weet, bekijk dan [de uitleg van express.js](../backend/wat-is-een-backend-framework/).

Onderstaande code hebben we minstens nodig om onze server op te starten op localhost 3000 én een POST route op /sendData.

```typescript
import express, {Express, Request, Response} from "express";

const app: Express = express();
app.use(express.json());

const hostname: string = "127.0.0.1";
const port: number = 3000;

interface MyFormData {
  name: string;
  email: string;
}

app.post("/sendData", (req: Request, res: Response) => {
  const json : MyFormData = req.body;
  res.status(200).end();
});

app.listen(port, hostname, () =>
  console.log(´[server] http://${hostname}:${port}/´);
);
```

We hebben het json framework geactiveerd waardoor we in de POST route uit de request body onze json data kunnen halen. Ook hier voorzien we dezelfde interface als op front end om de json data makkelijk leesbaar te maken.

{% hint style="warning" %}
In dit voorbeeld wordt de interface en route mee in het server.ts bestand geschreven.

Beter zou zijn om de route in een Express Router te steken én de interface via import / export uit een extern bestand te laten komen.

Het doel moet zijn om je server.ts bestand zo proper mogelijk te houden : routes en interfaces/classes horen niet thuis in dit bestand !
{% endhint %}

### Stap 5 : MySQL activeren

Voeg MySQL toe aan je express server.

Bekijk even [de theorie over MySQL](../backend/mysql.md) om op te frissen hoe je dit nu weer doet.

We laten de configuratie van de connectie even buiten beschouwen en concentreren ons op de code die toegevoegd dient te worden aan de POST route.

```typescript
app.post("/sendData", async (req: Request, res: Response) => {
  const json : MyFormData = req.body;
  
  try {
      const conn: Connection = await mysql.createConnection(access);
      const[results] = await conn.query("INSERT INTO users (name, email) VALUES (?, ?)", 
          [json.name, json.email]);
      res.status(200).send("De gegevens werden succesvol opgeslagen.");
  } catch(error) {
      console.log(error);
      res.status(500).send("Er is een fout opgetreden.");
  }
  
});
```

In dit voorbeeld gaan we ervanuit dat er een users tabel bestaat in onze database met de kolommen name en email.

Zoals al aangegeven wordt het access object voor de connection buiten beschouwing van dit voorbeeld gehouden.

### Extra : gebruikers opvragen

In het voorbeeld hierboven wordt informatie van een formulier naar de database gestuurd.

Meestal zal je ook geïnteresseerd zijn in de gegevens die in de database zitten om deze bijvoorbeeld in een tabel te tonen.

Volg ongeveer dezelfde stappen om dit op te zetten:

* Maak een lege HTML table klaar op je pagina
* Schrijf code in je VITE project om :
  * een fetch te doen op bijvoorbeeld GET http://localhost:3000/users
  * het resultaat van de fetch in een array op te slaan
  * over deze array te itereren en via createElement rijen aan te maken voor je HTML tabel
* Schrijf in je Express server een nieuwe GET route op /users
* Haal in deze route de records op van je users tabel via de query SELECT \* FROM users
* Stuur de records als json terug op de response van je route


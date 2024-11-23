# Request

Het Request object is een object dat door Express wordt aangemaakt en wordt meegegeven aan de callback functie van een route. Het bevat informatie over de request die de client verstuurd heeft. Je kan het gebruiken om bv. de inhoud van een `POST` request te lezen, de headers te lezen, de parameters van een route te lezen, etc.

Enkele properties van het Request object zijn:

* `req.body`: bevat de inhoud van een `POST` request
* `req.headers`: bevat de headers van de request
* `req.params`: bevat de parameters van een route
* `req.query`: bevat de query parameters van een request
* `req.path`: bevat het pad van de request
* `req.method`: bevat de HTTP method van de request (GET, POST, PUT, DELETE, etc.)
* `req.ip`: bevat het IP adres van de client

### Request Headers

Request headers zijn een belangrijk onderdeel van een HTTP request. Ze bevatten informatie over de request zelf. Ze worden meegestuurd door de client en kunnen door de server gelezen worden. Headers bevatten bv. informatie over de browser die de request verstuurd, de taal van de client, de versie van de HTTP protocol, etc. Een header bestaat uit een naam en een waarde.

Zo kan je bijvoorbeeld aan de hand van de header `User-Agent` de browser van de client bepalen. De waarde van deze header is bv. `Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/87.0.4280.88 Safari/537.36`.

Headers worden meegestuurd in de request. Je kan ze lezen via het Request object:

```typescript
app.get("/headers",(req: Request,res: Response)=>{
    let headers = req.headers;
    res.json(headers);
});
```

Wil je een specifieke header lezen, gebruik dan de property `req.headers`:

```typescript
app.get("/headers",(req,res)=>{
    let userAgent = req.headers["user-agent"];
    res.type("text/html")
    res.send(`Your browser is ${userAgent}`);
});
```

### PathParameters

Wanneer een deel van een URL een betekenis heeft in je code, dan spreken we van een path parameter. Een typische voorbeeld is een url als volgt:

```http
http://localhost:3000/planets/earth
http://localhost:3000/planets/mars
```

In dit voorbeeld zijn 'earth' en 'mars' parameters die we willen gebruiken in onze code.

De route wordt dan als volgt opgebouwd:

```typescript
app.get("/planets/:planet",(req: Request,res: Response)=>{
    let planet: string = req.params.planet;
    res.send(planet);
});
```

Om aan te geven dat een onderdeel van het path een parameter is, wordt een ":" gebruikt. In het voorbeeld zie het :planet wat wil zeggen dat er een parameter is met de naam 'planet'.

De waarde van deze parameter halen we van het request object via de params property en we vragen de param 'planet' : `req.params.planet`

### Query Parameters

Om een zoekopdracht door te geven aan een API wordt één of meerdere query parameters aan een url toegevoegd. Dat ziet er dan als volgt uit:

```http
http://localhost:3000/planets?planet=earth
```

En de route is dan :

```typescript
app.get("/planets",(req: Request,res: Response)=>{
    let planet: string = req.query.planet;
    res.send(planet);
});
```

Merk op dat, in tegenstelling tot path parameter, de route niet aangeeft welke mogelijke query parameters de route kan verwerken.

Goede documentatie zal nodig zijn!

### Request Body

Een request body gaan we terug vinden bij POST en PUT requests.

Hoewel het perfect mogelijk is om data te versturen via een `GET` request, is het niet altijd de beste keuze. De data die je verstuurd via een `GET` request is zichtbaar in de URL. Bovendien is de hoeveelheid data die je kan versturen beperkt. De meeste browsers hebben een limiet van 2048 karakters. Dit is niet altijd voldoende. Daarom gebruiken we `POST` en `PUT` requests.

Bij een `POST` request wordt de data niet zichtbaar in de URL. De data wordt verstuurd in de body van het request. De body is een onderdeel van het request dat gebruikt wordt om data te versturen. Je zou de body kunnen zien als een brief die je in een enveloppe steekt. Bij de `GET` request zou je het bericht op de enveloppe schrijven, bij de `POST` of `PUT` request steek je het bericht in de enveloppe. Beide zullen de bestemming bereiken, maar de inhoud van de enveloppe is niet direct zichtbaar voor iedereen.

Opgelet: Het is niet zo dat `POST` en `PUT` requests veilig zijn. De inhoud van een `POST` of `PUT` request is ook leesbaar. Als we teruggrijpen naar de analogie van de enveloppe, dan kan iedereen de enveloppe openen en de inhoud lezen. Als je echt zeker wil zijn dat de data veilig verstuurd wordt, moet je de data versleutelen.

Onze API ziet er nu als volgt uit:

```typescript
app.post("/planets",(req: Request,res: Response)=>{
    let planet: string = req.body.planet;
    res.send(planet);
});
```

Merk op: de method is post en niet meer get.

Een post kan je niet zomaar in de browser testen, browser sturen enkel GET requests uit. Om een POST request te testen heb je externe tooling zoals bv Postman nodig.

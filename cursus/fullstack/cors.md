---
description: >-
  CORS (Cross-Origin Resource Sharing) is een beveiligingsmechanisme dat wordt
  gebruikt in webbrowsers om te bepalen of bronnen (zoals API's, afbeeldingen,
  of data) van een andere "origin" mogen worden
---

# CORS

### Wat is CORS

CORS (Cross-Origin Resource Sharing) is een beveiligingsmechanisme dat wordt gebruikt in webbrowsers om te bepalen of bronnen (zoals API's, afbeeldingen, of data) van een andere "origin" mogen worden opgehaald. Een "origin" bestaat uit drie onderdelen: het **protocol** (bijv. `https://`), de **domeinnaam** (bijv. `example.com`) en de **poort** (bijv. `:3000`).

### Waarom bestaat CORS?

CORS beschermt gebruikers tegen schadelijke verzoeken van scripts in een browser. Stel je voor dat een website kwaadwillig een verzoek naar jouw bank zou sturen via JavaScript: zonder beperkingen zouden ze toegang kunnen krijgen tot jouw gevoelige gegevens. CORS voorkomt dit door standaard cross-origin-verzoeken te blokkeren, tenzij de server expliciet toestemming geeft.

### Hoe werkt CORS?

Wanneer een browser een verzoek doet naar een andere origin (cross-origin), gebeurt het volgende:

1.  **Preflight-verzoek** (OPTIONS):\
    Bij sommige types verzoeken (zoals `PUT` of `DELETE`), of als bepaalde headers worden gebruikt, stuurt de browser eerst een preflight-verzoek met de HTTP-methode `OPTIONS`. Dit controleert of de server de cross-origin-aanvraag toestaat.

    De browser stuurt headers zoals:

    ```http
    Origin: https://example-client.com
    Access-Control-Request-Method: POST
    Access-Control-Request-Headers: Content-Type
    ```
2.  **Reactie van de server**:\
    De server reageert met headers die aangeven of de cross-origin-aanvraag is toegestaan. Bijvoorbeeld:

    ```http
    Access-Control-Allow-Origin: https://example-client.com
    Access-Control-Allow-Methods: GET, POST, OPTIONS
    Access-Control-Allow-Headers: Content-Type
    ```
3. **Verzoek verwerken**:\
   Als de browser ziet dat de server de cross-origin-aanvraag toestaat, voert het de oorspronkelijke aanvraag uit. Zo niet, wordt het verzoek geblokkeerd.

### Veelgebruikte CORS-headers

1.  **Access-Control-Allow-Origin**\
    Specificeert welke origin(s) toegang hebben.

    Bijvoorbeeld:

    `Access-Control-Allow-Origin: *` (toestaan voor iedereen)

    `Access-Control-Allow-Origin: https://example-client.com`
2.  **Access-Control-Allow-Methods**\
    Definieert de HTTP-methoden die toegestaan zijn.

    Bijvoorbeeld:

    `Access-Control-Allow-Methods: GET, POST, PUT`
3.  **Access-Control-Allow-Headers**\
    Geeft aan welke headers in verzoeken zijn toegestaan.

    Bijvoorbeeld:

    `Access-Control-Allow-Headers: Authorization, Content-Type`
4.  **Access-Control-Allow-Credentials**\
    Toont of cookies en andere referenties (zoals HTTP-authenticatie) mogen worden meegezonden.

    Bijvoorbeeld:

    `Access-Control-Allow-Credentials: true`

### CORS fout oplossen in node.js

Als je een CORS fout tegenkomt, kan het zijn dat:

* De server geen toestemming geeft aan de origin van je verzoek.
* Een preflight-verzoek faalt omdat de server de benodigde headers niet retourneert.

1.  **CORS installeren**:\
    Installeer CORS in je node.js project.



    ```bash
    npm install cors
    npm install -D @types/cors
    ```
2.  **Serverconfiguratie aanpassen**:\
    Zorg ervoor dat de server de juiste CORS headers terug geeft. Gebruik het CorsOptions object om alle headers samen te stellen.



    ```javascript
    import cors from 'cors';

    const options: cors.CorsOptions = {
        origin : 'http://example.com',
        methods : 'GET,POST,PUT,DELETE'
    }

    app.use(cors(options));
    ```


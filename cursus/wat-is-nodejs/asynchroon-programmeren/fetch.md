# Fetch

Net zoals in de browser is het mogelijk om in Node.js een HTTP request te doen naar een andere server. Dit doe je met de `fetch` functie. Deze functie heeft als argument een URL. De functie geeft een Promise terug die een Response object bevat. Dit object bevat de data die je terugkrijgt van de server. In TypeScript is het wel belangrijk dat je het type van de data opgeeft die je verwacht terug te krijgen. Je moet dus een interface voorzien die de data beschrijft.

De syntax is grotendeels hetzelfde als in JavaScript. Het enige verschil is dat je het type van de data moet opgeven.

## Interface

We gaan in dit voorbeeld gebruik maken van de [JSONPlaceholder](https://jsonplaceholder.typicode.com/) API. Deze API bevat een aantal endpoints die je kan gebruiken om data op te halen. We gaan in dit voorbeeld gebruik maken van de `/posts` endpoint. Deze endpoint geeft een lijst van gebruikers terug.

```json
[
  {
    "userId": 1,
    "id": 1,
    "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
    "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
  },
  {
    "userId": 1,
    "id": 2,
    "title": "qui est esse",
    "body": "est rerum tempore vitae\nsequi sint nihil reprehenderit dolor beatae ea dolores neque\nfugiat blanditiis voluptate porro vel nihil molestiae ut reiciendis\nqui aperiam non debitis possimus qui neque nisi nulla"
  },
  ...
  {
    "userId": 10,
    "id": 100,
    "title": "at nam consequatur ea labore ea harum",
    "body": "cupiditate quo est a modi nesciunt soluta\nipsa voluptas error itaque dicta in\nautem qui minus magnam et distinctio eum\naccusamus ratione error aut"
  }
]
```

Het eerste wat je moet doen is een interface maken die de data beschrijft die je verwacht terug te krijgen. In dit geval is dit een array van objecten. Elk object heeft een userId, id, title en body property. De userId en id property zijn van het type number. De title en body property zijn van het type string.

```typescript
interface Post {
    userId: number;
    id: number;
    title: string;
    body: string;
}
```

Je kan deze interface zelf maken, maar je kan ook gebruik maken van een tool zoals [QuickType](https://app.quicktype.io/) om deze automatisch te genereren. Zorg vooral dat de interface correct is en overeenkomt met de data die je verwacht terug te krijgen.

### Fetch

Nu kunnen we de fetch functie gebruiken om de data op te halen. We geven als argument de URL van de endpoint mee. Omdat de fetch functie een Promise teruggeeft, kunnen we de then functie gebruiken om de data te gebruiken. Omdat over het algemeen de data die je terugkrijgt van een server een JSON object is, moeten we de data eerst omzetten naar een JavaScript object. Dit doen we met de `json` functie. Deze functie geeft ook een Promise terug. We kunnen dus de then functie gebruiken om de data te gebruiken.

Stel dat we de titel van de eerste post willen loggen naar de console. We kunnen dit doen met de volgende code:

```typescript
fetch('https://jsonplaceholder.typicode.com/posts')
    .then((response) => response.json())
    .then((response: Post[]) => {
        console.log(response[0].title);
    }).catch((error) => {
        console.log(error);
    });
```

of met async en await:

```typescript
(async function () {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts');
        const posts : Post[] = await response.json();
        console.log(posts[0].title);
    } catch (error: any) {
        console.log(error);
    }
})();
```

Let op dat een API niet altijd een array teruggeeft. Het kan ook een object zijn dat op zijn beurt weer een array bevat. Je moet dus altijd controleren wat de data is die je terugkrijgt.

## Error afhandelen

De catch functie is nodig om een error af te handelen. Onder een errors vallen alleen errors die veroorzaakt worden op netwerk niveau. Dus bijvoorbeeld als de server niet bereikbaar is of als de URL niet bestaat.

Als je toch een error wil afhandelen die veroorzaakt wordt door een fout in de code van de server, dan moet je de status code van de response controleren. Als de status code 2xx is, dan is er geen error. Als de status code iets anders is, dan is er een error.

```typescript
fetch('https://jsonplaceholder.typicode.com/posts/123')
    .then(r => {
        if (!r.ok) throw new Error(r.status)
        return r.json()
    })
    .then(r => console.log(r))
    .catch(e => console.log(e));
```

We kijken hier na of de status code niet 2xx is aan de hand van de `ok` property. Deze property is `true` als de status code 2xx is. Als de status code niet 2xx is, dan gooien we een error.

Deze code is ook weer sterk te vereenvoudigen met async en await:

```typescript
(async function () {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts/123');
        if (!response.ok) throw new Error(response.status);
        const posts : Post[] = await response.json();
        console.log(posts[0].title);
    } catch (error: any) {
        console.log(error);
    }
})();
```

Je kan ook de `status` property gebruiken om de status code op te vragen. Deze property bevat een nummer.

```typescript
(async function () {
    try {
        const response = await fetch('https://jsonplaceholder.typicode.com/posts/123');
        
        if (response.status === 404) throw new Error('Not found');
        if (response.status === 500) throw new Error('Internal server error');

        const posts : Post[] = await response.json();
        console.log(posts[0].title);
    } catch (error: any) {
        console.log(error);
    }
})();
```

## Een voorbeeld met paging

We gaan nu een iets complexer voorbeeld bekijken. We gaan deze keer eens de `https://reqres.in/api/users` API gebruiken. Als je naar de response kijkt, dan zie je dat deze geen array teruggeeft, maar een object. Dit object bevat een array met de key `data` en ook een andere properties zoals `page`, `per_page`, `total` en `total_pages`. Het data object bevat een array van gebruikers.

Hier kan je de volgende interface voor gebruiken:

```typescript
interface User {
    id: number;
    email: string;
    first_name: string;
    last_name: string;
    avatar: string;
}

interface RootObject {
    page: number;
    per_page: number;
    total: number;
    total_pages: number;
    data: User[];
}
```

We gaan nu de gebruikers ophalen en de gebruikers te loggen naar de console.

```typescript
async function main() {
    try {
        const response = await fetch('https://reqres.in/api/users');
        if (!response.ok) throw new Error(response.statusText);
        const users : RootObject = await response.json();
        for (const user of users.data) {
            console.log(user.first_name);
        }
    } catch (error: any) {
        console.log(error);
    }
};
main();
```

Merk op dat we hier wel geen rekening hebben gehouden met de pagina's. Als je naar de response kijkt zie je dat hier een `page` property in zit. Deze property geeft aan op welke pagina je zit. Als je naar de URL kijkt, dan zie je dat er een `page` query parameter in zit. Deze parameter geeft aan op welke pagina je zit. Als je deze parameter aanpast, dan krijg je een andere pagina terug. Je zou hier dus een loop kunnen maken die alle pagina's afgaat.

```typescript
async function main() {
    try {
        let page : number = 1;
        let total_pages : number = 1;

        while (page <= total_pages) {
            const response = await fetch("https://reqres.in/api/users?page=" + page);
            if (!response.ok) throw new Error(response.statusText);
            const root : RootObject = await response.json();
            total_pages = root.total_pages;
            console.log("Page " + page);
            for (const user of root.data) {
                console.log(user.first_name);
            }
            page++;
        }
    } catch (error: any) {
        console.log(error);
    }
};
main();
```

Let wel op dat elk paging systeem anders is. Je moet dus altijd controleren hoe het paging systeem werkt.

## Hoe bouw je je code nu best op? / Best Practices

De onderstaande code haalt informatie over "lemon"-cocktails op die een bepaald ingrediënt bevatten en toont de namen van de ontvangen cocktails gescheiden door een komma terug.

1. **Interfaces**: Er zijn twee `interfaces` gedefinieerd, `Cocktail` en `ResponseFormApi`. Deze beschrijven de structuur van de gegevens die uit de API worden verkregen.
2. **Functie getCocktailByIngredient**: Dit is een asynchrone functie die gegevens ophaalt van de Cocktail API. Het neemt een ingrediënt als een parameter (als een `string`) en stuurt een verzoek naar de API om alle cocktails te krijgen die dat ingrediënt bevatten. De functie heeft als return datatype een Promise dat uiteindelijk **ResponseFormApi** zal ontvangen.
3. **Functie main**: In de `main`-functie wordt de `getCocktailByIngredient`-functie aangeroepen met "lemon" als ingrediënt. Vervolgens worden de namen van de cocktails met "lemon" als ingrediënt verzameld en samen met een komma ertussen op het scherm geprint.

Kortom, het programma haalt de namen op van alle cocktails die "lemon" bevatten en laat deze zien.

```javascript
interface Cocktail {
  strDrink: string;
  idDrink: string;
  strDrinkThumb: string;
}
interface ResponseFormApi {
  drinks: Cocktail[];
}

async function getCocktailByIngredient(str: string): Promise<ResponseFormApi> {
  try{
    const response = await fetch(
      "https://www.thecocktaildb.com/api/json/v1/1/filter.php?i=" + str
    );
    const data = await response.json();
    return data;
  }catch(error){
    throw error
  }
}

async function main() {
  try{
    const lemonCocktails = await getCocktailByIngredient("lemon");
    console.log(
      lemonCocktails.drinks.map((cocktail) => cocktail.strDrink).join(", ")
    );
  }
  catch (error) {
    console.log("Error fetching cocktaildata")
  }  
}

main();
```

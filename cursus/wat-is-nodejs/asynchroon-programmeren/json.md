# JSON

### import statement

Je kan aan de hand van het `import` statement in TypeScript een JSON bestand inlezen. Dit is handig als je bijvoorbeeld een configuratie bestand hebt dat je wil inlezen of dat je een lijst van objecten wil inlezen vanuit een bestand.

Stel dat je een JSON bestand `users.json` hebt met de volgende inhoud:

```json
[
  {
    "name": "Andie",
    "age": 30,
    "address": {
      "street": "Fakestreet",
      "number": 133,
      "city": "Fakegem"
    }
  },
  {
    "name": "Debbie",
    "age": 25,
    "address": {
      "street": "Fakestreet",
      "number": 133,
      "city": "Fakegem"
    }
  }
]
```

Dan kan je dit bestand inlezen aan de hand van het `import` statement:

```typescript
import data from "./users.json";
```

Je moet hier wel op letten dat je in je `tsconfig.json` bestand de volgende optie hebt aangezet:

```json
{
  "compilerOptions": {
    ...
    "resolveJsonModule": true
    ...
  }
}
```

Je moet dan nog wel de inhoud van `usersJson` in een variabele of constante steken:

```typescript
const users: User[] = data;
```

Het is niet altijd mogelijk om een bestand in te lezen aan de hand van het `import` statement. Als je bijvoorbeeld een bestand wil inlezen dat niet in je project zit en ergens anders op je computer staat dan kan je dit niet inlezen aan de hand van het `import` statement. In dat geval kan je gebruik maken van de `fs` module.

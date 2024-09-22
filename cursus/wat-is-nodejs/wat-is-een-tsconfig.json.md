# Wat is een tsconfig.json?

Dit is een bestand dat vertelt hoe TypeScript moet werken wanneer het jouw TypeScript-code omzet naar JavaScript. Het bevat instellingen die de manier waarop TypeScript zich gedraagt, kunnen aanpassen. Hier zijn de belangrijkste instellingen die je vaak zult gebruiken:

#### 1. **`compilerOptions`**

Dit is de belangrijkste sectie in het bestand. Hier zet je de regels voor hoe TypeScript moet werken. Binnen deze sectie heb je een aantal opties:

* **`target`**: Dit bepaalt naar welke versie van JavaScript je TypeScript moet worden omgezet. Bijvoorbeeld, als je zegt `"target": "es5"`, dan zal TypeScript de code omzetten naar een versie van JavaScript die oudere browsers begrijpen. Als je `"es6"` kiest, krijg je een nieuwere versie van JavaScript.
* **`module`**: Dit vertelt hoe TypeScript om moet gaan met modules (stukjes code die je importeert en exporteert). Vaak gebruik je `"commonjs"` voor Node.js-projecten of `"es6"` voor moderne projecten.
* **`strict`**: Als deze op `true` staat, dwingt TypeScript je om heel precies te zijn met types, wat helpt om fouten in je code te voorkomen.
* **`outDir`**: Dit geeft de map aan waar de omgezette JavaScript-bestanden naartoe moeten. Bijvoorbeeld, als je `"outDir": "./build"` instelt, dan komen alle omgezette bestanden in de `build`-map.
* **`rootDir`**: Dit geeft de map aan waar je TypeScript-bestanden staan. Bijvoorbeeld, als je `"rootDir": "./src"` instelt, kijkt TypeScript naar alle bestanden in de `src`-map.

#### 2. **`include`**

Met deze instelling geef je aan welke bestanden TypeScript moet compileren. Bijvoorbeeld: `"include": ["src/**/*"]` betekent dat alle bestanden in de `src`-map, en alle submappen, worden meegenomen.

#### 3. **`exclude`**

Hier geef je aan welke bestanden of mappen TypeScript **niet** moet compileren. Bijvoorbeeld: `"exclude": ["node_modules"]` betekent dat TypeScript de `node_modules`-map overslaat, wat logisch is omdat deze map meestal door andere programma's wordt beheerd.

#### Samenvatting:

Het `tsconfig.json`-bestand bepaalt hoe TypeScript je code compileert naar JavaScript en helpt je om instellingen zoals de versie van JavaScript, modules, en welke mappen wel of niet meegenomen moeten worden te beheren. Dit zorgt ervoor dat je project soepel en zonder problemen werkt!

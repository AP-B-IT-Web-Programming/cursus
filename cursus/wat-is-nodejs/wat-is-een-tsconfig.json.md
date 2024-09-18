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

#### 4. **`typeRoots`**

Met de instelling **`typeRoots`** kun je expliciet aangeven in welke mappen TypeScript moet zoeken naar deze type-definitiebestanden.

#### Standaardgedrag zonder `typeRoots`

Normaal gesproken zoekt TypeScript automatisch naar type-definitiebestanden in de map `node_modules/@types`, omdat veel bibliotheken hun types daarin opslaan. Maar als je specifieke mappen hebt waar je eigen type-definitiebestanden staan, dan kun je `typeRoots` gebruiken om TypeScript naar die mappen te laten zoeken.

#### Hoe gebruik je `typeRoots`?

```json
{
  "compilerOptions": {
    "typeRoots": ["./types", "./node_modules/@types"]
  }
}
```

In dit voorbeeld:

* **`./types`**: Dit zou een eigen map kunnen zijn waar je zelfgemaakte `.d.ts`-bestanden staan.
* **`./node_modules/@types`**: Dit is de standaardlocatie waar TypeScript zoekt naar types voor geïnstalleerde bibliotheken.

#### Wat gebeurt er als je `typeRoots` gebruikt?

Zodra je deze optie instelt, zal TypeScript **alleen** in de mappen zoeken die je hier hebt opgegeven. Dus als je bijvoorbeeld `./node_modules/@types` vergeet op te nemen, kan het zijn dat TypeScript de types voor externe pakketten niet meer vindt!

#### Wanneer gebruik je `typeRoots`?

* Als je je eigen type-definitiebestanden hebt die niet in de standaardmappen staan.
* Als je meer controle wilt over waar TypeScript naar types zoekt **bijvoorbeeld als je deze globaal hebt geïnstalleerd**.

#### Hoe bepaal je waar je globale types staan ?

Om je globale types toe te voegen aan tsconfig moet je eerst weten waar deze net op je schijf staan. Gebruik hiervoor het commando:

```bash
npm root -g
```

Op windows is dat dan bijvoorbeeld : TODO

En op mac zou dat dan kunnen zijn : /usr/local/lib/node\_modules

Je globale types staan dan in subfolder @types van deze root folder.

{% hint style="success" %}
Voeg volgende lijn toe aan de compileroptions van je tsconfig zodat je klaar bent om aan de slag te gaan met de volgende onderdelen van de cursus:
{% endhint %}

```json
"typeRoots": ["<jouw global root>/@types", "./node_modules/@types"]
```

#### Samenvatting:

Het `tsconfig.json`-bestand bepaalt hoe TypeScript je code compileert naar JavaScript en helpt je om instellingen zoals de versie van JavaScript, modules, en welke mappen wel of niet meegenomen moeten worden te beheren. Dit zorgt ervoor dat je project soepel en zonder problemen werkt!

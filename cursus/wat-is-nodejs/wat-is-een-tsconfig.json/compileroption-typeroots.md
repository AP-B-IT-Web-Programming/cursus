# compilerOption typeRoots

Met de instelling **`typeRoots`** kun je expliciet aangeven in welke mappen TypeScript moet zoeken naar de type-definitiebestanden.

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

Op windows is dat dan bijvoorbeeld : C:/Users/\<name>/AppData/Roaming/npm/node\_modules

En op mac zou dat dan kunnen zijn : /usr/local/lib/node\_modules

Je globale types staan dan in subfolder @types van deze root folder.

{% hint style="success" %}
Voeg volgende lijn toe aan de compileroptions van je tsconfig zodat je klaar bent om aan de slag te gaan met de volgende onderdelen van de cursus:
{% endhint %}

```json
"typeRoots": ["<jouw global root>/@types", "./node_modules/@types"]
```

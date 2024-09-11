# Nieuw project

Om een node applicatie te kunnen schrijven moet en we uiteraard eerst node.js installeren. Surf naar [https://nodejs.org](https://nodejs.org/en) en klik op de grote download knop om de laatste LTS versie te installeren.

Start nadien je Visual Studio Code (VSC) op en maak een nieuwe folder aan waar we onze code in kunnen plaatsen.

We zullen in dit geval een nieuwe folder aanmaken met de naam `hello`. Je kan deze in een folder`theorie` plaatsen.

Vervolgens zorg je ervoor dat je in de `hello` directory zit aan de hand van het `cd` commando dat je kan uitvoeren in de terminal van je VSC

```bash
cd theorie/hello
```

Nu moeten we **eenmalig** nog een aantal installaties doen voor we kunnen beginnen programmeren.

## TypeScript installatie

We gaan met TypeScript werken, dus moeten we dit installeren. Hiervoor gebruiken we de Node Package Manager (npm) die automatisch mee geïnstalleerd werd met je node.js installatie. We komen later nog uitgebreid terug op het gebruik van npm.

```
npm install -g typescript
```

Later leggen we meer uit over het gebruik van npm, weet nu dat de -g aanduiding wil zeggen dat we deze bibliotheek globaal installeren.

Opgelet ! Mac gebruikers moeten globaal installeren met administrator rechten. Het commando wordt dan:

```
sudo npm install -g typescript
```

Vervolgens ze je je wachtwoord moeten ingeven voor de globale bibliotheek geïnstalleerd wordt.

## Node types installeren

Nu installeren we de node types. Dit zijn de types die nodig zijn om met TypeScript en Node.js te werken.

```bash
npm install -g @types/node
```

Mac gebruikers denk aan het sudo commando!

## TS Node installeren

Zoals in de introductie uitgelegd kan je TypeScript niet rechtstreeks uitvoeren. We gebruiken hiervoor een transpiler die de TypeScript omvormt naar JavaScript en vervolgens kan uitvoeren.

```bash
npm install -g ts-node
```

Mac gebruikers denk aan het sudo commando!

## npm init

Nu gaan we een nieuw project aanmaken. Dit doen we aan de hand van het `npm init` commando.

```bash
npm init
```

Dit commando zal een aantal vragen stellen over jouw project. Je kan deze gewoon beantwoorden door op enter te drukken. Als je dit commando hebt uitgevoerd zal je een nieuw bestand `package.json` zien in je directory. Dit bestand bevat alle informatie over jouw project. We zullen hier later nog op terugkomen.

## TypeScript configuratie

Nu we een nieuw project hebben aangemaakt moeten we een nieuwe TypeScript configuratie aanmaken. Dit doen we aan de hand van het `tsc --init` commando.

```bash
tsc --init
```

Dit commando zal een nieuw bestand `tsconfig.json` aanmaken in je directory. Dit bestand bevat alle configuratie opties voor de TypeScript compiler.

## Bestand aanmaken

Nu we alle configuratie hebben aangemaakt kunnen we beginnen met het schrijven van onze code. Maak een nieuw bestand `hello.ts` aan in de `hello` directory.&#x20;

Het bestand `hello.ts` moet het volgende bevatten:

```typescript
console.log('Hello, world!');
```

## Uitvoeren

Nu we ons programma hebben geschreven kunnen we dit uitvoeren. Dit kan je doen aan de hand van het `ts-node` commando.

```bash
ts-node hello.ts
```

Dit commando zal je programma uitvoeren en je zal `Hello, world!` zien verschijnen in je terminal.

## Samengevat

| Commando                 | Beschrijving                                                                          |
| ------------------------ | ------------------------------------------------------------------------------------- |
| `npm init`               | Maakt een nieuw project aan.                                                          |
| `tsc --init`             | Maakt een nieuw tsconfig bestand aan. Het initialiseert een nieuw TypeScript project. |
| `ts-node <naam file>.ts` | Voert het programma uit dat je geschreven hebt in `<naam file>.ts`.                   |

Deze commando's zal je voor elk nieuw project moeten uitvoeren. Het is dus handig om deze te onthouden.

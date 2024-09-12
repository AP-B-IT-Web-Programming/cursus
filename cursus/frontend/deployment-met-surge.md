# Deployment met Surge

## Introductie

In dit hoofdstuk maken we gebruik van Surge.sh om onze webpage te hosten.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Screenshot from surge.sh</p></figcaption></figure>

[Surge.sh](https://www.surge.sh) is een cloud-gebaseerde dienst die eenvoudig en snel statische websites kan hosten. Het is populair onder ontwikkelaars omdat het een zeer eenvoudige interface biedt voor het deployen van statische sites, zoals HTML, CSS, en JavaScript projecten, naar het web.

## Installatie

installeer éénmalig Surge door middel van het volgende commando

```
npm i -g surge
```

## Gebruik

Geef in de terminal het volgende commando in:&#x20;

```bash
surge
```

Surge zal dan vragen welke folder je wil publiceren. Hier geef je dus je 'dist' folder in. Surge zal dan een random domeinnaam voorstellen. Je kan deze wijzigen zolang deze maar eindigt op surge.sh.

### Kan dit sneller?

ja, dit alles kan tevens in 1 commando:&#x20;

```bash
surge /dist mijngewenstdomein.surge.sh
```


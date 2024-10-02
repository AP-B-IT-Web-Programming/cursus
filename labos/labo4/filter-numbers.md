# Filter Numbers

Maak een nieuw project aan met de naam `filter-numbers`.

Maak een class `NumberFilter` aan.

## Deel 1

Schrijf een method`filterPositive` die een array van getallen als parameter verwacht. De method `filterPositive` moet een nieuwe array teruggeven met enkel de positieve getallen uit de array die als parameter werd meegegeven. Deze functie **MOET** aan de hand van een **`for`-loop** geschreven worden en mag **geen** gebruik maken van de **ingebouwde functie `filter` van een array**.

Roep de method`filterPositive` aan met de volgende array als parameter:

```typescript
const numberFilter: NumberFilter = new NumberFilter();
const numbers: number[] = [-4,-4,1,2,3,4,5];

console.log(numberFilter.filterPositive(numbers)); // 1,2,3,4,5
```

## Deel 2

Schrijf een method`filterNegative` die een array van getallen als parameter verwacht. De method`filterNegative` moet een nieuwe array teruggeven met enkel de negatieve getallen uit de array die als parameter werd meegegeven.

Roep de method `filterNegative` aan met de volgende array als parameter:

```typescript
const numberFilter: NumberFilter = new NumberFilter();
const numbers: number[] = [-4,-4,1,2,3,4,5];

console.log(numberFilter.filterNegative(numbers)); // -4,-4
```

## Deel 3

Schrijf een method`filterEven` die een array van getallen als parameter verwacht. De method `filterEven` moet een nieuwe array teruggeven met enkel de even getallen uit de array die als parameter werd meegegeven.

Roep de method `filterEven` aan met de volgende array als parameter:

```typescript
const numberFilter: NumberFilter = new NumberFilter();
const numbers: number[] = [-4,-4,1,2,3,4,5];

console.log(numberFilter.filterEven(numbers)); // -4,-4,2,4
```

## Deel 4

Schrijf nu een method `filter` die een array van getallen als eerste parameter verwacht en een functie als tweede parameter. De method `filter` moet een nieuwe array teruggeven met enkel de getallen uit de array die als eerste parameter werd meegegeven waarvoor de functie die als tweede parameter werd meegegeven `true` teruggeeft.

Voorbeeld van gebruik:

```typescript
const numberFilter: NumberFilter = new NumberFilter();
const numbers: number[] = [-4,-4,1,2,3,4,5];
const isPositive = (number: number) => number >= 0;

console.log(numberFilter.filter(numbers, isPositive)); // 1,2,3,4,5
```

Maak naast de `isPositive` ook de `isNegative` en de `isEven` functies.

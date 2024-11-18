# Uitvinders

Deze oefening is een herhaling op werken met arrays.

Voor deze oefening heb je géén VITE project nodig !

Gegeven volgende array van uitvinders

\[

&#x20; { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },

&#x20; { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },

&#x20; { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },

&#x20; { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },

&#x20; { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },

&#x20; { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },

&#x20; { first: 'Max', last: 'Planck', year: 1858, passed: 1947 },

&#x20; { first: 'Katherine', last: 'Blodgett', year: 1898, passed: 1979 },

&#x20; { first: 'Ada', last: 'Lovelace', year: 1815, passed: 1852 },

&#x20; { first: 'Sarah E.', last: 'Goode', year: 1855, passed: 1905 },

&#x20; { first: 'Lise', last: 'Meitner', year: 1878, passed: 1968 },

&#x20; { first: 'Thomas', last: 'Edison', year: 1847, passed: 1931 }

]

1. Zorg voor een correcte interface
2.  Filter de lijst op uitvinders die geboren zijn in de 16e eeuw

    &#x20;Verwachte uitkomst:\
    &#x20;{ first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 }, { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 }&#x20;
3. Maak een array met daarin alle geboortejaren van de uitvinders\
   &#x20;Verwachte uitkomst: \[1879, 1643, 1564, 1867, 1571, 1473, 1858, 1898, 1815, 1855, 1878, 1847];
4.  Maak een array met daarin alle volledige namen van de uitvinders (dus voor- en achternaam als één string)

    &#x20;Verwachte uitkomst:\
    &#x20;\[ 'Albert Einstein', 'Isaac Newton', 'Galileo Galilei', 'Marie Curie', 'Johannes Kepler', 'Nicolaus Copernicus', 'Max Planck', 'Katherine Blodgett', 'Ada Lovelace', 'Sarah E. Goode', 'Lise Meitner', 'Thomas Edison']
5.  Sorteer de uitvinders op geboortejaar, oplopend van oudste naar jongste uitvinder

    &#x20;Verwachte uitkomst:\
    &#x20;\[   { first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },

    &#x20;  { first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },

    &#x20;  { first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },

    &#x20;  { first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },

    &#x20;  { first: 'Ada', last: 'Lovelace', year: 1815, passed: 1852 },

    &#x20;  { first: 'Thomas', last: 'Edison', year: 1847, passed: 1931 },

    &#x20;  { first: 'Sarah E.', last: 'Goode', year: 1855, passed: 1905 },

    &#x20;  { first: 'Max', last: 'Planck', year: 1858, passed: 1947 },

    &#x20;  { first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },

    &#x20;  { first: 'Lise', last: 'Meitner', year: 1878, passed: 1968 },

    &#x20;  { first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },

    &#x20;  { first: 'Katherine', last: 'Blodgett', year: 1898, passed: 1979 }

    &#x20;]
6.  Sorteer de uitvinders op hoeveel jaren ze geleefd hebben, van langste leven naar kortste leven

    &#x20;Verwachte uitkomst:

    &#x20;\[

    &#x20;{ first: 'Lise', last: 'Meitner', year: 1878, passed: 1968 },

    &#x20;{ first: 'Max', last: 'Planck', year: 1858, passed: 1947 },

    &#x20;{ first: 'Isaac', last: 'Newton', year: 1643, passed: 1727 },

    &#x20;{ first: 'Thomas', last: 'Edison', year: 1847, passed: 1931 },

    &#x20;{ first: 'Katherine', last: 'Blodgett', year: 1898, passed: 1979 },

    &#x20;{ first: 'Galileo', last: 'Galilei', year: 1564, passed: 1642 },

    &#x20;{ first: 'Albert', last: 'Einstein', year: 1879, passed: 1955 },

    &#x20;{ first: 'Nicolaus', last: 'Copernicus', year: 1473, passed: 1543 },

    &#x20;{ first: 'Marie', last: 'Curie', year: 1867, passed: 1934 },

    &#x20;{ first: 'Johannes', last: 'Kepler', year: 1571, passed: 1630 },

    &#x20;{ first: 'Sarah E.', last: 'Goode', year: 1855, passed: 1905 },

    &#x20;{ first: 'Ada', last: 'Lovelace', year: 1815, passed: 1852 }

    &#x20;]
7. Vind de gegevens over de uitvinder wiens achternaam 'Edison' is.\
   Verwachte uitkomst: { first: 'Thomas', last: 'Edison', year: 1847, passed: 1931 }

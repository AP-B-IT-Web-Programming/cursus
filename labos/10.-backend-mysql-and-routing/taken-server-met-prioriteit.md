# Taken server met prioriteit

Een taak heeft nu een prioriteit. Hoe lager de prioriteit, hoe sneller het opgelost moet worden.

De prioriteit is uniek, het kan dus niet zijn dat een taak eenzelfde prioriteit heeft als een andere taak.

Bij aanmaak van een taak komt deze steeds achteraan het prioriteitenlijstje. Heb je bijvoorbeeld al drie taken met prioriteit 1 , 2 en 3, dan zal de nieuwe taak prioriteit 4 krijgen. Zijn er geen taken, dan krijgt de nieuwe taak prioriteit 1.

Bij GET tasks sorteer je de taken op prioriteit, laagst eerst;

De GET task haalt steeds de prioriteit 1 op.

De DELETE task zal nog steeds een taak weghalen én zorgt ervoor dat de nummering wordt bijgewerkt zodat er geen gat ontstat.

Voeg nu nog een nieuwe API toe: POST task-urgent. Deze voegt een taak toe met prioriteit 1 en past alle prioriteiten van de andere taken aan.

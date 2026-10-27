---
cssclasses:
  - smart-iot
tags:
  - network-infrastructure
---
> [!summary] In breve
> L'**IoT Data Management and Compute Stack** è l'insieme di tecnologie, software, componenti hardware e processi utilizzato per raccogliere, filtrare, elaborare, archiviare e analizzare i dati generati dai dispositivi dell'Internet of Things (IoT).  ==Invece di inviare ogni singolo dato grezzo direttamente al cloud (generando traffico eccessivo e latenza), questo stack organizza l'elaborazione su più livelli gerarchici==.
 > <p align="center">   <img src="DataManagement-computeStack.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 200px; max-width: 100%; height: auto;" /> </p>


## Livello 1 - Edge
Esegue l'==elaborazione dei dati direttamente a bordo dei singoli dispositivi ==(*on-board*), garantendo reazioni immediate in tempo reale basate sugli eventi. Riduce il consumo di banda inviando solo allarmi o sintesi di eventi invece di flussi continui di dati grezzi, come nelle telecamere di videosorveglianza smart.

## Livello 2 - Fog
Utilizza nodi intermedi per aggregare, filtrare e pre-elaborare i dati provenienti da più *smart objects* senza gravare sui sistemi centrali. Implementa ==anelli di controllo distribuiti capaci di prendere decisioni tempestive a bassissima latenza==, azzerando i ritardi delle comunicazioni esterne.

## Livello 3 - Cloud
Fornisce ==capacità computazionali e di archiviazione centralizzate== per elaborare grandi quantità di dati storici (*data at rest*) tramite interrogazioni (*query-based*). Esegue analisi avanzate di lungo periodo e reportistica con tempi di risposta transazionali e non vincolati dal tempo reale.

---
cssclasses:
  - smart-iot
tags:
  - network-infrastructure
aliases:
  - IoTWF
---
> [!summary] In breve
> Il modello **IoTWF** (Internet of Things World Forum), promosso nel 2014 da aziende come Cisco, è un'architettura standard a **7 livelli** creata per strutturare i sistemi IoT. Serve a mappare in modo ordinato come i dati viaggiano dal sensore fisico fino ai processi decisionali aziendali. <p align="center">   <img src="IoTWF-architecture.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 650px; max-width: 100%; height: auto;" /> </p>

## Le Due Macro-Aree

1. **Livelli 1-3: Il Mondo OT (Operational Technology)**
   Operano sull'"Edge", ovvero vicino a dove i dati vengono generati. I dispositivi fisici raccolgono dati grezzi (L1), li trasmettono (L2) e subiscono una prima elaborazione immediata (L3, *Fog Computing*) per ridurre la latenza ed evitare di intasare la rete inviando dati inutili.
2. **Livelli 4-7: Il Mondo IT (Information Technology)**
   Operano nel Cloud o nei Data Center centrali. I dati in movimento si trasformano in dati a riposo (L4), vengono normalizzati e aggregati (L5), analizzati da software specifici (L6) fino a innescare decisioni di business o interazioni umane (L7).

## Differenze chiave con il Modello ISO/OSI
Mentre l'[[Modello ISO OSI|ISO OSI]] standardizza *come* i dati viaggiano su una rete, l'**IoTWF** descrive il ==🟡*ciclo di vita* dei dati== e dell'intero ecosistema aziendale. Le differenze principali sono:

| Caratteristica                   | Modello ISO/OSI                                                       | Modello IoTWF                                                                                               |
| :------------------------------- | :-------------------------------------------------------------------- | :---------------------------------------------------------------------------------------------------------- |
| **Scopo**                        | Modello di **telecomunicazione** (trasporto dei pacchetti).           | Modello **architetturale e logico** (gestione del dato dall'hardware al business).                          |
| **Estensione**                   | Si ferma al livello Applicazione (la consegna del dato al software).  | Va oltre: ==🟡include cosa succede *dopo*== (storage, big data, analytics) ==🟡fino alle decisioni umane==. |
| **Elaborazione vs Trasmissione** | Si disinteressa dell'elaborazione hardware, conta solo che trasmetta. | Integra nativamente i concetti di **Edge/Fog Computing** (elaborazione locale prima dell'invio).            |
## Stesso problema diversi paradigmi
Essendo il paradigma ISO/OSI limitato all'interno del mondo IOT è stato teorizzato il modello IoTWF che dirama in modo dettagliato il workflow ideale di un'infrastruttura IOT complessa. Tuttavia diversi problemi necessitano edi diversi punti di vista e diversi paradigmi d'approccio, per tanto sulla base di questo modello sono stati definiti 2 stack funzionali paralleli che deviniscono il comportamento di un'architettura IOT da 2 punti di vista contrapposti:
- Quello infrastrutturale: [[Functional stack]]
- Quello dell'elaborazione dei dati: [[Data management & compute stack]]


Poiché il modello ISO/OSI mostra limiti evidenti applicato all'IoT, è stato introdotto il modello di riferimento **IoTWF** (IoT World Forum), ideato per delineare nel dettaglio il flusso di lavoro ideale di un'infrastruttura IoT complessa.

Tuttavia, sfide eterogenee richiedono prospettive e paradigmi di approccio differenti. Per questo motivo, a partire da tale modello, sono stati definiti due stack funzionali paralleli che descrivono il comportamento dell'architettura da due punti di vista complementari:
- **Infrastrutturale:** [[Functional stack]]
- **Elaborazione e gestione dei dati:**  [[Data management & compute stack]]
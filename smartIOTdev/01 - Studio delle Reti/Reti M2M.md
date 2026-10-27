---
aliases:
  - M2M
  - machine to machine
tags:
  - network-infrastructure
  - automation
cssclasses:
  - smart-iot
---
> [!summary] Abstract
> Le reti M2M (Machine-to-Machine) sono un tipo di architetuttra di rete composta da tecnologie che permettono ai dispositivi di rete (cablati o wireless) di scambiare informazioni e svolgere azioni in modo autonomo, **senza alcun intervento umano**. ==🟡È il precursore e il nucleo operativo dell'Internet of Things (IoT)==.

## Caratteristiche Principali

- **Comunicazione Diretta:** Spesso basata su architetture punto-punto (point-to-point) o verso un server centrale (hub-and-spoke) chiuso.
- **Traffico Specifico:** Genera flussi di ==🟡dati continui ma di piccole dimensioni== (micro-transazioni, telemetria, stato dei sensori).
- **Automazione Pura:** L'obiettivo principale è far reagire una macchina all'input di un'altra (es. un sensore di temperatura che fa scattare in automatico un sistema di raffreddamento).

## M2M vs IoT
Mentre l'IoT è un concetto ampio che coinvolge cloud, big data e interfacce utente (B2C), l'M2M è storicamente più focalizzato sull'hardware industriale (B2B), usando reti cellulari (SIM M2M), collegamenti seriali o reti locali isolate, e raramente espone i dati direttamente all'utente finale.

## Protocolli Tipici
- **[[MQTT]] / CoAP:** Per telemetria su reti IP.
- **[[Modbus]] / [[CAN bus]]:** Storici per automazione industriale.
- **NB-IoT / [[LoRaWAN]]:** Per sensori a basso consumo e lunga distanza.

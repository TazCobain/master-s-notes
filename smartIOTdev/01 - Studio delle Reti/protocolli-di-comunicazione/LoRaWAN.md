---
aliases:
  - LoRa
cssclasses:
  - smart-iot
tags:
  - IT-protocol
  - network-infrastructure
---
> [!abstract] LoRaWAN in Breve
> LoRaWAN è un protocollo di rete LPWAN per l'IoT a lunghissimo raggio e bassissimo consumo, che sfrutta la modulazione radio sub-GHz LoRa per trasmettere piccoli payload su distanze chilometriche. 
> Ottimizza il compromesso tra efficienza e latenza e garantisce comunicazioni sicure end-to-end con crittografia AES-128.

protocollo MAC/Routing per reti **LPWAN** (Low Power Wide Area Network) dedicato all'IoT. Usa la modulazione radio **LoRa** (Livello Fisico) su frequenze sub-GHz (es. 868 MHz in Europa).

> [!info] LoRa vs LoRaWAN
> **LoRa** è la tecnologia radio (il livello fisico). **LoRaWAN** è il protocollo di rete (gestisce topologia, sicurezza e routing).

## Architettura (Star-of-Stars)
`Nodi Sensore ➔ Gateway ➔ Network Server ➔ Application Server`
I gateway operano come ponti radio trasparenti: inoltrano i pacchetti dai nodi al server centrale tramite IP.

## Classi dei Dispositivi
- **Classe A (Default):** Autonomia massima (anni a batteria). Riceve dati (RX) solo in 2 brevi finestre subito dopo aver trasmesso.
- **Classe B (Beacon):** Consumo medio. Finestre di ricezione programmate sincronizzandosi con i beacon del gateway.
- **Classe C (Continuo):** Consumo alto (alimentati a rete). Finestra di ricezione sempre aperta (latenza quasi nulla).

## Sicurezza e Attivazione
Cifratura **AES-128** end-to-end con chiavi separate per rete e applicazione.
- **OTAA (Over-the-Air Activation):** Negoziazione dinamica delle chiavi. Più sicuro, raccomandato.
- **ABP (Activation by Personalization):** Chiavi statiche pre-programmate. Più veloce ma meno sicuro.

## Performance e Trade-off

> [!note] Il Triangolo dell'IoT
> Nelle reti LPWAN, le prestazioni non si misurano in "velocità pura", ma nel compromesso ideale tra **Distanza**, **Consumo** e **Capacità dati**.

- **Throughput (Velocità):** Estremamente basso (da 0.3 kbps a 50 kbps). Pensato per payload di pochi byte (es. temperatura, stato batteria). Inadatto per audio, video o navigazione web.
- **Raggio d'azione:** Chilometrico. Circa 2-5 km in ambienti urbani densi, oltre 15 km in campo aperto (line-of-sight).
- **Consumo Energetico:** ==Irrisorio==. Un sensore in Classe A può operare dai 5 ai 10 anni con una singola batteria a bottone.
- **Resilienza al rumore:** ==Altissima==. Grazie alla modulazione CSS (*Spreading Factor* elevati), il segnale può essere decodificato anche se coperto dal rumore di fondo (SNR negativo).
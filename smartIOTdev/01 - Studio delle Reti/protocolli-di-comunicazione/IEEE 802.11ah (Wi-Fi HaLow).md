---
cssclasses:
  - smart-iot
aliases:
  - IEEE 802.11ah
  - WI-FI HaLow
tags:
  - network-infrastructure
  - IT-protocol
---
Estensione dello standard Wi-Fi operante nello spettro **Sub-1 GHz** (senza licenza). Progettato specificamente per applicazioni **IoT (Internet of Things)**, smart agriculture, smart city e sensoristica industriale, dove sono richieste lungo raggio e bassissimo consumo energetico.

> [!abstract] In Breve
> Wi-Fi HaLow ==combina la facilità d'integrazione e la sicurezza nativa del Wi-Fi== IP con la portata e l'efficienza energetica tipiche di tecnologie LPWAN (come Zigbee o LoRa), offrendo un raggio fino a **1 km** e throughput fino a decine di Mbps.

---

## Caratteristiche Fisiche (PHY Layer)

- **Banda di frequenza:** Bande ISM Sub-1 GHz (755–928 MHz a seconda delle normative regionali: es. 868 MHz Europa, 902–928 MHz USA).
- **Larghezza di canale:** Canali stretti da **1, 2, 4, 8 e 16 MHz** (i canali da 1 e 2 MHz sono obbligatori).
- **Modulazione:** OFDM (da BPSK fino a 256-QAM).
- **Data Rate:** Da un minimo di **150 kbps** (canale da 1 MHz con MCS0) fino a un massimo teorico di oltre **80 Mbps** (canale da 16 MHz con MCS9).
- **Propagazione e Penetrazione:** L'uso delle frequenze sub-GHz consente un'attenuazione nello spazio libero ridotta e una penetrazione di pareti e ostacoli nettamente superiore al Wi-Fi a 2.4/5 GHz.

---

## Meccanismi MAC per Risparmio Energetico e Scalabilità

IEEE 802.11ah introduce modifiche sostanziali al sottolivello MAC per supportare fino a **8191 stazioni (STA)** per singolo Access Point e ridurre al minimo il consumo di batteria:

### A. Gestione dell'Efficienza Energetica
- **Target Wake Time (TWT):** Permette all'AP e ai sensori di negoziare intervalli di sonno prestabiliti; i dispositivi possono dormire per ore o giorni senza perdere l'associazione di rete.
- **Header MAC compresso:** Formato dei frame alleggerito per ridurre l'overhead radio e il tempo di trasmissione su canali a basso bitrate.

### B. Gestione della Contesa (Scalabilità)
- **Restricted Access Window (RAW):** L'AP suddivide il tempo di accesso al canale in slot e assegna ciascun intervallo a un gruppo specifico di nodi. Questo riduce le collisioni del CSMA/CA in ambienti con migliaia di sensori.
- **Gerarchia AID (Association ID):** Struttura gerarchica a 4 livelli (Pagina, Blocco, Sub-blocco, Indice) per indirizzare e sincronizzare in modo efficiente migliaia di dispositivi.

---
## Struttura del Frame e Accesso al Canale

| Componente | Funzione |
| :--- | :--- |
| **Preamble Sub-1 GHz** | Sincronizzazione ottimizzata per canali a banda stretta (1/2 MHz). |
| **Short MAC Header** | Campi indirizzi ridotti (da 6 a 2 o 4 byte) per diminuire il consumo di bit. |
| **Controllo RAW** | Trasmissione confinata in finestre temporali dedicate per evitare contesa generalizzata. |
| **NDP (Null Data Packet)** | Frame di controllo ultra-compatti (es. ACK/CTS) privi di payload per velocizzare le risposte. |
> [!tip] Target Wake Time (TWT): Efficienza Energetica
> Il **Target Wake Time (TWT)** consente all'Access Point e ai nodi client di negoziare in anticipo schemi temporali precisi di attivazione. I dispositivi IoT possono spegnere la radio e rimanere in modalità *deep sleep* per ore, giorni o settimane, risvegliandosi solo negli istanti concordati per trasmettere o ricevere dati. ==Questo approccio azzera l'ascolto passivo (*idle listening*), minimizza le collisioni sul canale e prolunga la durata della batteria== dei sensori fino a oltre 5 anni.

---
## Confronto Tecnologico

| Tecnologia                | Banda             | Raggio Tipico | Throughput Tipico   | Target Principale                                       |
| :------------------------ | :---------------- | :------------ | :------------------ | :------------------------------------------------------ |
| **802.11ah (HaLow)**      | Sub-1 GHz         | ~1 km         | 150 kbps – 15+ Mbps | IoT/Smart Home ad alto throughput (video, firmware OTA) |
| **802.11b/g/n**           | 2.4 GHz           | ~50–100 m     | 11 – 300 Mbps       | Reti locali consumer/ufficio                            |
| **[[Zigbee (802.15.4)]]** | 2.4 GHz / Sub-GHz | ~10–100 m     | 250 kbps            | Reti mesh a bassissimo consumo                          |
| **[[LoRaWAN]]**           | Sub-1 GHz         | >5–10 km      | <50 kbps            | Telemetria a lungo raggio e pacchetti minimi            |

---

### collegamenti
[[Comunicazione wireless]]
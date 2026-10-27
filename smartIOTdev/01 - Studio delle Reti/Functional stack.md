---
cssclasses:
  - smart-iot
tags:
  - network-infrastructure
---
> [!summary] In breve
> Il Core IoT Functional Stack è un modo di interpretare i dati all è un framework architetturale semplificato che ==suddivide l'infrastruttura dell'Internet of Things (IoT) nei suoi tre blocchi funzionali fondamentali==. Questo modello serve a mappare il percorso dei dati dal mondo fisico fino alle piattaforme cloud dove vengono analizzati e trasformati in azioni. 
> 
> <p align="center">   <img src="CoreIOTfunztionalStack.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 350px; max-width: 100%; height: auto;" /> </p>

## Livello 1 - Things
È il livello di percezione, a diretto contatto con il mondo fisico. Include tutti gli oggetti intelligenti (_smart objects_) e i dispositivi hardware. Le sue funzioni si dividono tra **sensori** e **attuatori**. A questo livello va considerato

## Livello 2 - Communication Network
Questo stack si suddivide internamente in 4 sottolivelli.
### liv.2.1 Access network sub-layer
La progettazione di un'infrastruttura di rete non segue una formula universale, ma richiede una selezione tecnologica strettamente guidata dalle specifiche esigenze del problema da risolvere. 

Ogni architettura comporta infatti un delicato bilanciamento di compromessi operativi. In alcuni scenari potrebbe essere necessario adottare tecnologie fortemente orientate alla privacy, pur accettando un maggiore dispendio energetico; in altri contesti, si potrebbe optare per la reattività e l'estrema flessibilità dei sistemi Edge, consapevoli però di dover affrontare sfide più complesse sul fronte della sicurezza informatica. 
Il sistema ideale, pertanto, nasce sempre da un'attenta mediazione tra prestazioni, risorse disponibili e tolleranza al rischio.
![[networkChart.png]]

Questo sottolivello gestisce gli aspetti di ==🟡connessione a basso livello, corrispondenti ai livelli Fisico e Data Link del modello [[Modello ISO OSI|ISO/OSI]]==. Si occupa di definire le modalità con cui i dispositivi si collegano alla rete (via cavo o wireless), bilanciando quattro parametri fondamentali:
- **Copertura (Range)**
- **Throughput (Data Rate)**
- **Consumo energetico (Power)**
- **Costo marginale per connessione**

Le tecnologie d'accesso si dividono in base al raggio d'azione:
- **Contact / PAN (Personal Area Network):** raggio ridotto (da pochi centimetri a decine di metri), come Bluetooth, ZigBee, Thread o 6LoWPAN.
- **LAN / HAN / NAN (Local, Home, Neighborhood Area Network):** coperture fino a qualche centinaio di metri o pochi chilometri, come Wi-Fi (802.11a/b/g/n/ac/ax) e 802.11ah (HaLow Sub-1GHz).
- **WAN / FAN / LPWA (Wide, Field Area Network, Low Power Wide Area):** distanze elevate (fino a decine di chilometri) con consumi contenuti, come LoRaWAN, Sigfox, NB-IoT e reti cellulari (LTE/5G).
![[tecnology&range.png]]

> [!info] Topologia d'accesso 
> Tipi di configurazioni  principali della rete:
> - *Point-to-point* (punto-punto, meno comune).
> - *Point-to-multipoint* o *Cluster di point-to-multipoint* (es. Access Point domestico).
> - *Topologia ad albero (Tree)*.
> - *Topologia a maglia (Mesh)*, parziale o completa, orientata alla massima ridondanza.

---

### liv.2.2 Gateway & backhaul
Il **Gateway** è il ==🟡dispositivo di interconnessione== che raccoglie i dati generati dagli oggetti intelligenti circostanti (tramite la rete d'accesso) e li rilancia verso la stazione di elaborazione centrale attraverso la **rete di backhaul**.

Le tecnologie di **backhaul** includono collegamenti cablati (Ethernet) o wireless ad alto raggio/capacità (Wi-Fi, 802.11ah, WiMAX, reti cellulari LTE/5G). Alcune tecnologie (come il Wi-Fi) possono fungere sia da rete d'accesso sensore-gateway sia da connessione di backhaul verso la rete centrale, a seconda dell'architettura.

* **Esempio pratico: Smart Farm**
  In un'azienda agricola intelligente, vari sensori sul campo (umidità del terreno, temperatura, stazioni meteo) trasmettono i rilievi a basso consumo verso un gateway di fattoria tramite un protocollo d'accesso locale a corto/medio raggio (es. LoRaWAN o ZigBee). Il gateway raccoglie e pre-elabora i dati, per poi ==inviarli al server Cloud centrale sfruttando una rete di backhaul a lungo raggio== (es. connessione cellulare 4G/5G, link satellitare o WiMAX).

---

### liv.2.3 Network transport
Il sottolivello di **Network Transport** include i protocolli responsabili dell'==🟡instradamento e della consegna end-to-end dei pacchetti== di dati a destinazione, corrispondendo ai livelli di Rete (**Network**) e Trasporto (**Transport**) del modello [[Modello ISO OSI|ISO/OSI]].

Il protocollo di riferimento principale è l'**Internet Protocol (IP)**, in particolare nella versione **IPv6**, essenziale per garantire un indirizzamento univoco alla mole di dispositivi IoT. Per consentire l'uso di IPv6 su nodi e reti wireless fortemente vincolati e a basso consumo, si adotta lo standard **6LoWPAN** (IETF), che adatta e comprime le intestazioni IPv6.

---

### liv.2.4 IoT Network Mgmt
Il sottolivello di **IoT Network Management** opera a ==livello applicativo alto per gestire il flusso dei dati, il controllo dei dispositivi e l'interazione nella rete==.

I protocolli applicativi tradizionali del mondo IT (come HTTP) non sono adatti all'IoT, poiché richiedono troppa memoria, potenza di calcolo e banda, e tollerano male la frequente perdita di pacchetti delle reti vincolate. Per questo motivo si impiegano protocolli di gestione leggeri ed efficienti:
- **[[MQTT]] (Message Queuing Telemetry Transport):** basato su modello publish/subscribe, molto leggero e ottimizzato per connessioni instabili o a banda ridotta.
- **CoAP (Constrained Application Protocol):** progettato per dispositivi estremamente limitati, sfrutta UDP per ridurre l'overhead e riprendere il paradigma REST-like.
- **XMPP e altri protocolli dedicati:** adatti alla messaggistica e alla gestione remota avanzata dei nodi.

## Livello 3 - Application
Gestisce il controllo della rete e l'analisi dei dati attraverso applicazioni dedicate, come i sistemi SCADA industriali per l'azionamento degli attuatori. Integra moduli di analytics per monitorare sia le misurazioni del processo fisico sia lo stato di salute della rete.

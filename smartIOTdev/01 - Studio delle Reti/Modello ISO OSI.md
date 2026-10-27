---
cssclasses:
  - smart-iot
tags:
  - network-infrastructure
aliases:
  - ISO OSI
  - ISO/OSI
---


> [!summary] Abstract
> Il modello ISO/OSI (Open Systems Interconnection) è un'architettura logica di rete sviluppata per standardizzare la comunicazione tra sistemi informatici. Suddivide l'intero processo di comunicazione in **7 livelli** gerarchici e indipendenti.

## Architettura

```mermaid
flowchart LR
    subgraph Livelli_Host [Livelli Software]
        direction TB
        L7["<b>7. Applicazione</b><br><small>App / HTTP, MQTT</small>"] --- L6["<b>6. Presentazione</b><br><small>Cifratura / TLS</small>"] --- L5["<b>5. Sessione</b><br><small>Socket / Connessioni</small>"]
    end

    L4{"<b>4. Trasporto</b><br><small>End-to-End<br>TCP, UDP</small>"}

    subgraph Livelli_Media [Livelli Hardware / Rete]
        direction TB
        L3["<b>3. Rete</b><br><small>Routing / IP</small>"] --- L2["<b>2. Data Link</b><br><small>MAC / Switch</small>"] --- L1["<b>1. Fisico</b><br><small>Cavi, Radio, Segnali</small>"]
    end

    Livelli_Host --- L4 --- Livelli_Media
    
    classDef layer fill:#f8f9fa,stroke:#007acc,stroke-width:1px,color:#222;
    classDef transport fill:#e6f2ff,stroke:#005c99,stroke-width:2px,color:#222;
    class L7,L6,L5,L3,L2,L1 layer;
    class L4 transport;
```

Ogni livello comunica solo con quello immediatamente superiore o inferiore e "incapsula" i dati aggiungendo le proprie informazioni (header) prima di passare il pacchetto al livello successivo.
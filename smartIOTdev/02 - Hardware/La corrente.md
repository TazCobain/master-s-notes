---
cssclasses:
  - smart-iot
tags:
  - SMRT-IOT_teoria
aliases:
  - corrente
---
## Grandezze fondamentali
Logicamente si può vedere il funzionamento di un circuito come un quello delle tubature idraulica. Per evitare che i tubi esplodano e si allaghi casa bisogna tenere in considerazione pressione e portata dei tubi.
<p align="center">   <img src="VoltAmpOhm-chart.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 350px; max-width: 100%; height: auto;" /> </p>

### ==🟡Tensione== ($V$, Volt)
L'energia necessaria a muovere una carica (paragonata alla pressione dell'acqua spinta da una pompa).
### ==🟢Corrente== ($I$, Ampere, Amp, A)
Il flusso di cariche che attraversa un punto specifico nell'unità di tempo (la portata d'acqua).
### ==🔴Resistenza== ($R$, Ohm, $\Omega$)
L'opposizione al passaggio della corrente (la manopola/rubinetto che strozza il flusso).
### ==🟠WATT==
Sono l'==unità di misura della **potenza elettrica**== (e della potenza in generale nel Sistema Internazionale). Rappresentano la quantità di energia che un dispositivo consuma o produce in ogni singolo secondo (1 Watt = 1 Joule al secondo). Nell'analogia del tubo sarebbe lo *spruzzo finale*, ovvero il lavoro totale compiuto dall'acqua, che si calcola moltiplicando la pressione per la quantità ($Watt = V* I$).
<p align="center">   <img src="WattSpectrum.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 350px; max-width: 100%; height: auto;" /> </p>

## Modi di erogare la corrente
Ogni alimentatore ha un'etichetta che mostra tipo di corrente che è in grado di erogare (simboli $\sim$ per AC e $\approx$ linea continua per DC). Questo va tenuto in considerazione per evitare di bruciare i circuiti.

<p align="center">   <img src="CA-DC.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 350px; max-width: 100%; height: auto;" /> </p>

> [!tip] DC/AC
> DC come Dio Cane che è quello che dici quando prendi uno scottone sulla presa a muro. 
> AC come Avanti Cristo perché se la tocchi vai direttamente a rendere conto a lui.

### Corrente Continua (DC)
Corrente erogata secondo un flusso di cariche elettriche che si sposta sempre nella stessa direzione all'interno di un conduttore, mantenendo una polarità fissa nel tempo.
#### Principali utilizzi
- **==Dispositivi elettronici==:** Smartphone, computer, tablet e la maggior parte dei circuiti integrati funzionano a bassa tensione continua.
- **Sistemi di accumulo:** Batterie d'auto, veicoli elettrici e sistemi di accumulo per l'energia domestica.
- **Trasporto e infrastrutture:** Treni elettrici, tram e linee di trasmissione ad alta tensione in corrente continua (**HVDC**) ideali per trasportare energia sulle lunghe distanze con minori dispersioni.

###  Alternata (AC)
Un tipo di corrente elettrica in cui il **flusso delle cariche inverte periodicamente la propria direzione e la propria intensità nel tempo**, solitamente seguendo un andamento a onda sinusoidale.
#### caratteristiche
- **Frequenza:** in Europa la rete elettrica funziona a una frequenza fissa di **50 Hz**, il che significa che la corrente inverte la sua direzione 100 volte al secondo (50 cicli completi). Negli Stati Uniti (quindi il terzo mondo) la frequenza è di 60 Hz. 
- **Forma d'onda:** Il valore della tensione e dell'intensità oscilla in modo continuo tra valori positivi e negativi.
- **Generazione:** È prodotta tramite *alternatori nelle centrali elettriche* (idroelettriche, eoliche, termoelettriche) sfruttando l'induzione elettromagnetica.
#### perché si usa nella rete elettrica
- **Trasformabilità:** Grazie ai trasformatori, la tensione della corrente alternata può essere facilmente aumentata o ridotta.
- **==Trasporto efficiente==:** Elevando la tensione durante il trasporto sulle lunghe distanze si riducono drasticamente le dispersioni di energia e i costi di rete.

## Leggi fisiche
### Kirchhoff
Le **Leggi di Kirchhoff** sono due principi fondamentali dell'elettrotecnica basati sulla ==conservazione della carica e dell'energia==, utilizzati per calcolare correnti e tensioni nei circuiti complessi.
#### 1. Legge dei Nodi (LKC)
La somma delle correnti che entrano in un nodo (punto di incrocio) è uguale alla somma delle correnti che ne escono: la carica elettrica non può accumularsi né sparire.
- **Formula:** $\sum I_{\text{entranti}} = \sum I_{\text{uscenti}}$
#### 2. Legge delle Maglie (LKV)
La somma algebrica di tutte le tensioni (generatori e cadute di potenziale) lungo un percorso chiuso (maglia) è sempre uguale a zero: l'energia fornita viene interamente consumata.
- **Formula:** $\sum V = 0$
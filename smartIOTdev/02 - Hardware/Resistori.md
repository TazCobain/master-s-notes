---
aliases:
  - resistenza
  - resistenze
  - resistore
cssclasses:
  - smart-iot
tags:
  - SMRT-IOT_teoria
  - hardware
---
Nel gioco della  [[La corrente|corrente]] è l'omino rosso con il lazo ma in soldoni è un  componente elettrico passivo a due terminali che *si oppone al flusso della corrente elettrica*. 

> [!note] Legge di Ohm
> Il comportamento di un resistore ideale è descritto dalla formula $V = R*I$, dove  $V$ è la tensione in volt, $R$ è la resistenza misurata in ohm ($\Omega$) e $I$ è la corrente in ampere.
> <p align="center">   <img src="OhmLawSpectrum.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" /> </p>
> 
>> [!tip] Dissipazione di energia
> >  Quando la corrente lo attraversa, parte dell'energia elettrica viene convertita in calore per effetto Joule.

## Come leggere una resistenza

### 1. Orientare la Resistenza
- **Trova la banda di tolleranza**: di solito è di colore **oro** o **argento** (oppure marrone/rosso nelle resistenze di precisione) ed è *leggermente più distanziata* dalle altre.
- **Posiziona questa banda a destra**.
- **Leggi le bande da sinistra verso destra**.

### 2. Codice colore
<p align="center">   <img src="ReadResistor.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" /> </p>
Le resistenze elettriche si leggono principalmente a 4 o 5 bande di colore: nelle resistenze a 4 bande, le prime due indicano le cifre numeriche iniziali, la terza rappresenta il moltiplicatore (ovvero il *coefficiente per cui moltiplicare le cifre precedenti*, traducendosi in pratica nel numero di zeri da aggiungere), mentre l'ultima indica la tolleranza, cioè la *percentuale di errore massimo ammessa* rispetto al valore nominale. 

Il funzionamento rimane identico per le resistenze a 5 bande, con l'unica differenza che lo spazio dedicato alle cifre iniziali si estende alle prime tre bande, spostando di conseguenza il moltiplicatore sulla quarta banda e la tolleranza sulla quinta.

#### esempio
Se prendo la resistenza a 4 bande nell'immagine sopra avrò una resistenza di: $$22*10K \pm 5\% \rightarrow 220000 \Omega \pm 5\% \rightarrow 220 K\Omega \pm 5\%  $$

> [!WARNING] La sesta banda nei resistori borghesotti a 6 bande  
> La sesta banda indica il **coefficiente di temperatura**, espresso in ppm/K (parti per milione per kelvin). Serve a specificare quanto varia il valore della resistenza in Ohm al variare della temperatura operativa del circuito.
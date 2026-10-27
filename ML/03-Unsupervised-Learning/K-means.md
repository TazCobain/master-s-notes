---
tags:
  - clustering
  - classification
  - unsupervised
cssclasses:
  - machine-learning
---
Il **K-Means** è un algoritmo di _unsupervised learning_ (apprendimento non supervisionato) il cui scopo è partizionare un insieme di dati in **K** gruppi (cluster) omogenei all'interno di uno spazio vettoriale. L'obiettivo matematico è raggruppare gli elementi in modo da ==rendere massima la somiglianza all'interno dello stesso cluster e massima la differenza tra cluster diversi.==

<p align="center">
  <img src="clustering_example_K-mean.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</p>


##  funzionamento algoritmo
L'algoritmo procede per step successivi, partendo da un'ipotesi casuale e affinandola iterativamente.
### 1. Inizializzazione (Scelta di K)
L'utente deve definire a priori il parametro **K**, ovvero il numero esatto di cluster desiderati. ==L'algoritmo seleziona quindi in modo casuale **K punti** nel _feature space_==. Questi punti iniziali sono chiamati **centroidi** e rappresentano i centri provvisori dei futuri gruppi.

### 2. Fase Iterativa
Questa fase si ripete in un ciclo continuo composto da due passaggi chiave:

- **Step di Assegnazione:** Per ogni punto del dataset viene ==calcolata la distanza rispetto a tutti i K centroidi==. Il punto viene assegnato al cluster del centroide a lui più vicino.
    
- **Step di Aggiornamento:** Una volta che tutti i punti sono stati riassegnati, l'algoritmo ricalcola la posizione dei centroidi. ==Il nuovo centroide viene spostato nel **baricentro**== (la media delle coordinate) di tutti i punti che formano quel cluster.
### 3. Conclusione (Convergenza)
Il ciclo iterativo si interrompe (raggiunge la convergenza) quando si verifica una delle seguenti condizioni:
- **Stabilità dei centroidi:** I centroidi smettono di spostarsi (o lo spostamento è infinitesimale).    
- **Stabilità delle assegnazioni:** Nessun punto cambia cluster rispetto all'iterazione precedente.    
- **Limite massimo:** Viene raggiunto il numero massimo di iterazioni consentite (impostato preventivamente per evitare loop).

<p align="center">
  <img src="k-mean_flow.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</p>

> [!info] A cosa serve l'entropia? 
> L'entropia è una misura che valuta il livello di disordine o "impurità" di un gruppo di dati. L'albero di decisione la ricalcola ad ogni tentativo di taglio per misurare matematicamente quale opzione separa meglio le diverse classi. In questo modo, l'algoritmo riesce a scegliere sempre la divisione che crea i sotto-gruppi più omogenei e puri possibili.


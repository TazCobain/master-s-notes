---
cssclasses:
  - machine-learning
tags:
  - supervised
  - classification
aliases:
  - decision tree
  - DT
---
> [!abstract] In sinstesi
I Decision Tree sono modelli di apprendimento per l'inferenza induttiva che
==risolvono problemi di classificazione sfruttando una gerarchia di regole== logiche "se-allora". La loro costruzione avviene in modalità top-down (es. tramite l'algoritmo ID3), selezionando iterativamente gli attributi che separano meglio i dati attraverso la minimizzazione dell'[[Entropia]] e la massimizzazione dell'Information Gain. <p align="center">   <img src="decisionTree.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>


## Introduzione e Rappresentazione
- **Inferenza induttiva:** I Decision Tree rappresentano uno degli algoritmi più usati e pratici per l'inferenza induttiva.
- **Approssimazione discreta:** La funzione obiettivo viene appresa e approssimata con valori discreti tramite la struttura dell'albero.
- **Regole Se-Allora:** Gli alberi di decisione possono essere riscritti in modo equivalente come una serie di regole «if-then».

## Classi di Problemi adatte
Gli alberi di decisione si adattano particolarmente bene a problemi con le seguenti caratteristiche:
- **Coppie attributo-valore:** Le istanze sono rappresentate da coppie attributo-valore (es. attributo humidity con valori low, normal, high), specialmente con pochi valori disgiunti.
- **Valori di output discreti:** La funzione obiettivo presenta un numero limitato di categorie di classificazione (es. true/false, yes/no, low/medium/high).
- **Descrizioni disgiunte:** Il problema richiede l'uso di descrizioni disgiunte.
- **Rumore nei dati:** Sono algoritmi robusti in presenza di errori o rumore nelle coppie attributo-valore, oppure quando l'addestramento non raggiunge la convergenza.
- **Dati mancanti:** Possono gestire campioni in cui mancano i valori di alcuni attributi.

## Struttura dell'algoritmo e Algoritmo ID3
L'algoritmo di base esegue una ==ricerca top-down nello spazio di tutti i possibili alberi di decisione==, valutando localmente mediante un test statistico quale attributo classifica meglio il training set per posizionarlo al nodo radice.
"*Tra tutti i nodi quello che sceglierò sarà quello con il miglior attributo come root.*"

[^1]**Algoritmo ID3:** `ID3(TS, attributes, target)`
1. Crea il nodo radice dell'albero.
2. Caso base 1: Se tutti i campioni sono positivi, restituisce l'albero con un singolo nodo etichettato `+`.
3. Caso base 2: Se tutti i campioni sono negativi, restituisce l'albero con un singolo nodo etichettato `-`.
4. Passo ricorsivo:
  - Seleziona l'attributo $A$ che classifica meglio i campioni e impostalo come nodo radice.
  - Per ogni possibile valore $v_i$ dell'attributo $A$:
    - Aggiungi un nuovo ramo figlio collegato a $A$ per il test $A = v_i$.
    - Sia $TS_{v_i}$ il sottoinsieme del Training Set i cui campioni hanno il valore $v_i$ per l'attributo $A$.
    - Se $TS_{v_i}$ è vuoto ($\emptyset$), assegna un nodo foglia con l'etichetta del valore target più comune.
    - Altrimenti, collega un nuovo sotto-albero chiamando ricorsivamente `ID3`($TS_{v_i}$, attributes - {$A$}, target).


### **Information Gain** ($Gain$)
Misura la riduzione attesa dell'entropia ottenuta partizionando i campioni del Training Set corrente tramite l'attributo $A$:
- Formula:
$$Gain(TS, A) = E(TS) - \sum_{v_i \in A} \frac{\vert{}TS_{v_i}\vert{}}{\vert{}TS\vert{}} E(TS_{v_i})$$
- Rappresenta l'informazione acquisita sulla funzione obiettivo quando si conosce il valore dell'attributo $A$


> [!NOTE] Gerarchia e Ponderazione degli Attributi 
> Nelle classificazioni con molti attributi, può essere utile stabilire un **ordine di priorità o peso**. Ad esempio, per valutare la commestibilità di un frutto, la presenza di *muffa* ha un impatto decisamente maggiore rispetto a una semplice *ammaccatura*. 
>  > A livello concettuale: 
>  > - **Combinazione lineare (Pesi pesati):** È possibile assegnare a ciascun attributo $i$ un peso normalizzato $w_i \in [0, 1]$ tale che: > $$\sum_{i} w_i = 1$$ 
>  > - **Negli Alberi di Decisione:** Algoritmi come ID3 o C4.5 ricavano questa gerarchia in modo automatico. Gli attributi più discriminanti (con *Information Gain* più elevato) vengono selezionati per primi e posizionati più vicini alla radice, definendo implicitamente l'ordine di importanza senza bisogno di pesi manuali.

> [!warning] Convergenza e Ricerca Greedy
> L'algoritmo ID3 non calcola tutti gli alberi possibili (non effettua una ricerca *brute force*), ma valuta di volta in volta l'attributo locale più adatto tramite l'Information Gain. Una volta scelto, l'attributo viene escluso dal pool di attributi disponibili per quel ramo. Questo approccio *greedy* (senza *backtracking*) fa sì che l'algoritmo possa convergere a un **minimo locale**, che non corrisponde necessariamente al **minimo globale** (l'albero ottimale).

---

## algoritmo: Random forest

[^1]:Documentazione: https://en.wikipedia.org/wiki/ID3_algorithm

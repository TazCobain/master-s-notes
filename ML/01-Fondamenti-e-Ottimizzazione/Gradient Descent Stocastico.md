---
cssclasses:
  - machine-learning
tags:
  - ML-teoria
  - ML-optimization
---

> [!abstract] GD stocastico in breve
> L'SGD è un algoritmo di ottimizzazione iterativo utilizzato per aggiornare i pesi dei modelli di Machine Learning, come il percettore e le reti neurali.
> A differenza del [[Gradient Descent]] (GD) standard (o _batch_), che accumula le variazioni dei pesi sommando l'errore su **tutti i campioni del Training Set** ($TS$) prima di eseguire un singolo aggiornamento dei parametri, l'**SGD** aggiorna i pesi **immediatamente dopo aver processato ciascun singolo campione** $<x_d, t_d>$.

## 1. Principi Fondamentali dell'Algoritmo
* **Aggiornamento Incrementale**: A differenza del [[Gradient Descent]] (GD) standard che accumula l'errore su tutto il training set prima di aggiornare i pesi, lo Stochastic Gradient Descent (SGD) aggiorna i parametri del modello immediatamente dopo aver processato ciascun singolo campione $<x_d, t_d> \in TS$.
* **Minimizzazione dell'Errore locale**: L'algoritmo calcola la ==derivata parziale dell'errore $E_d$ del singolo campione rispetto a ciascun peso della rete== per determinare la direzione di aggiornamento.
## 2. Funzionamento dell'Algoritmo SGD nel Percettore
### Procedura Passo-Passo
1. **Inizializzazione**: Ogni peso $w_i$ viene inizializzato con un valore casuale piccolo compreso nell'intervallo $[-0.5, 0.5]$.
2. **Ciclo di Apprendimento**: Finché la condizione di arresto non viene soddisfatta:
   * Si azzera il valore di $\Delta w_i$.
   * Per ciascun campione $<x_d, t_d> \in TS$:
     1. Si invia l'input $x_d$ al percettore e si calcola l'output $o_d$.
     2. Per ogni peso $w_i$, si esegue l'aggiornamento immediato: $$w_i = w_i + \eta (t_d - o_d) x_{id}$$dove $\eta$ rappresenta il *learning rate*, $t_d$ è l'output desiderato per il dato $d$ e $x_{id}$ è la componente $i$-esima dell'input.
## 3. Funzionamento dell'Algoritmo SGD nelle Reti Neurali ([[Backpropagation]])
Nelle reti neurali multi-strato, l'algoritmo SGD si integra con la **Backpropagation** per aggiornare i pesi $w_{ji}$ tra il nodo $i$ ed il nodo $j$.
### Procedura Passo-Passo
1. **Inizializzazione**: I pesi della rete vengono inizializzati con piccoli valori casuali.
2. **Ciclo sui Campioni**: Finché la condizione di arresto non è soddisfatta, per ogni dato $<x_d, t_d> \in TS$:
   * **Propagazione in avanti (*Forward propagation*)**: Si fornisce l'input $x_d$ alla rete e si calcolano le uscite $o_d$.
-  **Propagazione all'indietro dell'errore (*Backward propagation*)**:
	 * Per ogni unità di output $k$, si calcola il termine di errore $\delta_k$: $$\delta_k = o_k (1 - o_k) (t_k - o_k)$$
	     * Per ogni unità nascosta $l$, si calcola il termine di errore $\delta_l$ propagando gli errori dai nodi del livello successivo $k \in nextl(l)$: $$\delta_l = o_l (1 - o_l) \sum_{k \in nextl(l)} w_{kl} \delta_k$$
   * **Aggiornamento dei Pesi**: Ciascun peso $w_{ji}$ della rete viene aggiornato incrementalmente tramite la regola: $$\Delta w_{ji} = \eta \delta_j x_{ji}$$ $$w_{ji} = w_{ji} + \Delta w_{ji}$$

### Variante con Momento (*Momentum*)
Per stabilizzare l'aggiornamento dei pesi durante la discesa del gradiente, è possibile aggiungere un termine di momento $\alpha$ basato sull'aggiornamento precedente:
$$\Delta w_{ji}(n) = \eta \delta_j x_{ji} + \alpha \Delta w_{ji}(n-1)$$
## Utilizzo
Nelle [[Reti Neurali]] multi-strato (_Multi-layer Perceptron_), la regola dell'SGD viene integrata con l'algoritmo di [[Backpropagation]]. L'errore $\delta$ calcolato per ciascun nodo (sia di output che nascosto) per il singolo campione $d$ viene propagato all'indietro per determinare l'aggiornamento dei pesi $\Delta w_{ji} = \eta \delta_j x_{ji}$.
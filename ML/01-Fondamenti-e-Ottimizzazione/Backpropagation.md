---
cssclasses:
  - machine-learning
tags:
  - ML-teoria
  - ML-optimization
---
> [!abstract] In breve la backpropagerion
> La **backpropagation** è il meccanismo che permette a una rete neurale di imparare confrontando la propria risposta con il risultato desiderato e propagando all'indietro l'errore calcolato, dall'uscita fino agli strati interni. Grazie a questo passaggio a ritroso, la rete quantifica lo sbaglio commesso da ciascuna connessione e ne modifica progressivamente i pesi per commettere sempre meno errori nelle prove successive.
## Scopo e Notazione
* **Scopo**: L'algoritmo di Backpropagation calcola il gradiente della funzione di errore rispetto a tutti i pesi della rete neurale, consentendone l'aggiornamento iterativo tramite [[Gradient Descent Stocastico]] (SGD).
* **Notazione adottata**:
  * $x_{ji}$: $i$-esimo ingresso al nodo $j$.
  * $w_{ji}$: peso della connessione dal nodo $i$ al nodo $j$.
  * $net_j = \sum_i w_{ji} x_{ji} = \mathbf{w}_j \cdot \mathbf{x}_j$: combinazione lineare ponderata degli ingressi al nodo $j$.
  * $o_j = \sigma(net_j)$: valore di uscita calcolato dal nodo $j$ applicando la funzione di attivazione sigmoide.
  * $t_j$: target (uscita desiderata) per il nodo $j$.
  * $outs$: insieme dei nodi appartenenti allo strato di uscita della rete.
  * $nextl(j)$: insieme dei nodi dello strato successivo che prendono in input l'uscita del nodo $j$.
* **Funzione di Errore sul Singolo Campione**: Per ciascun dato di addestramento $d$, l'errore quadratico complessivo è definito come:
  $$E_d(\mathbf{w}) = \frac{1}{2} \sum_{k \in outs} (t_k - o_k)^2$$

---

## 2. Derivazione Matematica tramite Regola della Catena (*Chain Rule*)
Per aggiornare ciascun parametro secondo la regola del gradiente stocastico $\Delta w_{ji} = -\eta \frac{\partial E_d}{\partial w_{ji}}$, si scompone la derivata dell'errore sfruttando il fatto che il peso $w_{ji}$ influenza l'intera rete unicamente attraverso la combinazione lineare $net_j$:
$$\frac{\partial E_d}{\partial w_{ji}} = \frac{\partial E_d}{\partial net_j} \frac{\partial net_j}{\partial w_{ji}}$$

Dato che $\frac{\partial net_j}{\partial w_{ji}} = \frac{\partial}{\partial w_{ji}} \left(\sum_p w_{jp} x_{jp}\right) = x_{ji}$, il calcolo si riduce a valutare la sensibilità rispetto a $net_j$:
$$\frac{\partial E_d}{\partial w_{ji}} = \frac{\partial E_d}{\partial net_j} x_{ji}$$

Definendo per convenzione il termine di errore locale del nodo come $\delta_j = -\frac{\partial E_d}{\partial net_j}$, la regola generale di variazione del peso diviene:
$$\Delta w_{ji} = \eta \delta_j x_{ji}$$

---

## 3. Calcolo dell'Errore $\delta$ per i Singoli Strati

### A. Nodi dello Strato di Uscita ($j \in outs$)
La grandezza $net_j$ influenza l'errore $E_d$ unicamente tramite l'uscita $o_j$ del nodo stesso:
$$\frac{\partial E_d}{\partial net_j} = \frac{\partial E_d}{\partial o_j} \frac{\partial o_j}{\partial net_j}$$

1. Derivata dell'errore rispetto all'uscita:
   $$\frac{\partial E_d}{\partial o_j} = \frac{\partial}{\partial o_j} \left( \frac{1}{2} \sum_{k \in outs} (t_k - o_k)^2 \right) = -(t_j - o_j)$$
2. Derivata della funzione sigmoide $\sigma(net_j)$ rispetto al proprio argomento:
   $$\frac{\partial o_j}{\partial net_j} = o_j (1 - o_j)$$
3. Termine di errore $\delta_k$ per il nodo di output $k$:
   $$\delta_k = -\frac{\partial E_d}{\partial net_k} = o_k (1 - o_k) (t_k - o_k)$$

### B. Nodi degli Strati Nascosti (*Hidden Layers*, $j \in hidden$)
Il valore $net_j$ di un'unità nascosta influenza l'errore $E_d$ solo attraverso tutti i nodi del livello successivo ad essa collegati ($k \in nextl(j)$):
$$\frac{\partial E_d}{\partial net_j} = \sum_{k \in nextl(j)} \frac{\partial E_d}{\partial net_k} \frac{\partial net_k}{\partial net_j} = \sum_{k \in nextl(j)} (-\delta_k) \frac{\partial net_k}{\partial o_j} \frac{\partial o_j}{\partial net_j}$$

Essendo $\frac{\partial net_k}{\partial o_j} = w_{kj}$ e $\frac{\partial o_j}{\partial net_j} = o_j (1 - o_j)$, il termine di errore retropropagato $\delta_l$ per l'unità nascosta $l$ risulta:
$$\delta_l = -\frac{\partial E_d}{\partial net_l} = o_l (1 - o_l) \sum_{k \in nextl(l)} w_{kl} \delta_k$$

---

## 4. Algoritmo di Backpropagation Passo-Passo

1. **Inizializzazione**: Assegnare a ciascun peso della rete un valore casuale piccolo.
2. **Ciclo di Apprendimento**: Fino al raggiungimento del criterio di arresto, per ciascun campione $\langle \mathbf{x}_d, \mathbf{t}_d \rangle \in TS$:
   * **Propagazione in avanti (*Forward propagation*)**: Fornire l'input $\mathbf{x}_d$ alla rete e propagare i segnali fino a calcolare le uscite $o_d$.
   * **Propagazione all'indietro dell'errore (*Backward propagation*)**:
     * Per ogni unità di output $k$, calcolare il termine di errore:
       $$\delta_k = o_k (1 - o_k) (t_k - o_k)$$
     * Per ogni unità nascosta $l$, calcolare l'errore combinando i contributi dei nodi successivi:
       $$\delta_l = o_l (1 - o_l) \sum_{k \in nextl(l)} w_{kl} \delta_k$$
   * **Aggiornamento dei pesi**:
     * Calcolare la correzione di ciascun peso:
       $$\Delta w_{ji} = \eta \delta_j x_{ji}$$
     * Aggiornare il valore del peso:
       $$w_{ji} = w_{ji} + \Delta w_{ji}$$

### Variante con Momento (*Momentum*)
Per regolarizzare il percorso di discesa e velocizzare la convergenza nei tratti a gradiente piatto, si può introdurre un coefficiente di momento $\alpha \in$ sull'aggiornamento precedente:
$$\Delta w_{ji}(n) = \eta \delta_j x_{ji} + \alpha \Delta w_{ji}(n-1)$$

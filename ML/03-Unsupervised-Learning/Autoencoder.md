

> [!abstract] Autoencoder in breve
> Si tratta di una rete neurale **non supervisionata** che impara a riprodurre i propri dati di input attraverso una fase di compressione (**encoder**, $h = f(x)$) e una successiva fase di ricostruzione (**decoder**, $r = g(h)$). 
> Per evitare che il modello impari una banale funzione identità, vengono introdotti vincoli architettonici come il "collo di bottiglia" (_undercomplete_, dove la dimensione del codice è inferiore all'input) o modifiche alla funzione di costo (_Regularized_ e _Denoising Autoencoders_), costringendo la rete ad apprendere la struttura geometrica sottostante (_manifold_) e i tratti salienti dei dati per compiti quali la riduzione di dimensionalità, l'estrazione di feature e l'information retrieval
> <p align="center">   <img src="autoencoder.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>

## 1. Cos'è un Autoencoder?
Un **autoencoder** è una rete neurale che viene addestrata per riprodurre in uscita lo stesso dato che riceve in ingresso. 

* **Nessun bisogno di etichette**: Si tratta di un modello non supervisionato poiché l'output desiderato non è una classe esterna, ma coincide con l'input stesso.
* **Oltre la semplice "copia"**: Se si limitasse a copiare il dato da input a output imparerebbe una banale funzione identità. Per renderlo utile, si applicano dei vincoli alla struttura della rete affinché sia costretta a estrarre solo le caratteristiche fondamentali ed eliminare il superfluo.

---

## 2. Come Funziona l'Architettura?
La rete è composta da due blocchi principali collegati in sequenza:

1. **Encoder ($f$)**: 
   * Prende l'input originale $x \in \mathbb{R}^D$ e lo comprime.
   * Produce una rappresentazione interna ridotta $h$, detta **codice** o spazio latente:
     $$h = f(x)$$
2. **Decoder ($g$)**:
   * Prende il codice compresso $h$ e cerca di ricostruire il dato di partenza.
   * Genera in uscita la ricostruzione $r = \hat{x} \in \mathbb{R}^D$:
     $$r = g(h) = g(f(x))$$

### Il "Collo di Bottiglia" (*Undercomplete Autoencoder*)
Nella configurazione più comune, la dimensione del codice intermedio $K$ è volutamente minore della dimensione iniziale $D$ ($K < D$). Questo restringimento costringe la rete a scartare le informazioni marginali e a conservare solo i tratti salienti dei dati.

> [!note] Collegamento con la PCA
> Un autoencoder semplice con un solo strato nascosto, funzioni di attivazione lineari ed errore quadratico medio (MSE) si comporta in modo analogo alla [[Principal Component Analysis (PCA)|PCA]], proiettando i dati sulle prime $K$ componenti principali.

---

## 3. Come Impara la Rete?
* **Addestramento**: Viene addestrata tramite **Backpropagation** e discesa del gradiente a mini-batch.
* **Funzione di Costo (Loss)**: Misura quanto la ricostruzione in uscita differisce dal dato originale e guida l'aggiornamento dei parametri $\theta$:
  $$\sum_{i=1}^{N} \mathcal{L}(g_\theta(f_\theta(x_i)), x_i) \to \min_\theta$$

---

## 4. Varianti Principali
* **Regularized Autoencoders (RAE)**: Aggiungono una penalità matematica alla funzione di perdita (ad esempio per incentivare la *sparsità* del codice), spingendo la rete a scoprire proprietà utili oltre alla semplice compressione.
* **Denoising Autoencoders**: Ricevono in input un dato "sporcato" da rumore artificiale ($\tilde{x}$) e vengono istruiti a ricostruire il dato pulito originale ($x$). In questo modo la rete impara a rimuovere le perturbazioni e comprende la struttura geometrica profonda (*manifold*) dei dati.

---

## 5. A Cosa Servono?
* **Riduzione della dimensionalità** e compressione dei dati.
* **Visualizzazione** di dati complessi in poche dimensioni.
* **Estrazione di feature** per migliorare l'accuratezza e la velocità di altri modelli predittivi.
* **Semantic hashing** e recupero rapido delle informazioni (*information retrieval*).
* **Pre-addestramento non supervisionato** (*unsupervised pretraining*) di reti profonde.

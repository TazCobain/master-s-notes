---
cssclasses:
  - machine-learning
tags:
  - supervised
  - regression
  - optimization
---
> [!abstract] In sintesi
> Il metodo dei **Minimi Quadrati** è il criterio di ottimizzazione alla base della **Regressione Lineare**. Consiste nel determinare i pesi $\theta$ che minimizzano la discrepanza complessiva tra predizioni e valori reali, calcolata come somma degli errori al quadrato (MSE). L'ottimo si trova calcolando dove il gradiente della funzione di costo è zero, risolvibile in modo esatto tramite **Equazione Normale** (per dataset ridotti) o in modo iterativo tramite **Discesa del Gradiente** (per grandi volumi di dati o molte feature).
# Il Problema dei Minimi Quadrati (Least Squares)

Il metodo dei minimi quadrati è l'approccio matematico fondamentale per risolvere i problemi di **regressione lineare**. L'obiettivo è trovare l'iperpiano (o la retta, in due dimensioni) che si adatta meglio ai dati di addestramento, riducendo al minimo la distanza tra i valori previsti dal modello e i valori reali. 

---
## 1. Il Setup del Problema (Notazione) 
In un problema di apprendimento supervisionato, abbiamo a disposizione: 
- **$X$**: La matrice delle feature (o variabili indipendenti) di dimensione $N \times (D+1)$, dove $N$ è il numero di campioni e $D$ il numero di feature. Si aggiunge una colonna di $1$ per gestire l'intercetta (bias). 
- **$y$**: Il vettore dei valori target (o variabili dipendenti) reali di dimensione $N \times 1$. 
- **$\theta$**: Il vettore dei parametri (o pesi) del modello di dimensione $(D+1) \times 1$. L'ipotesi del nostro modello lineare è che la predizione $\hat{y}$ si calcoli come combinazione lineare delle feature: $$ \hat{y} = X\theta $$
---
## 2. La Funzione di Costo (Loss Function)
Per valutare quanto il nostro modello si stia sbagliando, definiamo una **funzione di costo** (o loss function). Per i minimi quadrati, utilizziamo la somma degli errori al quadrato (o il Mean Squared Error, MSE): $$ J(\theta) = \frac{1}{2N} \sum_{i=1}^{N} (\hat{y}_i - y_i)^2 $$ In **forma matriciale**, questa espressione diventa molto più pulita: $$ J(\theta) = \frac{1}{2N} (X\theta - y)^T (X\theta - y) $$ 
> **Perché si eleva al quadrato l'errore?** 
> 1. **Assenza di cancellazioni:** Essendo tutti valori positivi, un errore di $+2$ e uno di $-2$ non si annullano a vicenda (cosa che accadrebbe se usassimo solo $(\hat{y} - y)$). 
> 2. **Penalizzazione degli outlier:** Gli errori grandi vengono amplificati (un errore di $4$ pesa $16$), costringendo il modello a non ignorare i dati distanti.
> 3. **Proprietà matematiche:** È una funzione **convessa**, il che garantisce l'esistenza di un unico minimo globale. Inoltre, è facilmente differenziabile. 

---
## 3. Come trovare il minimo (I due approcci) 
Per trovare il vettore dei pesi ottimali $\theta$ che minimizza la funzione di costo $J(\theta)$, possiamo usare due strade: una soluzione esatta (analitica) o una approssimata iterativa. 
### A. L'Equazione Normale (Soluzione Analitica) 
Poiché la funzione $J(\theta)$ è convessa, possiamo trovare il suo minimo calcolando la derivata (o gradiente) rispetto a $\theta$ e ponendola uguale a zero. 1. Calcoliamo il gradiente di $J(\theta)$: $$ \nabla_\theta J(\theta) = \frac{1}{N} X^T (X\theta - y) $$ 2. Poniamo il gradiente a zero per trovare il punto di minimo: $$ X^T X \theta - X^T y = 0 $$ 3. Isoliamo $\theta$ (questa è la cosiddetta **Equazione Normale**): $$ \theta = (X^T X)^{-1} X^T y $$
- **Vantaggio:** Trova il risultato esatto in un solo passaggio. Non serve impostare un learning rate.
- **Svantaggio:** Calcolare la matrice inversa di $(X^T X)$ ha una complessità computazionale di circa $O(D^3)$. Se il numero di feature $D$ è nell'ordine delle decine di migliaia, il calcolo diventa insostenibile. 

### B. Discesa del Gradiente (Soluzione Iterativa) 
Quando il dataset ha moltissime feature o l'Equazione Normale è troppo lenta, si utilizza il [[Gradient Descent]]. Inizializziamo $\theta$ con valori casuali e aggiorniamo iterativamente i pesi muovendoci nella ==direzione opposta al gradiente== sostituendo il gradiente precedentemente calcolato: $$ \theta_{nuovo} = \theta_{vecchio} - \alpha \left( \frac{1}{N} X^T (X\theta_{vecchio} - y) \right) $$
- **Vantaggio:** Scala benissimo con dataset enormi e tantissime feature.
- **Svantaggio:** Richiede il tuning di iperparametri (come $\alpha$ e il numero di epoche) e richiede lo scaling delle feature (standardizzazione) per convergere velocemente. 

---

## Collegamenti (Backlinks) 
* [[Regressione lineare]] 
* [[Gradient Descent|Discesa del Gradiente (Gradient Descent)]]
* [[Metriche di Valutazione: MSE, RMSE, R-quadro]]
* [[Overfitting e Regolarizzazione (Ridge e Lasso)]]
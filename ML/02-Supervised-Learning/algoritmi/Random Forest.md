---
tags:
  - classification
cssclasses:
  - machine-learning
---
> [!abstract] Abstract: Random Forest in Breve
> Un algoritmo di apprendimento supervisionato che combina molteplici [[Decision Tree Learning|decision tree]] per ridurre la varianza e prevenire l'overfitting tipico dei singoli modelli. Il suo funzionamento si basa su una doppia componente di casualità: il **Bagging** (addestramento su campioni estratti con reinserimento) e il **Feature Bagging** (selezione di un sottoinsieme casuale di feature a ogni split, solitamente $m \approx \sqrt{p}$ per classificazione), utile a decorrelare gli alberi. 
> Le predizioni finali derivano dal *voto di maggioranza* (classificazione) o dalla *media* (regressione). 
> Include meccanismi nativi per la validazione interna tramite **OOB Error** (Out-of-Bag) e per il calcolo della **Feature Importance**, sacrificando l'immediata interpretabilità visiva del singolo albero a favore di una maggiore accuratezza e robustezza al rumore.


L'algoritmo **Random Forest** è un metodo di apprendimento supervisionato basato sull'approccio di **ensemble learning** (apprendimento d'insieme). Si fonda sull'idea che combinare le previsioni di molteplici modelli deboli (*weak learners*) — in questo caso singoli [[Decision Tree Learning|decision tree]] — produca un modello robusto, accurato e meno incline all'overfitting.

> [!tip] Principio Base: "La saggezza della folla"
> Un singolo albero di decisione tende ad avere un'alta varianza (*high variance*) e a memorizzare il rumore del dataset. Una foresta mitiga questo problema aggregando centinaia o migliaia di alberi indipendenti e facendo mediare le loro risposte.

---

## 1. Come Funziona l'Ensemble: Bagging e Random Subspace

Il cuore di Random Forest poggia su due livelli di casualità (da cui il nome *Random*):

### A. Bootstrap Aggregating (Bagging)
Per addestrare $B$ alberi diversi a partire dallo stesso dataset di dimensione $N$:
1. **Campionamento con reinserimento (Bootstrap):** Ogni albero viene allenato su un sottoinsieme casuale di righe (campioni) estratto con rimpiazzo dal dataset originale. Circa il $63.2\%$ delle istanze uniche finisce nel set di training, mentre le rimanenti costituiscono i dati **Out-of-Bag (OOB)**.
2. **Aggregazione:**
   - **Classificazione:** Si applica il principio del voto di maggioranza (*majority voting*).
   - **Regressione:** Si calcola la media aritmetica delle previsioni dei singoli alberi.

### B. Feature Bagging (Random Subspace Method)
A differenza di un albero di decisione standard (che ad ogni split valuta *tutte* le $p$ feature disponibili per trovare quella ottimale tramite [[Information Gain]] o Indice di Gini):
- In Random Forest, ad ogni nodo viene selezionato un **sottoinsieme casuale di feature** di dimensione $m < p$.
- *Regola euristica tipica:*
  - Per **classificazione:** $m \approx \sqrt{p}$
  - Per **regressione:** $m \approx \frac{p}{3}$

> [!important] Perché forzare la selezione casuale delle feature?
> Se nel dataset esiste una feature dominante, tutti gli alberi guidati da Bagging semplice sceglierebbero quella feature come radice, rendendo gli alberi fortemente **correlati**. Limitare la scelta delle feature forza gli alberi a esplorare percorsi alternativi, **decorrelandoli** e abbattendo drasticamente la varianza totale.

---

## 2. Valutazione Out-of-Bag (OOB Error)

Poiché ogni albero non vede circa un terzo dei campioni durante l'addestramento, questi campioni esclusi (**OOB**) fungono da test set naturale:
- Ogni istanza viene predetta esclusivamente dagli alberi che *non* l'hanno usata nel loro training.
- L'**OOB Error** fornisce una stima non distorta delle prestazioni del modello senza richiedere un set di validazione separato o una validazione incrociata (*cross-validation* computazionalmente costosa).

---

## 3. Punti di Forza e Limiti

| Vantaggi | Limiti |
| :--- | :--- |
| **Bassa varianza:** Riduce sensibilmente il rischio di overfitting rispetto ai singoli alberi. | **Scatola nera (Black Box):** Perde la totale interpretabilità visiva tipica del singolo albero decisionale. |
| **Versatilità:** Gestisce dati sia categorici che continui, senza richiedere normalizzazione o scalatura. | **Costo computazionale:** Richiede più memoria e tempo di inferenza per aggregare centinaia di alberi. |
| **Robusto agli outlier e al rumore:** L'aggregazione smussa le deviazioni estreme. | **Regressione limitata:** Non può estrapolare valori al di fuori dell'intervallo osservato nel training set. |

---

## 4. Feature Importance

Un sottoprodotto fondamentale di Random Forest è la stima dell'importanza relativa delle variabili:
- Si calcola sommando la riduzione totale dell'impurità (Gini o Entropia) apportata da ciascuna feature lungo tutti i nodi di tutti gli alberi della foresta (*Mean Decrease in Impurity*).
- Permette di effettuare una rapida fase di **Feature Selection** prima di impiegare modelli più complessi.

---

> [!info] Collegamenti Utili
> - [[Decision Tree Learning|decision tree]]
> - [[Entropia]]

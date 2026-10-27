---
tags:
  - supervised
  - regression
aliases:
  - Regressori
cssclasses:
  - machine-learning
---
> [!abstract] Il Regressore (Concetto e Tassonomia)
> **Supervised Learning** $\rightarrow$ **Regressione** *(non Classificazione)*
> * **Definizione:** Modello statistico e predittivo che mappa una o più variabili indipendenti (*feature* $X$) in una variabile dipendente (*target* $y$).
> * **Compito:** Apprendimento supervisionato (i dati di training contengono coppie note input-output $(X, y)$).
> * **Distinzione chiave:** Prevede un valore numerico **continuo** (es. prezzi, temperature).
> * **Obiettivo teorico:** Apprendere una funzione di ipotesi $h(x)$ che stimi la vera relazione $f(X)$ sottostante ai dati, minimizzando l'errore di stima complessivo tramite una specifica funzione di costo.

>[!tip] Obiettivo chiave
> Sintetizzare i dati grezzi in una rappresentazione matematica più semplice, interpretabile e riutilizzabile per fare previsioni future.

### Cos'è la Regressione?
È un processo statistico (e di Machine Learning) utilizzato per modellare e stimare la *relazione matematica tra una o più variabili predittive e un risultato continuo*.

---

### Variabili in gioco

| Variabile | Sinonimi comuni | Ruolo pratico | Esempio |
| :--- | :--- | :--- | :--- |
| **Indipendente (IV)** | *Feature*, Predittore, Input, $X$ | I dati noti usati come punto di partenza per stimare il risultato. | Superficie della casa ($m^2$) |
| **Dipendente (DV)** | *Target*, Etichetta, Output, $y$ | Il valore sconosciuto che il modello deve prevedere o spiegare. | Prezzo di vendita (€) |

> **In sintesi:** Modifichi o osservi le **IV** per stimare come cambierà la **DV** secondo una **$F$**:
> 
> $DV=F(IV)$.

| Ruolo | Condizione | Descrizione | Classificazione |
| :--- | :--- | :--- | :--- |
| **Target (DV)** | $\vert DV\vert = 1$ | Un solo target | **Univariata** |
| | $\vert DV\vert > 1$ | Più target | **Multivariata** |
| **Feature (IV)** | $\vert IV\vert = 1$ | Una sola feature | **Semplice** (*Simple*) |
| | $\vert IV\vert > 1$ | Più feature | **Multipla** (*Multiple*) |
<div style="page-break-after: always;"></div>

<img src="regressione.png" style="float: left; margin-right: 20px; width: 270px;" alt="descrizione">


Modella la variabile dipendente y come combinazione lineare delle feature x, pesate dai coefficienti w più un termine di intercetta b.
$$y = \mathbf{w}^T \mathbf{x} + b$$


<div style="clear: both; padding-bottom: 25px;"></div>


### Modelli di Regressione Principali

Differenti relazioni richiedono differenti approccio alla regressione:
- **[[Regressione lineare]]:** Modella relazioni lineari dirette ($y = \mathbf{w}^T\mathbf{x} + b$).
- **[[Polynomial Regression]]:** Cattura ==andamenti non lineari== elevando le feature a *potenza*.
- **[[Logistic Regression]]:** Usa la regressione per stimare probabilità, ma è impiegata per ==compiti di classificazione==.
- **Non-parametric / Semi-parametric:** Modelli flessibili che non impongono una forma funzionale rigida a priori (es. *Kernel regression*, Spline).
- **[[Principal Component Analysis (PCA)|PCA]] (Principal Component Analysis):** Tecnica di ==riduzione della dimensionalità== spesso usata a monte per eliminare multicollinearità tra le variabili.

### workflow degli algoritmi di regressione

<div style="text-align: center;">
  <img src="regression-workflow.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 600px; max-width: 100%; height: auto;" />
</div>



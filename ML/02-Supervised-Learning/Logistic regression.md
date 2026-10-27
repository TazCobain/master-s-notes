---
cssclasses:
  - machine-learning
tags:
  - supervised
  - regression
  - classification
---
> [!abstract] In sintesi
> La **Regressione Logistica** è un algoritmo di classificazione utilizzato per *stimare la probabilità che un'osservazione appartenga a una specifica classe discreta*. 
> Applica una funzione non lineare (la **sigmoide**) a una combinazione lineare delle feature per mappare l'output nell'intervallo $[0, 1]$. I parametri ottimali vengono stimati massimizzando la verosimiglianza tramite la funzione di costo di **Entropia Incrociata (Log Loss)**, risolvibile numericamente via [[Gradient Descent]].
<p align="center">
  <img src="logistic-regression.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 700px; max-width: 100%; height: auto;" />
</p>

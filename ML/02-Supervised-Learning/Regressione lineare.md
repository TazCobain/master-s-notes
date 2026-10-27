---
tags:
  - supervised
  - regression
cssclasses:
  - machine-learning
---
> [!abstract] Regressione Lineare
> Algoritmo di apprendimento supervisionato che modella la relazione tra variabili indipendenti e un target continuo tramite una combinazione lineare. L'obiettivo è stimare i parametri ottimali della retta (o iperpiano) minimizzando lo scarto quadratico medio tra valori reali e predetti.

# L'Algoritmo

> [!info] L'Idea di Base (Obiettivo)
> Selezionare i parametri $\theta_0$ e $\theta_1$ in modo tale che i valori calcolati dalla nostra ipotesi $h(x^{(i)})$ siano **il più vicino possibile** ai valori reali $y^{(i)}$ per ogni singolo campione presente nel Training Set (TS).

### 1. L'Ipotesi e l'Errore Singolo
Il modello formula una predizione (ipotesi) basata su una retta:
$$h(x) = \theta_0 + \theta_1 x$$

L'**errore della funzione di ipotesi** per un singolo campione $i$-esimo è semplicemente la ==differenza tra il valore predetto e il valore reale==:
$$e(x^{(i)}) = h(x^{(i)}) - y^{(i)}$$

---

### 2. Funzione di Costo (Quadratic Error)
Per misurare l'errore complessivo su tutti gli $m$ campioni del dataset, non si guarda il singolo errore, ma si utilizza una **Cost Function** $J(\theta_0, \theta_1)$ basata sull'errore quadratico:

$$J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})^2$$

Sostituendo l'ipotesi $h(x)$ con la sua formula estesa ($\theta_0 + \theta_1 x$), otteniamo:
$$J(\theta_0, \theta_1) = \frac{1}{2m} \sum_{i=1}^{m} (\theta_0 + \theta_1 x^{(i)} - y^{(i)})^2$$

> [!info] Perché dividere per $2m$?
> Oltre a calcolare la media (dividendo per $m$), si aggiunge un $2$ al denominatore per una convenienza matematica: quando si calcolerà la derivata durante l'ottimizzazione, l'esponente $2$ si eliderà con il $2$ al denominatore, semplificando i calcoli.

---

### 3. Minimizzazione
Il training del modello di Machine Learning si traduce quindi in un **problema di ottimizzazione matematica**: trovare la combinazione esatta dei parametri $\theta_0$ (intercetta) e $\theta_1$ (pendenza) che rende la funzione di costo più piccola possibile.

Matematicamente si scrive come:
$$\min_{\theta_0, \theta_1} J(\theta_0, \theta_1)$$


# corrispettivo in codice
```python 
import numpy as np
from sklearn.linear_model import LinearRegression

# 1. Dati: Altezza [cm] -> Peso [kg]
X = np.array([[150], [160], [170], [180], [190]])  # Input (array 2D)
y = np.array([50, 60, 68, 78, 85])                 # Target

# 2. Addestramento del modello
model = LinearRegression()
model.fit(X, y)

# 3. Parametri ottimali (theta_0 e theta_1)
theta_0 = model.intercept_
theta_1 = model.coef_[0]
print(f"Modello: h(x) = {theta_0:.2f} + {theta_1:.2f}x")

# 4. Predizione su un nuovo valore
x_test = np.array([[175]])
pred = model.predict(x_test)
print(f"Peso stimato per 175 cm: {pred[0]:.1f} kg")
```
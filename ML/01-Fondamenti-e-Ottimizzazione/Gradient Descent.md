---
cssclasses:
  - machine-learning
aliases:
  - Discesa del Gradiente (Gradient Descent)
tags:
  - optimization
  - supervised
---
> [!abstract] Definizione Generale
> È un **algoritmo generico e iterativo** utilizzato per calcolare il minimo di una funzione di costo (Cost Function).
> CERCARE QUELLE 2 DEFINIZIONI CHE HA DETTO NEGLI ULTIMI 2 MINUTI

<div style="text-align: center;">
  <img src="gradient-descente.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</div>

---

### Caratteristiche Fondamentali

- **Universale ("The salt of Machine Learning"):** Non è limitato alla sola [[Regressione lineare]]; è il motore di ottimizzazione alla base di moltissimi modelli complessi, inclusi i sistemi a **Reti Neurali** (*[[Neural Networks]]*).
- **Processo Iterativo:** Parte da una stima iniziale e aggiorna ripetutamente i parametri a ogni passo, procedendo lungo la discesa fino a raggiungere il minimo della funzione.


### La Matematica del Gradient Descent

L'algoritmo aggiorna simultaneamente i parametri $\theta_j$ sottraendo una frazione $\alpha$ (learning rate) della derivata parziale della funzione di costo $J(\theta_0, \theta_1)$.

#### 1. Formulazione Matematica

Regola generale di aggiornamento:
$$\theta_j := \theta_j - \alpha \frac{\partial}{\partial \theta_j} J(\theta_0, \theta_1)$$

Calcolando le derivate della MSE, il 2 dell'esponente si elide con il denominatore:
$$\frac{\partial J}{\partial \theta_0} = \frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})$$
$$\frac{\partial J}{\partial \theta_1} = \frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)}) \cdot x^{(i)}$$

Regole di aggiornamento esplicite:
$$\theta_0 := \theta_0 - \alpha \frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})$$
$$\theta_1 := \theta_1 - \alpha \frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)}) \cdot x^{(i)}$$

---

#### 2. Esempio Pratico (1 step con $m=1$)

**Setup iniziale:**
- Campione di training: $x = 2$, $y = 5$
- Parametri iniziali: $\theta_0 = 0$, $\theta_1 = 1$
- Learning rate: $\alpha = 0.1$

**Passo 1: Calcolo della previsione e dell'errore**
- Previsione: $h(x) = \theta_0 + \theta_1 x = 0 + 1(2) = 2$
- Errore: $h(x) - y = 2 - 5 = -3$ (il modello sottostima il dato reale)

**Passo 2: Calcolo del gradiente**
- Gradiente per $\theta_0$: $\text{grad}_0 = -3$
- Gradiente per $\theta_1$: $\text{grad}_1 = (-3) \cdot x = -3 \cdot 2 = -6$

**Passo 3: Aggiornamento dei parametri**
- $\theta_0 := 0 - 0.1 \cdot (-3) = 0 + 0.3 = 0.3$
- $\theta_1 := 1 - 0.1 \cdot (-6) = 1 + 0.6 = 1.6$

Dopo una singola iterazione, l'ipotesi diventa:
$$h(x) = 0.3 + 1.6x$$
> [!note] Aggiornamento simultaneo
> Il simbolo $:=$ indica un'assegnazione. È fondamentale calcolare prima entrambi i gradienti usando i parametri correnti, e solo successivamente aggiornare $\theta_0$ e $\theta_1$ insieme.


#### 3.  Esempio in codice
```python 
import numpy as np
# 1. Dataset giocattolo: Altezza [cm] -> Peso [kg]
X = np.array([150, 160, 170, 180, 190], dtype=float)
y = np.array([50, 60, 68, 78, 85], dtype=float)
# Feature Scaling (normalizzazione standard per facilitare la convergenza)
X_norm = (X - np.mean(X)) / np.std(X)

# 2. Iperparametri del Gradient Descent
alpha = 0.05       # Learning rate
max_epochs = 2000  # Numero massimo di iterazioni di sicurezza
epsilon = 1e-6     # Soglia di tolleranza (stop se delta costo < epsilon)
m = len(y)         # Numero di campioni

# 3. Inizializzazione parametri e costo precedente
theta_0 = 0.0
theta_1 = 0.0
prev_cost = float('inf')

# 4. Ciclo di addestramento con criterio di stop a tolleranza
for epoch in range(max_epochs):
	#Ipotesi:h(x) = theta_0 + theta_1 * x
    predictions = theta_0 + theta_1 * X_norm 
    errors = predictions - y #Errore sui singoli campioni: e = h(x) - y
    
    # Calcolo della funzione di costo attuale J(theta)
    current_cost = (1 / (2 * m)) * np.sum(errors ** 2)
    
    # Criterio di convergenza
    if abs(prev_cost - current_cost) < epsilon:
        print(f"Convergenza raggiunta all'epoca {epoch}!")
        break
    
    prev_cost = current_cost
    
    # Calcolo dei gradienti (derivate parziali della MSE)
    grad_0 = (1 / m) * np.sum(errors)
    grad_1 = (1 / m) * np.sum(errors * X_norm)
    
    # Aggiornamento simultaneo dei parametri
    theta_0 -= alpha * grad_0
    theta_1 -= alpha * grad_1

print(f"Parametri appresi: theta_0 = {theta_0:.3f}, theta_1 = {theta_1:.3f}")
print(f"Costo finale J(theta): {current_cost:.6f}")
```

> [!warning] Criterio di Stop: Evitare il confronto esatto `costo_nuovo == costo_vecchio`
> A causa della rappresentazione dei numeri a virgola mobile (*floating-point arithmetic*), due valori calcolati in successione difficilmente risulteranno identici a livello di bit. Usare una condizione del tipo `if J_new == J_old:` rischia di innescare cicli infiniti.
> 
> **Approccio corretto (tolleranza $\varepsilon$):**
> Interrompere l'algoritmo quando la variazione assoluta tra due iterazioni consecutive scende sotto una soglia minima $\varepsilon$ (es. `1e-6` o la precisione macchina):
> 
> ```python
> epsilon = 1e-6  # Soglia di tolleranza
> 
> if abs(prev_cost - current_cost) < epsilon:
>     print(f"Convergenza raggiunta all'epoca {epoch}!")
>     break
> ```

---
 
## Note utili

> [!tip] Condizione di Ottimalità: Convessità
> Il raggiungimento del minimo (minimo globale) è **garantito matematicamente** se la funzione di costo è **convessa** (ad esempio la funzione quadratica usata nella regressione lineare, che ha la forma di una "ciotola" priva di minimi locali).

> [!warning] Rischio di Divergenza (Overshooting)
> Teoricamente ad ogni iterazione il sistema fa un passo verso il minimo; tuttavia, se il passo è troppo grande ($\alpha$ elevato), c'è il rischio di "scavalcare" la conca e non convergere mai.
> 
> * **Comportamento della derivata:** Man mano che ci si avvicina al minimo, l'inclinazione (derivata $\frac{\partial J}{\partial \theta}$) diminuisce naturalmente, riducendo l'ampiezza dell'aggiornamento anche a parità di $\alpha$. Se però $\alpha$ è eccessivo, il gradiente cresce ad ogni rimbalzo portando alla divergenza.
> * **Soluzione:** Ridurre il learning rate $\alpha$, oppure adottare tecniche di *learning rate decay* (decadimento dinamico) o algoritmi con tasso adattivo (es. Adam, RMSprop).

> [!warning] Il Rischio dei Minimi Locali (*Non-Convex Functions*)
> Se la funzione di costo **non è convessa** (situazione tipica delle Reti Neurali complesse), il paesaggio dell'errore presenta più avvallamenti:
> 
> * **Minimo Locale:** Un punto dove l'errore è più basso rispetto alle zone circostanti, ma non è il valore minimo assoluto.
> * **Il Problema:** Il gradiente in questi punti si annulla ($\nabla J \approx 0$), facendo "credere" all'algoritmo di aver concluso l'ottimizzazione; di conseguenza, il modello si blocca prematuramente e non raggiunge mai il **minimo globale**.
> * **Nella Regressione Lineare:** Questo pericolo non sussiste, poiché la funzione di costo quadratica (MSE) è rigorosamente convessa e garantisce un unico minimo globale.


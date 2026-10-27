---
cssclasses:
  - machine-learning
tags:
  - activation-function
  - classification
---
> [!abstract] In sintesi
> La **ReLU (Rectified Linear Unit)** è la funzione di attivazione più utilizzata negli hidden layer delle reti neurali moderne. Definita matematicamente come $f(x) = \max(0, x)$, introduce la non-linearità indispensabile per apprendere relazioni complesse con un costo computazionale irrisorio. 
> Risolve efficacemente il problema della **scomparsa del gradiente (vanishing gradient)** per valori positivi (dove la derivata è costante e pari a $1$), pur presentando come limite principale il fenomeno del **"Dying ReLU"**, in cui i neuroni con input negativi si disattivano permanentemente con gradiente pari a $0$.

--- 
## 1. Cos'è? 
Immagina la ReLU come una specie di "filtro" estremamente severo con i numeri negativi ma totalmente permissivo con quelli positivi. La regola è semplicissima: 
- Se il numero in entrata è **negativo**, lo trasforma in **0**. 
- Se il numero in entrata è **positivo**, lo lascia **esattamente com'è**. 
  In formula: $$ f(x) = \max(0, x) $$
Se disegniamo il suo grafico, vedremo una linea orizzontale piatta (sullo zero) per tutta la parte sinistra, e poi una linea dritta in salita (a 45 gradi) per tutta la parte destra. 
<p align="center">
  <img src="ReLu-function.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 350px; max-width: 100%; height: auto;" />
</p>


## 2. Quando va usata? 
La ReLU è diventata lo standard assoluto ("default") per gli **hidden layers** delle [[reti neaurale]] moderne (reti feedforward, reti convoluzionali CNN, ecc.). 

> [!warning]  dove NON usarla
> Quasi mai nel livello di output finale. Se dobbiamo prevedere una probabilità tra 0 e 1, usiamo una [[Funzione Sigmoide]] o una [[Softmax]]. La ReLU serve solo nei "motori interni" della rete. 
## 3. Perché funziona? 
1. **È velocissima da calcolare:** Il computer non deve calcolare potenze o esponenziali (come $e^{-x}$). Deve solo chiedersi "Questo numero è maggiore di zero?". Questo rende l'addestramento della rete molto più veloce. 
2. **Risolve la "Scomparsa del Gradiente":** Le funzioni come la [[Sigmoide]] "schiacciano" i numeri grandi verso l'1. Quando la rete cerca di imparare (calcolando l'errore a ritroso), questo schiacciamento *fa disperdere il segnale d'errore* (vanishing gradient). La ReLU, non avendo un tetto massimo per i numeri positivi, fa passare il segnale in modo pulito e forte. 
   
## 4. Problema dei "Neuroni Morti" (Dying ReLU) 
La ReLU  soffre di quella cosa definita come **Dying ReLU problem**. Se, durante l'addestramento, un neurone riceve una ==🟡serie di input molto negativi==, l'output della ReLU sarà 0. Quando l'output è 0, anche la sua derivata (la sua capacità di aggiornarsi e imparare) è 0. 
In parole semplici: ==🟡**il neurone "muore"**. Da quel momento in poi smetterà di aggiornarsi==, restando per sempre spento, ignorando qualsiasi dato futuro. 

> [!tip] Come counterare la cosa 
Per evitare questo degradamento dei neurani sono nate delle varianti, come la **Leaky ReLU**. Questa variante, invece di bloccare del tutto i numeri negativi, li fa passare "solo un pochino" (ad esempio moltiplicandoli per $0.01$), permettendo al neurone di rimanere vivo e continuare a imparare. <p align="center">  <img src="leaky-relu-activation-function.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" /> </p>









---
## Collegamenti (Backlinks) 
* [[Funzioni di Attivazione (Panoramica)]] 
* [[Sigmoide|funzione_sigmoide]] 
* [[Vanishing Gradient Problem]] 
* [[Leaky ReLU ed ELU]]



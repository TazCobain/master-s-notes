---
cssclasses:
  - machine-learning
tags:
  - activation-function
  - classification
aliases:
  - funzione_sigmoide
---
> [!abstract] In sintesi
> La **funzione Sigmoide** (o curva logistica) è una funzione di attivazione a forma di "S" definita come $\sigma(x) = \frac{1}{1 + e^{-x}}$, che comprime qualsiasi valore reale nell'intervallo continuo $(0, 1)$. È storicamente fondamentale per modellare probabilità (usata soprattutto nel layer di output per la **classificazione binaria**), ma è stata progressivamente abbandonata nei layer nascosti delle reti profonde per via del grave problema della **scomparsa del gradiente (vanishing gradient)** nelle  regioni sature e del fatto di non essere **centrata sullo zero (zero-centered)**, rallentando la convergenza dell'ottimizzazione.
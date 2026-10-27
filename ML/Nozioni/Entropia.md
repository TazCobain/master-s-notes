---
cssclasses:
  - machine-learning
tags:
  - Teoria
---
Derivata dalla teoria dell'informazione, ==l'entropia misura il grado di incertezza in un insieme di dati ed è associata al numero minimo di bit necessari per codificare una specifica informazione.==

### Formula per il caso binario ($true/false$)
$$Entropy(X) = -p_v \log_2(p_v) - p_f \log_2(p_f)$$

### Interpretazione nei dati
- $E = 0$: Nessuna incertezza, l'informazione è ovvia e non serve inviare bit (insieme puro).
- $E = 1$: Incertezza massima nel caso binario, è necessario un bit intero per ogni campione.

### Formula generale per $C$ classi
$$E(TS) = -\sum_{i=1}^{C} p_i \log_2(p_i)$$

---

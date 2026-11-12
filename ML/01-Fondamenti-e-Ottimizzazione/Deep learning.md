---
cssclasses:
  - machine-learning
tags:
  - ML-teoria
aliases:
  - DL
---
Il **Deep Learning** (apprendimento profondo) è una sottocategoria del Machine Learning che utilizza **reti neurali artificiali** strutturate su più livelli (*deep*, ovvero "profondi") per apprendere autonomamente rappresentazioni complesse a partire da grandi quantità di dati grezzi.

> [!abstract] In breve il deep learning
> Mentre nel Machine Learning tradizionale l'essere umano deve estrarre manualmente le caratteristiche rilevanti dai dati (*feature engineering*), nel Deep Learning è la rete stessa a scoprire quali caratteristiche contano, passando da concetti semplici a concetti sempre più astratti.

---

## 🏗️ Come funziona: l'architettura a strati

Una rete neurale profonda (*Deep Neural Network* - DNN) è composta da nodi (**neuroni artificiali** o *percettroni*) organizzati in strati sequenziali:

1. **Input Layer (Strato di ingresso):** Riceve i dati grezzi (es. i pixel di un'immagine, le parole di un testo, i campioni di un file audio).
2. **Hidden Layers (Strati nascosti):** È qui che avviene la "magia". Ogni strato elabora le informazioni ricevute dal precedente, applicando pesi matematici e funzioni di attivazione non lineari.
   - *Primi strati:* Riconoscono pattern elementari (es. bordi, linee, contrasti).
   - *Strati intermedi:* Combinano i pattern per formare elementi più complessi (es. forme geometriche, occhi, ruote).
   - *Strati finali:* Riconoscono l'oggetto nella sua interezza (es. un volto umano, un'automobile).
3. **Output Layer (Strato di uscita):** Restituisce il risultato finale (es. una classificazione, una probabilità o un nuovo contenuto generato).

---

## ⚙️ Il processo di addestramento (Training)

Per imparare, una rete neurale ripete milioni di volte questo ciclo:

1. **Forward Propagation:** I dati attraversano la rete dall'input all'output generando una previsione.
2. **Calcolo dell'errore (Loss Function):** Si misura quanto la previsione si discosta dal risultato reale desiderato.
3. **Backpropagation (Retropropagazione):** L'errore viene propagato all'indietro attraverso la rete per capire quanto ogni singolo neurone ha contribuito allo sbaglio.
4. **Ottimizzazione (Gradient Descent):** I "pesi" delle connessioni tra i neuroni vengono leggermente modificati per ridurre l'errore al tentativo successivo.

---

## 🧩 Principali architetture

A seconda del tipo di dato da analizzare, si utilizzano architetture specifiche:

| Architettura | Acronimo | Uso principale |
| :--- | :--- | :--- |
| **Convolutional Neural Networks** | `CNN` | Visione artificiale, riconoscimento immagini e video. |
| **Recurrent Neural Networks** | `RNN` / `LSTM` | Dati sequenziali, serie temporali, analisi audio (oggi spesso sostituite dai Transformer). |
| **Transformers** | — | Elaborazione del linguaggio naturale ([[LLM]]), traduzione, generazione multimodale. |
| **Generative Adversarial Networks** | `GAN` | Generazione di immagini sintetiche, deepfake, upscaling. |
| **Diffusion Models** | — | Generazione di immagini ad altissima qualità partendo dal rumore (es. Stable Diffusion, Midjourney). |

---

## ⚖️ Confronto rapido: Machine Learning vs Deep Learning

- **Quantità di dati:** Il DL richiede enormi dataset per brillare; il ML classico funziona bene anche con pochi dati.
- **Hardware:** Il DL necessita di grande potenza di calcolo (GPU / TPU) per l'addestramento.
- **Interpretabilità:** Il DL è spesso una *"Black Box"* (difficile capire esattamente perché ha preso una decisione), mentre molti algoritmi di ML sono più trasparenti.

---
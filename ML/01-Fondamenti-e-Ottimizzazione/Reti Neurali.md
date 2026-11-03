---
cssclasses:
  - machine-learning
tags:
  - ML-teoria
aliases:
  - Neural Network
  - NN
---
> [!abstract] In breve le reti neurali
> Una rete neurale artificiale è un modello strutturato in livelli sequenziali per l'elaborazione di pattern complessi. I dati grezzi vengono acquisiti dall'Input Layer e trasmessi agli Hidden Layer, dove l'effettiva computazione avviene tramite matrici di pesi matematici.
> Il risultato di questa elaborazione viene infine tradotto dall'Output Layer in una previsione o classificazione finale. Il cuore dell'architettura è l'applicazione delle funzioni di attivazione, che introducono la non-linearità necessaria per permettere alla rete di apprendere e mappare relazioni complesse, superando i limiti della semplice regressione lineare.

## Architettura
Una **rete neurale (NN)** è un modello matematico e computazionale ispirato al funzionamento del cervello biologico. È progettata per riconoscere pattern complessi nei dati e prendere decisioni o fare previsioni. ==La rete "impara" aggiustando iterativamente i collegamenti tra i suoi nodi (neuroni) durante la fase di addestramento==.  
L'architettura di base di una rete neurale si divide in tre tipologie principali di livelli (layer).
<p align="center">   <img src="NN-scheme.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>

### 1. Input Layer (Livello di Ingresso)
È il punto di accesso dei dati grezzi nella rete.
- **Funzione:** Riceve le informazioni dall'esterno (es. i pixel di un'immagine, le parole di un testo, i valori numerici di un dataset) e le passa al livello successivo.    
- **Caratteristiche:** I neuroni in questo livello non compiono elaborazioni matematiche attive; servono solo come "passacarte". Il numero di neuroni in questo layer corrisponde esattamente al numero di _feature_ (variabili) del dato in ingresso.
### 2. Hidden Layer(s) (Livelli Nascosti)
I livelli nascosti si trovano tra l'input e l'output e sono il "motore" computazionale della rete. Una rete con più livelli nascosti è definita "Deep Neural Network" (da cui _Deep Learning_).
- **Funzione:** ==🟡Estraggono caratteristiche sempre più complesse e astratte dai dati.== Ogni neurone riceve i dati dal layer precedente, li moltiplica per un **peso (weight)**, aggiunge un valore di **bias**, e passa il risultato alla funzione di attivazione.
- **I Pesi (Weights):** I pesi sono i parametri reali che la rete impara e memorizza. Rappresentano l'importanza di una determinata connessione tra due neuroni.

> [!note] Open Weights vs Closed Models
> Nel panorama moderno dell'Intelligenza Artificiale, i miliardi di pesi contenuti negli _hidden layers_ definiscono il valore commerciale e le capacità del modello.
> - **Open Weights:** Modelli (come Llama di Meta o Mistral) in cui le matrici dei pesi addestrati vengono rilasciate pubblicamente. Gli sviluppatori possono scaricare il modello, ispezionare gli _hidden layers_, eseguirlo in locale e modificarlo (fine-tuning).
> - **Closed (Proprietari):** Modelli (come GPT-4 di OpenAI o Claude di Anthropic) in cui i pesi e l'esatta architettura degli _hidden layers_ sono mantenuti segreti. L'utente interagisce con il modello solo tramite API o interfaccia web (la cosiddetta "black box"), senza avere accesso ai parametri matematici interni.

### 3. Output Layer (Livello di Uscita)
È l'ultimo strato della rete e restituisce il risultato finale dell'elaborazione.
- **Funzione:** Trasforma le rappresentazioni astratte elaborate dagli _hidden layers_ in una previsione interpretabile dall'utente.
- **Caratteristiche:** La sua struttura dipende dal tipo di problema.
	- _==🟠Classificazione binaria==_: 1 singolo neurone (es. restituisce 0 o 1, spam o non-spam).
	- _==🟠Classificazione multi-classe==_: $N$ neuroni, quanti sono le classi possibili (es. probabilità che l'immagine sia un cane, un gatto o un'auto).
	- _==🟠Regressione==_: 1 neurone che restituisce un valore numerico continuo (es. la previsione del prezzo di una casa).

## Il neurone

## Activation Function (Funzione di Attivazione)
La funzione di attivazione è un'operazione matematica applicata al risultato di ogni neurone (dopo aver sommato input $\times$ pesi $+$ bias) prima di passarlo al livello successivo.
- **Scopo principale:** Introdurre la **non-linearità** nel modello.
- **Perché è cruciale?** Senza funzioni di attivazione, non importa quanti _hidden layers_ aggiungi: l'intera rete si comporterebbe come una singola e semplice regressione lineare, incapace di risolvere problemi complessi o mappare relazioni non lineari (come il riconoscimento vocale o visivo).
**Funzioni di attivazione comuni:**
- **ReLU (Rectified Linear Unit):** Restituisce $x$ se positivo, altrimenti $0$. È la più usata negli _hidden layers_ perché computazionalmente leggera e previene il problema della scomparsa del gradiente.
-  **Sigmoide:** Comprime i valori in un intervallo tra $0$ e $1$. Storicamente molto usata, oggi si usa per lo più nell'_output layer_ per la classificazione binaria (interpretando il risultato come probabilità).
- **Softmax:** Utilizzata nell'_output layer_ per la classificazione multi-classe, trasforma i risultati grezzi in una distribuzione di probabilità che somma a $1$.
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

## Il neurone (la base di tutto)
<p align="center">   <img src="NeuralModel.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>

Il neurone (spesso chiamato _nodo_ o _percettrone_) è **l'unità computazionale fondamentale** di una rete neurale. Ispirato al funzionamento del neurone biologico, il suo compito è ricevere informazioni, elaborarle matematicamente e decidere se (e con quanta intensità) trasmettere un segnale ai neuroni successivi.
Il suo funzionamento interno segue una sequenza matematica precisa:
1. **Ricezione e pesatura degli input**: Il neurone riceve i valori in ingresso (che possono essere i dati originali o l'output dei neuroni del layer precedente). Ogni singolo input ($x_i$) viene moltiplicato per il proprio **peso** assegnato ($w_i$), che ==stabilisce quanto quel segnale sia rilevante== per il risultato.
2. **Sommatoria pesata dei bias**: Il neurone calcola la somma di tutti questi input moltiplicati per i rispettivi pesi. A questa somma aggiunge un valore costante chiamato **bias** ($b$) che agisce come una soglia di base (simile all'intercetta in una retta), permettendo al neurone di traslare il risultato per adattarsi meglio al problema.  Matematicamente questo: $$z = \sum (x_i \cdot w_i) + b$$
3. **Attivazione ed emissione**: Il risultato ($z$) non viene passato così com'è ma viene elaborato dalla **funzione di attivazione** ($f(z)$), che lo trasforma e genera l'output finale ($y$) da inviare al livello successivo.

> [!NOTE] iI neurone in matematichese
> $$f(\sum (x_i \cdot w_i) + b)$$

## Activation Function 
La funzione di attivazione è un'operazione matematica applicata al risultato di ogni neurone (dopo aver sommato input $\times$ pesi $+$ bias) prima di passarlo al livello successivo.
- **Scopo principale:** Introdurre la **non-linearità** nel modello.
- **Perché è cruciale?** Senza funzioni di attivazione, non importa quanti _hidden layers_ aggiungi: l'intera rete si comporterebbe come una singola e semplice regressione lineare, incapace di risolvere problemi complessi o mappare relazioni non lineari (come il riconoscimento vocale o visivo).

**Funzioni di attivazione comuni:**
- **ReLU ([[ReLu|Rectified Linear Unit]]):** Restituisce $x$ se positivo, altrimenti $0$. È la più usata negli _hidden layers_ perché computazionalmente leggera e previene il problema della scomparsa del gradiente.
-  **[[Sigmoide]]:** Comprime i valori in un intervallo tra $0$ e $1$. Storicamente molto usata, oggi si usa per lo più nell'_output layer_ per la classificazione binaria (interpretando il risultato come probabilità).
- **[[Softmax]]:** Utilizzata nell'_output layer_ per la classificazione multi-classe, trasforma i risultati grezzi in una distribuzione di probabilità che somma a $1$.
<p align="center">   <img src="type-of-activation-function.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 550px; max-width: 100%; height: auto;" /> </p>

---
> [!warning] Attenzione: Rischio di Addestramento Infinito (Mancata Convergenza) 
> Poiché l'addestramento di una rete neurale è un processo iterativo basato sull'ottimizzazione e sulla minimizzazione continua dell'errore (Loss), senza precise condizioni di interruzione il modello potrebbe continuare ad aggiornare i pesi all'infinito senza mai trovare una soluzione definitiva.
 > Per evitare che il _training loop_ giri a vuoto o rimanga intrappolato, devono sussistere determinate condizioni e salvaguardie architettoniche: 
> - **Arresto Anticipato (Early Stopping):** Un meccanismo di controllo che interrompe forzatamente l'addestramento se le prestazioni sui dati di validazione non migliorano per un numero definito di cicli (epoche).
> - **Imporre un limite massimo di iterazioni (Max Epochs)**


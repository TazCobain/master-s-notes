---
cssclasses:
  - machine-learning
---

**Nb: queste cose vanno sapute a menadito perché il prof scassa il cazzo e ci tiene ci tiene**

### Cos'è il machine learning?
  *Il Machine Learning studia algoritmi capaci di apprendere una certa conoscenza a partire da un dataset, per poi applicarla su nuovi dati*
  
  L'obiettivo principale è ==generalizzare un concetto da un numero limitato di esempi==, quando un'analisi esaustiva di tutti gli input possibili non è praticabile.

### Suddivisione dei dati
1) **Training Set**: Il dataset usato per apprendere la conoscenza. È il cuore del processo di addestramento.
2) **Validation Set**: Usato per misurare le prestazioni durante l'apprendimento. Fondamentale per rilevare l'overfitting.
3) **Test Set**: Usato per misurare le prestazioni dopo l'apprendimento, su dati completamente nuovi.
### Cos'è un vettore
La possiamo definire come una tupla che identifica un punto in uno spazio. Avrà una sua direzione ed un suo modulo. 
==Brutalmente nel ML è un punto in uno spazio definito da tutte le misurazioni che abbiamo.==

#### esempio peso persone
Future vector: \[89 kg, 175 cm, 40 anni, **Maschio**]
in questo caso abbiamo una variabile descrittiva che non può essere messa in un paino quindi va fatto un mapping, converto le variabili descrittive in un valore numerico (nb: si può fare se le combinazioni sono finire e sai quante sono).

### Spazi delle Feature
Uno spazio delle feature è uno spazio vettoriale in cui ogni feature corrisponde a una dimensione. Ogni campione del dataset diventa un punto in questo spazio.
<div style="text-align: center;">
  <img src="spazioVettoriale.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</div>

#### Feature: Classificazione
Un algoritmo ML che classifica fiori iris opera nello spazio delle feature: il suo obiettivo è suddividere lo spazio in tre regioni, una per ciascuna specie. 
Ogni nuova osservazione viene assegnata  alla classe corrispondente alla regione del feature space in cui cade il suo feature vector.
*La qualità della separazione dipende dalla scelta delle feature e dall'algoritmo utilizzato*.


### Problema della dimensionalità
<p align="center">
  <img src="dimensionalitaFeatures.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</p>

Esempio:
Il dataset Arrhythmia contiene ECG di 452 pazienti con 279 feature ciascuno. 
L'obiettivo è distinguere ECG normali da 15 tipi di aritmia cardiaca. Se in 2D bastano 100 campioni per addestrare il modello, con 3 dimensioni ne servono molti di più. ==Il numero di campioni necessari cresce esponenzialmente con le dimensioni.==

**\+ aumentano le dimensioni e \+ aumentano le features da utilizzare. Ogni dimensione aumenta di un fattore$^2$ **

### Che problemi risolve il ML?
<p align="center">
  <img src="ML-problem-resolve.png" style="background-color: white; padding: 10px; border-radius: 6px; max-width: 100%; height: auto;" />
</p>

#### Classificatori
2 opprocci
- ==oneVSall==: classificatore binario per ogni classe contro tutte le altre.
	  Praticamente ho sempre 2 blocchi distinti in cui vado a prendere il targhet che mi interessa e lo sapero da tutto il resto. Quindi per $n$ calssi avrò $n$ calssificatori. (soluzione. più comune).
- ==oneVSone==: una classificatore per ogni coppia di calssi.
  *esempio*: "è pedone o non è pedone, bici o non bici"
  *problema*: in questo caso se ho una persona che va in bici potrebbero arrivarsi entrambe le classi.

**Gli algormi di classificazione sono labellizati!**

#### Clustering
<p align="center">
  <img src="clustering.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</p>

L'obiettivo è **raggruppare feature vector con proprietà simili**, senza usare etichette predefinite. Il clustering è un tipico task di apprendimento ==non supervisionato==.

**Il clustering è utile per l'analisi esplorativa dei dati: rivela strutture nascoste che potrebbero non essere evidenti a priori.**


#### Regressori
<p align="center">
  <img src="regressione.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</p>

L'obiettivo è modellare l'==evoluzione di una variabile== dipendente in funzione di una o più variabili indipendenti, per effettuare previsioni quantitative.
**approfondimento**: [[-Regressori|Regressori]]


#### Riduzione della dimensione
==Ridurre il numero di feature rende gli algoritmi più affidabili ed efficienti==, contrastando la maledizione della dimensionalità. 

Esempio — Eigenfaces: anziché rappresentare un volto come 9900 pixel (90×110), lo si decompone come combinazione lineare di poche immagini di riferimento (eigenfaces), riducendo drasticamente le dimensioni necessarie.

### Paradigmi di Apprendimento
<div style="text-align: center;">
  <img src="paradigmiApprendimento.png" style="background-color: white; padding: 10px; border-radius: 6px; max-width: 100%; height: auto;" />
</div>

![[self-supervised-learning.png]]



### Underfitting e Overfitting
#### Underfitting
Si parla di underfitting quando il modello *non ha sufficiente capacità espressiva per  rappresentare la distribuzione* dei dati. Il modello è troppo semplice rispetto alla complessità del problema.
<div style="text-align: center;">
  <img src="underfitting.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</div>

#### Overfitting
Si parla di overfitting quando l'algoritmo si *specializza eccessivamente nel modellare i dati di training*, perdendo la capacità di generalizzare su nuovi dati.
<div style="text-align: center;">
  <img src="overfitting.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 400px; max-width: 100%; height: auto;" />
</div>

##### cause
- *Modello troppo complesso*
- *Dati insufficienti*
- *Curse of Dimensionality*: con molte feature, il numero di campioni necessari cresce
  esponenzialmente. I dati disponibili diventano "scarsi" nello spazio ad alta dimensione.

##### come counterare la cosa
<div style="text-align: center;">
  <img src="overfitCounter.png" style="background-color: white; padding: 10px; border-radius: 6px; max-width: 100%; height: auto;" />
</div>

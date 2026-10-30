---
Tags:
  - classification
  - dimensionality-reduction
  - LDA
cssclasses:
  - machine-learning
aliases:
  - LDA
  - Linear Discriminant Analysis
---
> [!abstract] Linear Discriminant Analysis in breve
> LDA unisce riduzione della dimensionalità e classificazione proiettando i campioni lungo direzioni ottimali che ==🟡massimizzano la distanza tra le medie delle classi e minimizzano la dispersione interna==. L'ottimizzazione del rapporto tra le matrici di scatter $S_B$ e $S_W$ si risolve tramite un problema agli autovalori generalizzato, limitando la dimensione del sottospazio discriminante a un massimo di $D-1$. In presenza di matrici singolari dovute al problema dello _Small Sample Size_, l'approccio regolarizzato evita l'eliminazione del null space di $S_W$, preservando l'informazione a più elevato potere discriminativo.

> [!tip] quanto funziona?
> > LDA funziona se le sue precondizioni sono rispettate; ovvero che i dati devono essere distribuiti, secondo l'appartenenza ad una classe, in modo gaussiane

# Linear Discriminant Analysis (LDA): Classificazione in Spazi Proiettati

## 1. Introduzione e Intuizione Teorica

### Il Problema della Classificazione
Nel contesto del Machine Learning, l'obiettivo di una **regola di classificazione** è definire un criterio che, partendo da un insieme di misurazioni, sia in grado di ==associare una specifica classe a un determinato pattern==. Dal punto di vista matematico, distinguiamo due elementi fondamentali:
* **Variabile indipendente ($x$):** rappresenta il vettore delle *feature* (le misurazioni effettuate sull'oggetto).
* **Variabile dipendente ($y$):** rappresenta la classe o il gruppo di appartenenza degli oggetti.

### L'Obiettivo di LDA e la Separabilità Lineare
La **Linear Discriminant Analysis (LDA)** si pone l'obiettivo di determinare una ==🟠combinazione lineare nello spazio delle feature che separi linearmente gli oggetti nei rispettivi gruppi o classi==. A seconda della dimensione dello spazio delle feature, il confine di separazione lineare assume una forma geometrica differente:
* **2 Feature** $\implies$ Linea.
* **3 Feature** $\implies$ Piano.
* **4 Feature** $\implies$ Iper-piano.

> [!info] Intuizione: Dalla Separazione Diretta alla Proiezione
> Nei casi reali è molto difficile che gli oggetti possano essere separati linearmente in modo netto direttamente nello spazio originale per definire l'appartenenza a una classe. Per superare questo ostacolo, l'idea chiave di LDA è **unire la riduzione della dimensionalità all'interno del problema di classificazione**. Invece di cercare subito un confine nello spazio originale, cerchiamo le **direzioni dello spazio delle feature** (rappresentate da un vettore $w$) che risultano più efficienti per la discriminazione quando vi proiettiamo sopra i nostri dati.
> 
> Osservando i grafici nello spazio bidimensionale $(x_1, x_2)$, se scegliamo una direzione di proiezione $w$ "sbagliata", le ombre (proiezioni) dei punti appartenenti a due classi diverse (es. punti rossi e punti neri) si sovrappongono sulla retta $w$, rendendo difficile distinguerli. Se invece ruotiamo la retta $w$ lungo una direzione ottimale, le proiezioni delle due classi si raggruppano in zone ben distinte della retta, massimizzando la capacità di discriminazione.

---

## 2. Meccanica Matematica: Il Caso a 2 Classi

Analizziamo passo dopo passo come trovare matematicamente la direzione di proiezione ottimale $w$ nel caso binario (problema a 2 classi).

### Setup del Problema e Proiezione
* **Campioni originali:** disponiamo di $n$ vettori $d$-dimensionali $x_1, \dots, x_n$ appartenenti a due classi $C_1$ e $C_2$ (associate ai gruppi $Y_1, Y_2$).
* **Proiezione dei campioni:** proiettiamo i vettori $d$-dimensionali in una singola dimensione lungo la direzione $w$ tramite il prodotto scalare:
  $$y = w^T x$$
  ottenendo così dei campioni scalari proiettati $y$ appartenenti alle due classi.

### Il Criterio di Fisher nello Spazio Proiettato
Per ottenere una separazione ottimale nel nuovo spazio di rappresentazione, la proiezione LDA punta a soddisfare contemporaneamente due requisiti geometrici:
1. **La media di ogni classe deve avere la massima separazione possibile** (massimizzare la distanza tra i centri delle classi proiettate $|\mu'_1 - \mu'_2|$).
2. **La varianza di ogni classe deve essere minima** (rendere ogni classe il più compatta possibile attorno alla propria media, minimizzando $\sigma'_1$ e $\sigma'_2$).

Definiamo nello spazio proiettato:
* $\tilde{\mu}_i$: la media dei campioni proiettati $y \in C_i$.
* $\tilde{s}_i^2$: la dispersione (*scatter*) dei campioni proiettati della classe $C_i$, definita come:
  $$\tilde{s}_i^2 = \sum_{y \in C_i} (y - \tilde{\mu}_i)^2$$

> [!tip] Funzione Obiettivo $J(w)$
> Il criterio di ottimizzazione consiste nel **massimizzare** il rapporto tra la distanza quadratica delle medie proiettate e la somma delle dispersioni interne delle due classi proiettate:
> $$J(w) = \frac{|\tilde{\mu}_1 - \tilde{\mu}_2|^2}{\tilde{s}_1^2 + \tilde{s}_2^2}$$

---

### Passo 1: La Matrice di Dispersione Interna (*Within-Class Scatter Matrix* $S_W$)
Per determinare la proiezione ottima $w^*$, dobbiamo esprimere la funzione obiettivo $J(w)$ esplicitamente in funzione di $w$ e dei dati originali $x$.

Nello spazio originale delle feature $x$, definiamo una misura di dispersione (*scatter*) per ciascuna classe $C_i$ chiamata **matrice scatter** $S_i$ (che rappresenta la matrice di covarianza della classe $C_i$ a meno di un fattore di scala):
$$S_i = \sum_{x \in C_i} (x - \mu_i)(x - \mu_i)^T$$
La somma delle matrici di dispersione delle singole classi prende il nome di **within-class scatter matrix** ($S_w$ o $S_W$):
$$S_w = S_1 + S_2$$

Ora colleghiamo la dispersione dei campioni proiettati $\tilde{s}_i^2$ alla matrice $S_i$ sostituendo $y = w^T x$ e $\tilde{\mu}_i = w^T \mu_i$:
$$\begin{aligned}
\tilde{s}_i^2 &= \sum_{y \in C_i} (y - \tilde{\mu}_i)^2 \\
&= \sum_{x \in C_i} (w^T x - w^T \mu_i)^2 \\
&= \sum_{x \in C_i} w^T (x - \mu_i)(x - \mu_i)^T w \\
&= w^T S_i w
\end{aligned}$$
Di conseguenza, il denominatore del criterio $J(w)$ (lo scatter interno totale dei campioni proiettati, indicato con $\tilde{S}_w$) può essere riscritto come:
$$\tilde{s}_1^2 + \tilde{s}_2^2 = w^T S_1 w + w^T S_2 w = w^T (S_1 + S_2) w = w^T S_w w = \tilde{S}_w$$

---

### Passo 2: La Matrice di Dispersione tra Classi (*Between-Class Scatter Matrix* $S_B$)
Procediamo in modo analogo per il numeratore di $J(w)$, esprimendo la distanza quadratica tra le medie proiettate in funzione di $w$:
$$\begin{aligned}
(\tilde{\mu}_1 - \tilde{\mu}_2)^2 &= (w^T \mu_1 - w^T \mu_2)^2 \\
&= w^T (\mu_1 - \mu_2)(\mu_1 - \mu_2)^T w \\
&= w^T S_B w = \tilde{S}_B
\end{aligned}$$
Dove:
* $S_B = (\mu_1 - \mu_2)(\mu_1 - \mu_2)^T$ è chiamata **between-class scatter** dei campioni originali.
* $\tilde{S}_B = w^T S_B w$ è chiamata **between-class scatter** dei campioni proiettati.

---

### Passo 3: Massimizzazione del Criterio e Soluzione Ottima
Unendo i risultati dei Passi 1 e 2, il criterio di massimizzazione $J(w)$ si esprime interamente in termini di $w$ e delle matrici di scatter $S_B$ e $S_W$:
$$J(w) = \frac{|\tilde{\mu}_1 - \tilde{\mu}_2|^2}{\tilde{s}_1^2 + \tilde{s}_2^2} = \frac{w^T S_B w}{w^T S_W w}$$

Per trovare il vettore ottimo $w$, calcoliamo la derivata parziale di $J(w)$ rispetto a $w$ e la poniamo uguale a zero:
$$\frac{\partial}{\partial w} J(w) = \frac{\partial}{\partial w} \left( \frac{w^T S_B w}{w^T S_W w} \right) = 0$$
Sviluppando la condizione di stazionarietà (assumendo $S_W$ invertibile), si ottiene l'equazione agli autovalori:
$$S_W^{-1} S_B w - J(w)w = 0$$
Poiché nel caso a 2 classi il termine $S_B w = (\mu_1 - \mu_2)(\mu_1 - \mu_2)^T w$ ha sempre la direzione del vettore $(\mu_1 - \mu_2)$, la direzione della soluzione ottima è data direttamente da:
$$w = S_W^{-1}(\mu_1 - \mu_2)$$

---

## 3. Estensione al Caso Multiclasse ($D$ Classi)

Quando il problema di classificazione coinvolge $D$ classi invece di 2, una singola retta può non bastare: vogliamo quindi proiettare lo spazio delle feature su **direzioni multiple** $w_i$ (indicate complessivamente dalla matrice $W$ le cui colonne sono i vettori $w_i$).

> [!info] Visualizzazione nel Caso Multiclasse
> Immaginiamo 3 classi distribuite come ellissoidi nello spazio tridimensionale. Proiettando questi 3 ellissoidi su un piano generico $W_2$, le proiezioni bidimensionali potrebbero sovrapporsi parzialmente. Scegliendo invece il sottospazio ottimo $W_1$, le 3 classi risultano perfettamente separate sul piano di proiezione.

### Proiezione e Matrici di Scatter per $D$ Classi
La proiezione di un campione $x$ lungo la $i$-esima direzione è data da $y_i = w_i^T x$, che in forma matriciale compatta per tutte le direzioni diventa:
$$y = W^T x$$

Le matrici di dispersione vengono generalizzate per $D$ classi nel seguente modo:
* **Within-class scatter matrix ($S_w$):** è la somma delle matrici di covarianza interne a tutte le $D$ classi:
  $$S_w = \sum_{i=1}^D S_i = \sum_{i=1}^D \sum_{x \in C_i} (x - \mu_i)(x - \mu_i)^T$$
* **Between-class scatter matrix ($S_B$):** misura la dispersione delle medie delle singole classi $\mu_i$ rispetto alla media globale $\mu$ di tutti i campioni, pesata per il numero di campioni $n_i$ presenti nella classe $i$-esima:
  $$S_B = \sum_{i=1}^D n_i (\mu_i - \mu)(\mu_i - \mu)^T$$

### Problema agli Autovalori Generalizzato e Riduzione della Dimensionalità
Il criterio da massimizzare viene formulato tramite il rapporto dei determinanti (o moduli) delle matrici proiettate:
$$J(w) = \frac{|w^T S_B w|}{|w^T S_W w|}$$

La soluzione di questo problema di ottimizzazione porta a un **problema agli autovalori generalizzato**:
$$S_B w_i = \lambda_i S_W w_i$$
Se $S_W$ è invertibile, possiamo moltiplicare a sinistra per $S_W^{-1}$, riconducendoci alla ricerca degli **autovettori** $w_i$ della matrice $S_W^{-1} S_B$:
$$S_W^{-1} S_B w_i = \lambda_i w_i$$
In forma matriciale per tutti gli autovettori $W$ e la matrice diagonale degli autovalori $\Lambda$, scriviamo:
$$S_W^{-1} S_B W = \Lambda W$$

> [!warning] Vincolo Fondamentale sulla Dimensionalità del Sottospazio
> Quante direzioni di proiezione $w_i$ possiamo estrarre al massimo?
> * Poiché $S_B$ è la somma di $D$ matrici di rango 1 i cui vettori $(\mu_i - \mu)$ sono legati linearmente dalla definizione della media globale $\mu$, la matrice $S_B$ ha **al massimo rango $D-1$**.
> * Di conseguenza, ci possono essere **al massimo $D-1$ autovalori non nulli** e, quindi, al massimo **$D-1$ soluzioni (autovettori $W_i$)**.
> * **Conclusione teorica cruciale:** La dimensionalità del sottospazio di classificazione è **limitata superiormente dal numero di classi del problema ($D-1$)** e *non* dalla dimensionalità originale o dalla complessità dello stesso.

---

## 4. Precondizioni e Limiti di LDA

### Ipotesi di Gaussianità e Casi di Fallimento
LDA opera con successo solo se le sue precondizioni sono verificate:
* **I dati devono essere distribuiti in modo Gaussiano rispetto all'appartenenza a una classe**.

Dall'analisi visiva delle distribuzioni patologiche, emergono tre scenari classici in cui LDA fallisce:
1. **Dati multimodali con medie coincidenti ($\mu_1 = \mu_2 = \mu$):** ad esempio una configurazione a "scacchiera" (tipo XOR) in cui ciascuna classe $\omega_1$ e $\omega_2$ è divisa in più cluster simmetrici rispetto all'origine. Poiché le medie globali delle due classi coincidono ($\mu_1 = \mu_2$), la matrice $S_B$ si annulla e LDA non riesce a trovare una direzione discriminante.
2. **Classi Gaussiane incrociate con la stessa media ($\mu_1 = \mu_2 = \mu$):** quando due ellissoidi appartenenti a classi diverse $\omega_1$ e $\omega_2$ condividono lo stesso centro ($\mu_1 = \mu_2 = \mu$) e differiscono solo per l'orientamento della varianza, LDA fallisce perché si basa sulla distanza tra le medie per separare le classi.
3. **Distribuzioni non Gaussiane (non linearmente separabili):** se le classi $\omega_1$ e $\omega_2$ hanno forme curve e intrecciate (es. forme a "mezzaluna" o "ferro di cavallo"), anche se le medie $\mu_1$ e $\mu_2$ sono distinte, nessuna proiezione lineare può separare le classi senza sovrapporre le code delle distribuzioni.

### Limite sul Numero di Feature: Recursive Fisher Linear Discriminant
* Il vincolo stringente sul numero totale di feature estraibili tramite Fisher Linear Discriminant (al massimo $D-1$) ha limitato seriamente la sua applicazione a un'ampia classe di problemi complessi.
* Per superare questo limite, in letteratura (Xiang, Fan, Lee, *"Face recognition using recursive Fisher linear discriminant"*, IEEE Transactions on Image Processing, 2006) è stata introdotta una **procedura ricorsiva** per calcolare ulteriori feature discriminanti oltre il limite standard.

---

## 5. Il Problema "Small Sample Size" (SSS) e Regularized LDA

### Il Problema della Singolarità di $S_W$
La formulazione standard di LDA ($S_W^{-1} S_B W = \Lambda W$) funziona solo quando la matrice $S_w$ è **non-singolare** (ossia invertibile).
* Tuttavia, nelle applicazioni reali (come il riconoscimento facciale, dove i vettori delle feature hanno dimensione altissima ma si dispone di pochi esempi di addestramento), a causa dello **Small Sample Size problem (SSS)** accade spesso di avere una matrice **$S_w$ singolare** (non invertibile).

### Analisi dei Null Space e perché PCA + LDA non è ottimale
Definiamo i sottospazi nucleo (*null space*) delle due matrici di scatter:
* Sia **$A$** il *null space* di $S_B$ (cioè lo spazio dei vettori $w$ tali che $w^T S_B w = 0$, che non portano informazione separatrice tra le medie).
* Sia **$B$** il *null space* di $S_w$ (cioè lo spazio dei vettori $w$ tali che $w^T S_w w = 0$, dove la varianza interna alle classi è nulla).

Un approccio tradizionale (come applicare prima la **PCA** per ridurre la dimensionalità) rimuoverebbe entrambi i null space $A$ e $B$, rendendo $S_w$ invertibile. Tuttavia, osserviamo cosa significa massimizzare il rapporto di LDA $\frac{|w^T S_B w|}{|w^T S_W w|}$ nel caso ideale:
* Vogliamo che il numeratore sia non nullo: $|w^T S_B w| \neq 0$ (quindi vogliamo stare fuori da $A$).
* Vogliamo che il denominatore sia minimo, idealmente uguale a zero: $|w^T S_W w| = 0$ (quindi vogliamo proprio trovarci dentro $B$, dove la dispersione intra-classe è zero!).

> [!danger] Perché non bisogna eliminare il Null Space $B$
> **Eliminare il null space $B$ significa rimuovere l'informazione più discriminativa!**
> La base ottima per la proiezione deve invece coprire (*span*) l'intersezione tra il complemento di $A$ (nello spazio totale $R$) e il sottospazio $B$, ovvero:
> $$(R - A) \cap B$$

---

### Soluzione: Regularized LDA
Per preservare l'informazione contenuta in $(R - A) \cap B$ senza incorrere nella divisione per zero dovuta alla singolarità di $S_W$, è sufficiente inserire un **criterio di regolarizzazione** (con parametro $\eta > 0$) al denominatore della funzione obiettivo (Juwei, Plataniotis, Venetsanopoulos, *Pattern Recognition Letters*, 2005):
$$J(w) = \frac{|w^T S_B w|}{|\eta w^T S_B w + w^T S_W w|}$$

#### Algoritmo Passo-Passo per Regularized LDA
Dati i campioni $z_{ij}$ divisi in $C$ classi (dove $C_i$ indica la cardinalità della classe $i$-esima e $N$ il numero totale di campioni), la matrice di trasformazione regolarizzata $\Psi$ si calcola in 6 passi:

1. **Fattorizzazione di $S_b$:** Si esprime la matrice between-class scatter come $S_b = \Phi_b \Phi_b^T$, dove $\Phi_b = [\Phi_{b,1}, \dots, \Phi_{b,C}]$. Ogni colonna è definita da:
   $$\Phi_{b,i} = (C_i / N)^{1/2} (\bar{z}_i - \bar{z})$$
   con la media di classe $\bar{z}_i = \frac{1}{C_i} \sum_{j=1}^{C_i} z_{ij}$ e la media globale $\bar{z} = \frac{1}{N} \sum_{i=1}^C \sum_{j=1}^{C_i} z_{ij}$.
2. **Autovettori nello spazio ridotto:** Si trovano gli $m$ autovettori della matrice più piccola $\Phi_b^T \Phi_b$ corrispondenti ad autovalori non nulli, indicandoli con $E_m = [e_1, \dots, e_m]$.
3. **Sottospazio significativo di $S_b$:** Si calcolano i primi $m$ autovettori più significativi ($U_m$) di $S_b$ e i corrispondenti autovalori ($\Lambda_b$) tramite le relazioni:
   $$U_m = \Phi_b E_m \quad \text{e} \quad \Lambda_b = U_m^T S_b U_m$$
   *(Nota: questo passo proietta i dati fuori dal null space $A$ di $S_b$ e normalizza la dispersione tra le classi).*
4. **Diagonalizzazione di $S_w$ nel sottospazio di $S_b$:** Si pone $H = U_m \Lambda_b^{-1/2}$ e si trovano gli autovettori della matrice proiettata $H^T S_w H$, indicati con $P = [p_1, \dots, p_m]$, **ordinati in ordine crescente di autovalore** (così i primi autovettori corrispondono alla minima varianza intra-classe, inclusi gli autovalori nulli del null space $B$).
5. **Selezione delle componenti:** Si scelgono i primi $M (\le m)$ autovettori in $P$, indicando con $P_M$ la matrice degli autovettori scelti e con $\Lambda_w$ la matrice diagonale dei rispettivi autovalori.
6. **Calcolo della proiezione finale regolarizzata:** Si restituisce la matrice di proiezione ottima:
   $$\Psi = H P_M (\eta I + \Lambda_w)^{-1/2}$$
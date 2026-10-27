---
aliases:
  - PCA
  - Principal Component Analisy
tags:
  - Teoria
  - ML-optimization
  - dimensionality-reduction
cssclasses:
  - machine-learning
---
> [!abstract] PCA in breve
> La Principal Component Analysis (PCA) è una tecnica fondamentale di Machine Learning utilizzata per identificare pattern nei dati ad elevata dimensionalità, evidenziandone similitudini e differenze. L'obiettivo primario è effettuare un cambio di base (una rotazione) per trovare un sottoinsieme di feature in grado di rappresentare i dati originali massimizzando la varianza delle proiezioni e minimizzando l'errore di ricostruzione.
> <p align="center">   <img src="PCA.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>

## 1. Motivazione e Intuizione
Per comprendere la necessità della PCA, il problema della selezione delle feature cerca di rispondere a due domande chiave nell'ambito della *Discriminant Analysis*:
1. Quale insieme di feature fornisce la maggior discriminazione?
2. Qual è il modello che meglio separa i gruppi?

> [!example] L'Analogia della Molla Fisica
> Immagina di studiare il moto di una molla fisica ideale ($F=-kx$) usando tre telecamere (sensori in 3D).
> * **Il problema:** Non conosciamo a priori l'orientazione ottimale dei sensori né la dimensione minima per rappresentare il fenomeno, e inevitabilmente catturiamo del rumore di fondo.
> * **La soluzione:** Dobbiamo isolare i "dati significativi" agendo su tre fronti: **Rumore, Rotazione e Ridondanza** Il rumore (misurato col rapporto Segnale/Rumore $SNR$) deve essere inferiore ai dati significativi ($SNR >> 1$) per poter estrarre informazioni. Inoltre, è fondamentale eliminare le feature con alta ridondanza per comprimere le informazioni.

## 2. Formulazione Matematica della PCA
La PCA trasforma il problema intuitivo in un rigoroso problema di ottimizzazione matematica.
### A. La Proiezione
Sia $X \in \mathbb{R}^{M \times N}$ una matrice contenente $N$ vettori (dati) in uno spazio a $M$ dimensioni. Cerchiamo un vettore direzione $v \in \mathbb{R}^M$ (con norma unitaria $||v||=1$) su cui proiettare i dati.
La proiezione $p_k$ dell'$k$-esimo vettore $x_k$ su $v$ è:
$$ p_k = v^T x_k = \sum_{i=1}^M x_{ik} v_i $$

### B. Varianza delle Proiezioni e Matrice di Covarianza
Per applicare la PCA, il dataset deve avere media zero. Sottraiamo quindi la media $\mu_i$ da ogni dimensione: $\hat{x}_{ik} = x_{ik} - \mu_i$.
La varianza $\sigma^2$ delle proiezioni diventa quindi una funzione della matrice di covarianza $C$ dei dati centrati:
$$ \sigma^2 = \frac{1}{N} \sum_{k=1}^N (p_k - \bar{p})^2 = v^T C v $$
Dove la matrice di covarianza è $C = \frac{1}{N} \hat{X}\hat{X}^T$.

### C. Massimizzare la Varianza (Autovettori e Autovalori)
Il cuore della PCA è trovare il vettore $v$ che massimizza $\sigma^2$ sotto il vincolo $||v||=1$. Utilizzando i moltiplicatori di Lagrange, il problema si riduce all'equazione:
$$ Cv = \lambda v $$
Questo significa che i vettori ottimali $v$ sono gli **autovettori** della matrice di covarianza $C$, e la varianza massimizzata corrisponde ai rispettivi **autovalori** $\lambda$.

## 3. Applicazione: Proiezione e Compressione

Una volta calcolati gli autovalori e gli autovettori della matrice di covarianza, il processo operativo della PCA è il seguente:

1. **Ordinamento:** Gli autovalori (che esprimono la varianza massima) non sono tutti uguali; alcuni sono elevati, altri quasi nulli. Si ordinano gli autovettori in modo decrescente in base ai rispettivi autovalori.
2. **Selezione:** L'autovettore associato all'autovalore più grande è la *Componente Principale. Per comprimere i dati, selezioniamo solo le prime $k$ componenti (matrice ridotta $\dot{V}$) scartando quelle meno importanti.
3. **Riduzione della Dimensionalità:** I dati vengono proiettati nel nuovo spazio a dimensione ridotta calcolando i coefficienti delle componenti principali $P$:
   $$ P = \dot{V}^T \hat{X} $$

> [!warning] Errore di Ricostruzione
> La matrice $V$ agisce come trasformazione lineare. Se si utilizzassero tutti gli autovettori originari ($M$), i dati originali potrebbero essere ricostruiti perfettamente ($\hat{y} = \hat{x}$) senza alcun errore. Tuttavia, scartando alcuni autovettori per comprimere lo spazio (usandone solo $k$), si introduce un **errore di ricostruzione** $e$ pari alla somma delle componenti scartate:
> $$ e = \hat{x} - \hat{y} = \sum_{i=k+1}^M p_i v_i $$
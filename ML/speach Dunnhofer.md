---
cssclasses:
  - machine-learning
---
# Reverse Engenieering the Brain with AI

## Neuro Ai
Campo interdisciplinare che unisce **intelligenza artificiale** e **neuroscienze** per creare algoritmi ispirati al cervello e usare l'AI per studiare il sistema nervoso

## Core visual recognition
La capacità del cervello di **identificare rapidamente un oggetto nella parte centrale del campo visivo** (circa i 10 gradi centrali) in tempi brevissimi, intorno ai 200 millisecondi, corrispondenti alla durata di una singola fissazione oculare



IT inferior temporal cortex
## Neuro response
Viene fatto un campionamento sui primati con un dispositivo simile al neuralink. Viene fatta vedere una foto alla  cavia e vine campionato il numero di neuroni attivati in un tempo X. le regioni versi sono i momenti in cui il neurone si è attivato e l'intensità indica quanti si sono attivati in quel istante temporale. Praticamente viene fatto un encoder con usando la la cavia e poi si usa una Super Vector Machine per creare un decoder capace di passare da un tensore di neuroni attivi all'immagine iniziale.
<p align="center">   <img src="neuro-response-1.png" style="width: 450px; max-width: 100%; height: auto;" /> </p> <p align="center">   <img src="neuro-response-2.png" style="width: 450px; max-width: 100%; height: auto;" /> </p>

> [!NOTE] Domande
> 1) come si chiama esattamente questa pratica (quello dei neuroni e della SVM). 2
> 2) Ricapitolandoi; se è correttto e chiedere se ogni tendore è 0/1 o se è uno scalare che indica l'intensità dell'attivazione).

Il passo successivo è **sostituire la cavia con una rete neurale artificiale** per vedere se è in grado di simulare in modo sintetico il vettore di attivazione dei neuroni di output. Successivamente si usa una regressione lineare per predire l'outup "atteso" che avrebbe avuto il primate

<p align="center">   <img src="neuro-response-3.png" style="width: 450px; max-width: 100%; height: auto;" /> </p>
<p align="center">   <img src="neuro-response-4.png" style="width: 450px; max-width: 100%; height: auto;" /> </p>

> [!NOTE] Domande
> Ma quindo tutto questa parte {dati di input, ANN (_Artificial Neural Network_), syntetic neural responde, linear regression neural response} è tutto la parte di encoding del dato con il neural responde del primate come label? quindi poi andrebbe aggiunta la parte di deconding vista sopra?

---
Presentatore: Matteo Dunnhofer


dire che non ci avevo mai riflettuto su quanto siamo veloci. l'immagine dell'areo non l'ho vista. ho riconosciuto la sagoma da un dettaglio ed ho "quasi tirato ad indovinare".

[^1]: 

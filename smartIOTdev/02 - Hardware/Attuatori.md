---
cssclasses:
  - smart-iot
tags:
  - hardware
  - attuatori
---
> [!summary] Definizione Fondamentale
> Se il sensore esegue il passaggio *dal mondo fisico al mondo digitale*, l'**attuatore** compie il percorso inverso: converte un valore o un segnale digitale in un'**azione fisica tangibile** che altera lo stato del mondo reale.
> -- AGGIUNGERE LA FOTO DELLA SLIDE --

---

## Tassonomia 

### Tipo di Movimento Eseguito (Cinematica)
* **Movimento Lineare:** L'azione avviene lungo un unico asse rettilineo.
  * *Esempio:* Pistone lineare che spinge in fuori un cassetto all'avvicinamento dell'utente.
* **Movimento Rotativo / Angolare:** Il componente ruota intorno a un perno o asse centrale.
  * *Esempio:* Meccanismo per l'apertura automatica delle portiere delle auto; levetta/tappo rotante per il dosatore di cibo per animali.
* **Movimento Multi-Asse (Più gradi di libertà):** Sistemi complessi capaci di muoversi su 2, 3 o più assi coordinati.
  * *Esempio:* Bracci robotici industriali, teste cardaniche (gimbal).

### Livello di Potenza ed Energia Richiesta
La potenza assorbita dall'attuatore deve essere proporzionata allo sforzo meccanico e al carico da spostare:
* **Alta Potenza / Carico Pesante:** Attuatori dimensionati per vincere attriti e masse nell'ordine delle decine o centinaia di chili.
  * *Esempio:* Motore rotativo per aprire una portiera dell'auto (peso 30–100 kg), dove lo sforzo richiede correnti elevate e meccanismi robusti.
* **Bassa Potenza / Micro-Carico:** Movimentazione di masse trascurabili (pochi grammi).
  * *Esempio:* Servomotore per spostare un dischetto di plastica o cartone in un distributore di croccantini.

### Modalità di Controllo (Binario vs Continuo)
* **Attuatore Binario (On / Off):**
  * Possiede solo due stati discreti stabili: $0$ (chiuso/spento) o $1$ (aperto/acceso).
  * Non consente di modulare posizioni o flussi intermedi.
  * *Esempio tipico:* Elettrovalvola idraulica a solenoide per irrigazione (o fa passare l'acqua al 100% o la blocca completamente; non può parzializzare al 50%).
* **Attuatore Continuo (Modulante / Proporzionale):**
  * Consente di controllare con precisione l'entità dello spostamento o dello stato fisico su una scala continua.
  * *Esempi:* 
    * Attuatore rotativo posizionato ad angoli arbitrari ($5^\circ$, $10^\circ$, $47.2^\circ$).
    * Pistone lineare estratto a corsa variabile ($10\text{ cm}$ anziché $20\text{ cm}$).

### Tipologia di Energia e Principio Operativo
| Tipologia | Principio di Funzionamento | Esempi Tipici |
| :--- | :--- | :--- |
| **Meccanico** | Trasmissione di forze tramite leveraggi, viti senza fine, ingranaggi | Molle, bielle, azionamenti manuali/a vite |
| **Elettrico** | Trasformazione diretta dell'energia elettrica in segnale fisico | **LED** (energia elettrica $\to$ fotoni/luce) |
| **Elettromeccanico** | Conversione dell'energia elettromagnetica in forza o coppia motrice | **Motori passo-passo (stepper)**, servomotori DC, relè |
| **Pneumatico / Idraulico** | Sfruttamento della pressione di gas (aria compressa) o fluidi in pressione | Cilindri idraulici ad alta spinta, valvole pneumatiche per dosatori chimici |
| **Smart Materials** *(Nuove Tecnologie)* | Materiali intelligenti che mutano forma o stato se stimolati da energia termica, luminosa o IR | Micro-attuatori a memoria di forma per chirurgia mini-invasiva |

---

## Attuatori nel Contesto IoT (Caso d'Uso: Smart Farming)

In un impianto automatizzato, la scelta dell'attuatore risponde a vincoli specifici di sicurezza, costo e impatto ambientale:
1. **Elettrovalvola (Attuatore Binario / Elettromeccanico):** Apre o interrompe la mandata dell'acqua nelle condutture.
2. **Dosatore Pneumatico:** Rilascia la quantità esatta di fertilizzante liquido o fitofarmaco dalla bombola/lattina.
3. **Motori di Propulsione (Droni):** Distribuiscono chimici e pesticidi dall'alto coprendo ampie porzioni di terreno.
4. **Attuatori Meccanici per Serre:** Apertura/chiusura di finestre o teli ombreggianti per mitigare vento o eccesso di calore.

---

## Ruolo nel Ciclo Chiuso (Sense $\to$ Decide $\to$ Act)

```text
[ Sensore ]  --->  (Trasduzione ADC)  --->  [ Controller / Algoritmo ]
    ^                                                    |
    |                                          (Comando Digitale)
    |                                                    v
[ Mondo Fisico ] <--- (Azione Meccanica/Termica) <--- [ Attuatore ]
```

- L'attuatore non lavora isolato: **la sua azione modifica la grandezza fisica reale** (es. l'elettrovalvola aumenta l'umidità del suolo). 
- Tale modifica viene poi ==rilevata alla scansione successiva del sensore, permettendo al sistema di spegnere o modulare l'attuatore== (retroazione negativa).
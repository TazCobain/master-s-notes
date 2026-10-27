---
cssclasses:
  - smart-iot
tags:
  - hardware
  - sensori
---
> [!summary] In breve
> Un **sensore** è un elemento hardware che acquisisce parametri fisici traducendoli in segnali interpretabili; nell'architettura del [[Data management & compute stack]], presidia il livello base (**Edge**), fungendo da interfaccia diretta tra ambiente fisico e infrastruttura di calcolo.

> [!danger] DOMANDA TIPICA D'ESAME ORALE
> **Domanda del docente:** *"Avete un sensore analogico e volete collegarlo a un dispositivo con sole porte digitali (es. Raspberry Pi): come fate? Spiegatemi come funziona il processo."*
> 
> **Risposta sintetica:** È necessario interporre un convertitore **ADC (Analog-to-Digital Converter)** per eseguire una conversione analogico-digitale, che traduce un segnale fisico continuo in una rappresentazione numerica binaria discreta tramite due fasi obbligatorie: **campionamento** e **quantizzazione**.


---

## Conversione Analogico-Digitale (ADC)

### A. Campionamento (Sampling)
* **Definizione:** Discretizzazione lungo l'asse del **tempo**. Consiste nel campionare il valore reale del segnale a intervalli temporali definiti ($T_s$).
* **Frequenza di campionamento ($f_s$):** Poiché non è possibile effettuare infinite misurazioni al secondo, la frequenza di campionamento deve essere tarata in base alla dinamica del segnale. Per catturare correttamente le variazioni è necessario conoscere la frequenza massima del segnale (Teorema del campionamento).

> [!warning] Sottocampionamento
>   Se la frequenza è troppo bassa, il sistema non è sufficientemente rapido e si perdono le
>   oscillazioni troppo veloci del segnale (es. i picchi), alterando la percezione della misurazione.

### B. Quantizzazione (Quantization)
* **Definizione:** Discretizzazione lungo l'asse delle **ampiezze**. Traduce la misura continua campionata nel valore binario più vicino tra quelli disponibili.
* **Risoluzione ($n$ bit):** Definisce il numero di livelli discreti disponibili ($2^n$).
  * *Esempio (range 0–180°):* 
    * Con $1\text{ bit} \to 2^1 = 2$ livelli ($0^\circ$ o $180^\circ$).
    * Con $2\text{ bit} \to 2^2 = 4$ intervalli ($0^\circ, 45^\circ, 90^\circ, 135^\circ, 180^\circ$).
    * All'aumentare dei bit aumenta la risoluzione e cala l'approssimazione.
    
> [!warning]  Errori nella quantizzazione
  > Ogni approssimazione porta con se un errore nel campionamento (la differenza tra il valore reale e quello binario assegnato). 
  > L'errore massimo è pari alla *metà della differenza tra due step consecutivi* (metà dell'altezza del "gradino" della scala binaria): $$\text{Err}_{\max} = \frac{\Delta V}{2}$$
  >  Un numero di bit troppo basso porta a un segnale "a zig-zag" molto impreciso rispetto all'onda originale.
  
---

## Tassonomia dei Sensori

Classificazione strutturata su **5 assi operativi** + **1 asse fondamentale** (la grandezza fisica).

### Alimentazione (Attivo vs Passivo)
* **Attivo:** Richiede nativamente ==alimentazione elettrica continua== per effettuare la misura e trasmettere il dato (es. termometro digitale, microfono).
* **Passivo:** Non richiede alimentazione continua; si ==attiva solo quando sollecitato==/interrogato da un dispositivo esterno (es. tag RFID).

### Integrazione Ambientale (Invasivo vs Non Invasivo)
* **Invasivo:** ==Fisicamente inserito== all'interno dell'ambiente da monitorare (es. termostato montato a parete in stanza).
* **Non invasivo:** Rileva la grandezza operando dall'esterno dell'ambiente (es. termometro a infrarossi/rilevamento da remoto).

### Contatto Fisico (A contatto vs Non a contatto)
* **A contatto:** Deve toccare fisicamente la grandezza o l'oggetto da misurare (es. sensore di contatto per metalli, sonda di temperatura a immersione).
* **Non a contatto:** Misura senza toccare l'oggetto target (es. telecamera, fotoricevitore ottico, sensore PIR a infrarossi).

### Tipologia di Misura (Assoluta vs Relativa)
* **Assoluta:** Misura riferita a uno zero fisso globale (es. angolo di apertura porta: $0^\circ = \text{chiusa}$, $135^\circ = \text{aperta}$).
* **Relativa:** Misura lo scostamento (delta) rispetto allo stato dell'istante precedente (es. il sensore invia solo $+45^\circ$ o $-45^\circ$ e si resetta dopo ogni spostamento).

### Tecnologia Implementata
Principio fisico/chimico sfruttato per estrarre la grandezza:
* **Meccanica / Elettromeccanica**
* **Elettrica / Elettronica**
* **Ottica**
* **Chimica**
*(Nota: la stessa grandezza fisica, ad esempio l'apertura angolare, può essere rilevata con tecnologie diverse: potenziometro elettrico, encoder ottico, o switch meccanico).*

---

### Grandezza Fisica della Misurata
| Grandezza | Sensori Tipici |
| :--- | :--- |
| **Posizione / Distanza** | Potenziometro, inclinometro, sensore di prossimità |
| **Presenza vs Movimento** | Telecamera, radar, LiDAR (*presenza* rileva anche da fermo; *movimento* solo oggetti dinamici) |
| **Cinematica** | Accelerometro (accelerazione lineare), Giroscopio (velocità angolare) |
| **Forza / Pressione** | Cella di carico, sensore touch capacitivo/resistivo, barometro, piezometro |
| **Flusso / Fluidi** | Anemometro (vento/aria), flussimetro idraulico (portata/massa d'acqua) |
| **Umidità** | Igrometro (aria), Soil moisture sensor (terreno) |
| **Luce / Radiazione** | Fotodiodo, fotorilevatore IR, tubo Geiger-Müller |
| **Chimica / Biologia** | Sensori gas (CO₂, CO), particolato (PM2.5, PM10), pH-metro, biosensori (glucosio, SpO₂) |

---

## Il Ciclo di Controllo IoT (Feedback Loop)

I sensori e gli attuatori operano all'interno di un loop continuo a tre fasi:

$$\text{Sensing (Sensore)} \longrightarrow \text{Decisione (Elaborazione Digitale)} \longrightarrow \text{Azione (Attuatore)}$$

* **Esempio smart farming:**
  1. *Sensing:* L'igrometro misura l'umidità del suolo ($X\%$).
  2. *Decisione:* Se $X < 50\%$, il controller invia un comando all'attuatore.
  3. *Azione:* L'elettrovalvola si apre e irriga il terreno, modificando lo stato fisico reale e chiudendo il ciclo alla misurazione successiva.
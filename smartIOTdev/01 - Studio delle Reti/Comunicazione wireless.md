---
cssclasses:
  - smart-iot
tags:
  - network-infrastructure
---
> [!abstract] In sinstesi
> La comunicazione wireless si basa sul propagare "onde invisibili" nell'etere, si usano le antenne per leggere e propagare / propagare le onde e ci sono limiti di sicurezza per evitare che onde troppo forti (e dannose) vengano propagate in modo indiscriminato.
> - **Come definisco un'onda?**  Con frequenza, ampiezza, periodo/lunghezza.
> - **Modulazione:** Tecniche per codificare l'informazione su un'onda portante alterandone l'ampiezza (AM), la frequenza (FM) o la fase (PM).
> - **Spread Spectrum:** Metodi di espansione dello spettro (FHSS, DSSS, CSS) per garantire resistenza alle interferenze, sicurezza e accesso multiplo.
## Cos'è un Segnale e Come si Propaga

Nelle comunicazioni wireless, l'informazione viene trasmessa sotto forma di **onde elettromagnetiche**: perturbazioni oscillatorie di campi elettrici e magnetici che si propagano nello spazio (anche nel vuoto, a differenza delle onde acustiche del parlato che necessitano di un mezzo materiale).
<p align="center">   <img src="waveChart.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>
Un'onda periodica può essere descritta analizzando lo stesso fenomeno da due prospettive complementari: **nello spazio** e **nel tempo**.

### Dominio dello Spazio vs Dominio del Tempo

* **Dominio dello spazio (fotografia istantanea):** misurando la distanza fisica tra due picchi (creste) consecutivi si ottiene la **lunghezza d'onda** ($\lambda$), espressa in metri ($m$).
* **Dominio del tempo (osservazione in un punto fisso):** misurando l'intervallo temporale che intercorre tra il passaggio di due picchi successivi si ottiene il **periodo** ($T$), espresso in secondi ($s$).

---

### Parametri Fondamentali del Segnale

> [!NOTE] Relazione Spazio-Tempo
> Frequenza e lunghezza d'onda sono legate dalla velocità di propagazione nel mezzo (nel vuoto pari alla velocità della luce $c \approx 3 \times 10^8 \text{ m/s}$):
> $$c = \lambda \cdot f$$

* **Frequenza ($f$):** rappresenta il numero di cicli o oscillazioni complete compiute in un secondo. Si misura in **Hertz (Hz)** ed è legata al periodo dalla relazione:
  $$f = \frac{1}{T}$$
* **Ampiezza ($A$):** indica lo scostamento massimo del segnale rispetto al suo valore di riposo (livello neutro). Questa misura quantifica l'intensità del segnale e non varia sia che il segnale venga rappresentato rispetto al tempo, sia rispetto alla distanza spaziale.

## Conversione del Segnale: Il Ruolo dell'Antenna

L'**antenna** funge da **trasduttore**: converte un segnale elettrico guidato (tensione/corrente alternata che viaggia su un circuito o cavo) in un'onda elettromagnetica che si irradia nello spazio libero (e viceversa in ricezione).
> [!note] Principio Fisico
> L'antenna non vibra meccanicamente. A oscillare sono gli **elettroni** all'interno del conduttore metallico, spinti dalla corrente alternata sinusoidale fornita dal trasmettitore.

#### Come avviene l'irradiazione
1. **Oscillazione delle cariche:** la corrente alternata fa muovere avanti e indietro le cariche elettriche lungo l'antenna, sottoponendole a continua **accelerazione e decelerazione**.
2. **Generazione dei campi:**
   * La separazione periodica di carica positiva e negativa crea un **campo elettrico ($\vec{E}$)** variabile.
   * Il moto delle cariche (corrente) genera un **campo magnetico ($\vec{B}$)** variabile perpendicolare al primo.
3. **Distacco dell'onda:** secondo le leggi dell'elettromagnetismo (Equazioni di Maxwell), un campo elettrico che varia nel tempo genera un campo magnetico, e un campo magnetico variabile genera un campo elettrico. A frequenze sufficientemente elevate, questa concatenazione si "stacca" dalla superficie dell'antenna e si propaga autonomamente nello spazio sotto forma di **onda elettromagnetica piana**.

> [!TIP] Reciprocità dell'Antenna
> Il processo è perfettamente simmetrico: in **ricezione**, l'onda elettromagnetica incidente investe l'antenna ricevente, inducendo nei suoi conduttori un minuscolo movimento di elettroni (una micro-corrente alternata) che viene poi amplificata e decodificata dal ricevitore.

## La Modulazione del Segnale

Per trasmettere un'informazione tramite onde radio, non si usa il fenomeno dell'interferenza (che nelle telecomunicazioni indica un disturbo indesiderato), ma il processo di **modulazione**.

> [!INFO] Principio di Base
> Un'onda sinusoidale pura a frequenza fissa non trasporta alcuna informazione utile di per sé, poiché è perfettamente prevedibile. Per veicolare dati, occorre variarne in modo controllato una o più caratteristiche fondamentali.

L'operazione coinvolge due componenti principali:

1. **Onda Portante (*Carrier wave*):** un'onda periodica continua ad alta frequenza che fa da "veicolo" fisico per viaggiare nel mezzo trasmissivo (canale wireless).
2. **Segnale Modulante (Messaggio):** l'informazione vera e propria che si vuole trasmettere (voce, flusso di bit `0` e `1`, dati video).

Il modulatore varia una caratteristica della portante in funzione del messaggio, generando l'**onda modulata** finale che incorpora l'informazione:

* **Modulazione di Ampiezza (AM / ASK):** il valore di picco della portante varia in proporzione al messaggio.
* **Modulazione di Frequenza (FM / FSK):** la rapidità delle oscillazioni della portante aumenta o diminuisce a seconda dei dati.
* **Modulazione di Fase (PM / PSK):** si introduce uno sfasamento istantaneo dell'onda per codificare i valori trasmessi.
Se voglio trasmettere un'informazione tramite un'onda posso ==modularla creando delle interferenze sul mezzo==. la somma dell'interferenza conj il pattern ricorrente dell'onda porta a creare un'onda caratteristica che incorpora il messaggio al suo interno.
<p align="center">   <img src="typeOfWave.png" style="background-color: white; padding: 10px; border-radius: 6px; width: 450px; max-width: 100%; height: auto;" /> </p>
## Spread Spectrum (Spettro Espanso)
Tecnica di trasmissione radio in cui il ==segnale informativo non viene inviato su una singola frequenza a banda stretta== (*narrowband*), ==ma distribuito== (*espanso*) ==su un intervallo di frequenze== notevolmente più ampio (*wideband*).
### Tecniche Principali
- **FHSS** (*Frequency-Hopping Spread Spectrum*): commuta rapidamente la frequenza di trasmissione a intervalli minimi, secondo una sequenza pseudo-casuale condivisa tra trasmettitore e ricevitore.
- **DSSS** (*Direct-Sequence Spread Spectrum*): combina il segnale dati con una sequenza pseudo-casuale a frequenza più alta, distribuendo direttamente l'energia su tutta la banda.
- **CSS** (*Chirp Spread Spectrum*): sfrutta impulsi a frequenza variabile nel tempo (*chirp*); impiegato a livello fisico nelle tecnologie LPWA (es. [[LoRaWAN]]).
### Vantaggi Chiave
- **Immunità alle interferenze**: riduce drasticamente l'impatto dei disturbi a banda stretta.
- **Bassa intercettabilità (*anti-eavesdropping*)**: la modulazione pseudo-casuale rende il segnale simile a rumore di fondo per ricevitori non sincronizzati.
- **Mitigazione del *multipath fading***: compensa i ritardi e le attenuazioni dovuti a riflessioni multiple del segnale.
- **Accesso multiplo (CDMA)**: consente a più nodi di trasmettere contemporaneamente sulla stessa porzione di spettro.
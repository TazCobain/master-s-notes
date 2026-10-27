---
cssclasses:
  - smart-iot
aliases:
  - CSMA/CA
---
Protocollo MAC a contesa usato nelle [[Comunicazione wireless]] (es: **[[IEEE 802.11ah (Wi-Fi HaLow)|WI-FI HaLow]]**). Opera al Livello 2 (Data Link) dello stack [[.

> [!tip] Perché Avoidance e non Detection (CSMA/CD)?
> Nelle reti wireless le radio operano in **half-duplex** e il segnale trasmesso sovrasta quello ricevuto: rilevare collisioni in tempo reale è impossibile, quindi il protocollo mira a **prevenirle**. Risolve inoltre il problema del **nodo nascosto** (nodi fuori portata tra loro che collidono sullo stesso Access Point).

---

## Come Funziona

1. **Carrier Sensing:**
   - **Fisico (CCA):** La radio ascolta se il canale radio è occupato.
   - **Virtuale (NAV):** I pacchetti dichiarano la durata della trasmissione; le altre stazioni impostano un timer interno (**NAV**) e attendono che arrivi a zero.
2. **Spazi di attesa (IFS):**
   - **DIFS:** Tempo obbligatorio di canale libero prima di poter tentare l'invio.
   - **SIFS:** Tempo di attesa minimo riservato alle risposte prioritarie (es. ACK).
3. **Random Backoff:** Se il canale è occupato, il nodo sceglie un tempo casuale di attesa prima di trasmettere. Il timer scorre solo a canale libero; se si verificano collisioni, la finestra di attesa raddoppia (*Exponential Backoff*).
4. **Conferma (ACK):** La corretta ricezione è confermata solo se il destinatario invia un frame ACK entro il timeout.

---

## Meccanismo RTS/CTS (Opzionale)

Usato per frame grandi per azzerare il problema dei nodi nascosti:
1. Il mittente invia un **RTS** (*Request to Send*).
2. Il ricevitore risponde con un **CTS** (*Clear to Send*) che zittisce tutti i nodi circostanti impostando il loro NAV.
3. Il mittente trasmette i dati e attende l'**ACK**.
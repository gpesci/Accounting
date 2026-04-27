# Skill: Fatturazione

Questa skill guida GitHub Copilot nelle attività operative legate alla fatturazione: archiviazione, nomenclatura, aggiornamento degli statement e redazione delle mail di invio.

---

## 1. Archiviazione e nomenclatura delle fatture

### Struttura cartelle

```
/Fatturazione attiva/
  Fatture Attive PDF/
    YYYY/
      MM/
/Fatturazione passiva/
    YYYY/
      MM/
```

### Convenzione di nomenclatura

**Fatture Passive:**
```
YYYY-MM-DD_<Fornitore>_<NumeroFattura>.<ext>
```

**Fatture Attive:**
```
<NumeroFattura>_<Nome Cliente>
```

**Esempi:**
- `123_ClienteABC.pdf`   → Fattura Attiva
- `2026-04-20_FornitoreXYZ_INV-0891.pdf`  → Fattura Passiva


### Regole di archiviazione

- Archivia sempre nella sottocartella dell'anno e mese di **emissione**.
- Il nome del cliente/fornitore non deve contenere spazi: usa il CamelCase o i trattini (es. `Cliente-ABC`).
- Conserva sempre la versione originale del file; eventuali annotazioni vanno su una copia.

---

## 2. Aggiornamento dello statement per cliente

Lo **statement** è il documento riepilogativo che mostra per ogni cliente le fatture emesse, gli importi, le scadenze e lo stato dei pagamenti.

### Formato del file statement

Il file di riferimento è `/report/statement_clienti.xlsx` (o `.csv`) con le seguenti colonne:

| Colonna | Descrizione |
|---|---|
| `cliente` | Nome o ragione sociale del cliente |
| `numero_fattura` | Numero univoco della fattura |
| `data_emissione` | Data di emissione (formato `YYYY-MM-DD`) |
| `data_scadenza` | Data di scadenza del pagamento |
| `importo_netto` | Importo imponibile in EUR |
| `iva` | Percentuale IVA applicata |
| `importo_totale` | Totale fattura (netto + IVA) |
| `stato_pagamento` | `attesa` / `parziale` / `pagato` / `scaduto` |
| `data_pagamento` | Data di ricezione del pagamento (se avvenuto) |
| `note` | Eventuali note aggiuntive |

### Regole di aggiornamento

- Inserisci ogni nuova fattura emessa entro il giorno di emissione.
- Aggiorna `stato_pagamento` e `data_pagamento` appena il pagamento è confermato.
- Le fatture con `data_scadenza` superata e `stato_pagamento` non `pagato` devono essere marcate `scaduto`.
- Ordina le righe per `data_emissione` discendente.

---

## 3. Mail di invio fattura

### Struttura della mail

```
Oggetto: iSolutions' invoice <NumeroFattura> – <NomeCliente> 

Dear Customer,

find attached the invoice no. <NumeroFattura> for the month of <MeseEmissione>, due on <DataScadenza>.

We would also to take this opportunity to share with you the statement of issued invoices.
According to our records these are the invoices still outstanding:
•	<NumeroFatturaScaduta>
..

For any further information, please do not hesitate to contact us.

Best regards,


```

### Variabili da sostituire

| Segnaposto | Fonte |
|---|---|
| `<NumeroFattura>` | Campo `numero_fattura` dello statement |
| `<NomeAzienda>` | Ragione sociale mittente |
| `<MeseEmissione>` | Mese e anno di emissione (es. `April 2026`) | |
| `<DataScadenza>` | Campo `data_scadenza` (formato `DD/MM/YYYY`) |
| `<NumeroFatturaScaduta>` | Campo `numero_fattura` dello statement per ogni riga che presenta lo stato 'scaduto'|


### Regole per la mail

- Allega sempre il PDF della fattura nella versione definitiva.
- Usa sempre la formula di cortesia `Dear Customer'.
- Se la fattura sostituisce una nota di credito, menzionarlo esplicitamente nel corpo.
- Invia in CC il responsabile amministrativo interno.

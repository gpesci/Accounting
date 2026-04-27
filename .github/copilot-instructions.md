# Copilot Instructions — Accounting

## Contesto del progetto
Questo repository gestisce le attività amministrative e contabili dell'organizzazione. Include documenti, script e automazioni relativi a fatturazione, budget, contratti e reportistica finanziaria.

## Linee guida generali

- Usa l'italiano per commenti, messaggi di commit e documentazione interna.
- Mantieni la struttura delle cartelle ordinata e coerente con le categorie definite.
- Non committare mai dati sensibili (credenziali, dati personali, informazioni bancarie).

## Struttura del repository

```
/fatture/        → Fatture emesse e ricevute
/contratti/      → Contratti attivi e archiviati
/budget/         → Piani di budget annuali e mensili
/report/         → Report finanziari e riepiloghi periodici
/script/         → Automazioni e script di supporto
```

## Convenzioni per i file

- Nomenclatura: `YYYY-MM_descrizione.ext` (es. `2026-04_fattura-fornitore-X.pdf`)
- I file di testo e configurazione devono essere in formato UTF-8.
- I fogli di calcolo devono essere in formato `.xlsx` o `.csv`.

## Automazioni e script

- Gli script devono essere documentati con un commento iniziale che descriva scopo, input e output.
- Preferire Python o PowerShell per le automazioni.
- Ogni script deve gestire gli errori in modo esplicito e loggare le operazioni principali.

## Issue e task

- Usa le **Issues** per tracciare scadenze fiscali, attività pendenti e revisioni.
- Etichette suggerite: `fatturazione`, `scadenza`, `contratto`, `revisione`, `urgente`.

## Sicurezza e privacy

- Non caricare documenti contenenti dati personali non anonimizzati.
- I file con dati sensibili devono essere cifrati o esclusi tramite `.gitignore`.

# Presentazione Database Versioning
Questo è un progetto in stile doc-as-code per la creazione della presentazione sul Database Versioning. 
La presentazione è stata creata attraverso lo strumento [Slidev](https://github.com/slidevjs/slidev).

Questa presentazione sul Database Versioning illustra i benefici, gli strumenti comuni e le best practices per gestire 
le versioni delle strutture e dei dati di un database.

Questa presentazione vuole essere l'introduzione a un argomento conteso tra più aree di competenza e fondamentale 
per la gestione di un database in un contesto di sviluppo software di tipo collaborativo (o di social coding).

## Quick Start
Se non volete installare nulla, potete vedere la presentazione direttamente su
1. [GitHub Pages](https://amusarra.github.io/database-versioning-slide)
2. Netlify su [database-versioning-slide](https://database-versioning.dontesta.it/)

Per chi di voi volesse installare la presentazione in locale, seguite questi passaggi:

```bash
# Installazione o verifica di Node.js >= 18
node -v

# Clonare il repository
git clone https://github.com/amusarra/database-versioning-slide.git

# Entrare nella cartella
cd database-versioning-slide

# Installare le dipendenze
npm install

# Avviare la presentazione in modalità sviluppo
npm run dev
```
Console 1 - Installazione e avvio della presentazione in locale

Una volta avviata la presentazione con il comando `npm run dev`, vi sarà aperto automaticamente il browser mostrando la
presentazione in modalità sviluppo/presentazione.

Per i più curiosi, la pubblicazione della presentazione su GitHub Pages è automatizzata attraverso la GitHub Action
definita nel file `.deploy_gh_pages.yml`. Su Netlify, invece, il processo di build e pubblicazione è automatizzato
attraverso la CI/CD di Netlify che usa il file `netlify.toml` come elemento di configurazione.

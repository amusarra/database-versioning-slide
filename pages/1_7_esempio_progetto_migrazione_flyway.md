---
layout: default
---

# Esempio di progetto di migrazione con Flyway 1/8

Brevemente vedremo com'è strutturato un classico progetto di migrazione del database usando **Flyway** e come gestire le migrazioni attraverso la CLI (Command Line Interface) messa a disposizione. La versione di riferimento è la OSS Edition v10.13.0

<span v-click>Un progetto standard (standalone) in genere include: script di migrazione, configurazione di Flyway e uno script di esecuzione.</span>

<v-clicks>

```shell {lineNumbers: false}
.
├── flyway.toml
├── migrate.sh
└── sql
    ├── V1.0.0__create_users_table.sql
    ├── V1.1.0__add_email_to_users.sql
    ├── V2.0.0__create_orders_table.sql
    └── V2.0.1__add_foreign_key_to_orders.sql
```

</v-clicks>

<br>

<v-clicks>

- **flyway.toml**: contiene le configurazioni di Flyway (comprese le informazioni di connessioni dal database)
- **migrate.sh**: script shell che esegue la migrazione

È quindi richiesto avere Flyway installato sulla propria macchina o sulla quella dedicata all'esecuzione dello script. 
Puoi scaricarlo dal sito ufficiale di Flyway [qui](https://documentation.red-gate.com/fd/command-line-184127404.html).

</v-clicks>

---
level: 2
---

# Esempio di progetto di migrazione con Flyway 2/8

Configurazione di Flyway tramite il file di properties `flayway.toml` ed esecuzione della migrazione attraverso lo 
script shell `migrate.sh`

<v-clicks>

```toml
# More information on the parameters can be found
# here: https://documentation.red-gate.com/flyway/flyway-cli-and-api/configuration/parameters

[environments.default]
url = "jdbc:postgresql://localhost:5432/migration_db"
user = "migration_user"
password = "migration_password"

[flyway]
locations = ["filesystem:sql"]
```

</v-clicks>

<br>

<v-clicks>

Il file di configurazione è in formato [TOML - Tom's Obvious, Minimal Language](https://toml.io/en/) e sostituisce
il formato tradizionale (legacy) conf (properties format). Per maggiori consultare la guida [TOML Configuration](https://documentation.red-gate.com/fd/flyway-cli-and-api/configuration/toml-configuration-file/).

</v-clicks>


---
level: 2
---

# Esempio di progetto di migrazione con Flyway 3/8

<v-clicks>

```shell
#!/usr/bin/env bash

# Assicurati che Flyway sia installato e che il comando `flyway` sia disponibile nel PATH
# Puoi installare Flyway seguendo le istruzioni 
# qui: https://documentation.red-gate.com/fd/command-line-184127404.html

# Esegui la migrazione
flyway migrate

# Visualizza lo stato delle migrazioni
flyway info
```

</v-clicks>

<br>

<v-clicks>

Il comando di migrazione di Flyway (`flyway migrate`) è uno degli strumenti principali utilizzati per applicare le modifiche al database, mentre il comando `flyway info` visualizza le informazioni circa lo stato delle migrazioni.

Nelle successive slide vedremo una spiegazione breve e dettagliata di come funziona il processo di migrazione, che in genere i vari tool gestiscono alla stesso modo.

</v-clicks>


---
level: 2
---

# Esempio di progetto di migrazione con Flyway 4/8

Sotto il cofano, l'esecuzione del comando `flyway migrate` esegue le seguenti attività.

<v-clicks depth="2">

1. **Configurazione**
   - Flyway legge la configurazione da `flyway.toml`, `flyway.conf` o dalle variabili d'ambiente. Queste configurazioni includono le informazioni di connessione al database, la posizione degli script di migrazione, e altre impostazioni.
2. **Connessione al Database**
   - Flyway si connette al database specificato usando le credenziali fornite nella configurazione.
3. **Verifica della Tabella di Metadati**
   - Flyway verifica l'esistenza di una tabella di metadati (di solito chiamata `flyway_schema_history`) nel database. Questa tabella tiene traccia delle migrazioni che sono state già applicate al database. 
4. **Ricerca delle Migrazioni**
   - Flyway cerca gli script di migrazione nelle posizioni specificate (come filesystem:sql). Gli script devono seguire una convenzione di denominazione specifica (es., V1__init.sql, V2__add_email_to_users.sql). 

</v-clicks>

---
level: 2
---

# Esempio di progetto di migrazione con Flyway 5/8

<v-clicks depth="3">

5. **Ordinamento delle Migrazioni**
    - Flyway ordina gli script di migrazione in base alla loro versione. Le versioni devono essere univoche e incrementali.
6. **Verifica degli Stati delle Migrazioni**
    - Flyway confronta le migrazioni trovate con quelle registrate nella tabella di metadati. Se ci sono nuove migrazioni che non sono state ancora applicate, Flyway le identifica.
7. **Applicazione delle Migrazioni**
    - Flyway applica le nuove migrazioni in ordine sequenziale. Per ogni migrazione:
      1. Esegue il codice SQL nello script.
      2. Aggiorna la tabella di metadati per registrare che la migrazione è stata applicata correttamente.
      3. Se una migrazione fallisce, Flyway interrompe il processo e segnala l'errore.
8. **Conferma dello Stato Finale**
    - Dopo aver applicato tutte le migrazioni, Flyway aggiorna la tabella di metadati e fornisce un riepilogo delle migrazioni applicate, quelle in sospeso, e qualsiasi errore che potrebbe essersi verificato.

</v-clicks>

---
level: 2
---

# Esempio di progetto di migrazione con Flyway 6/8

Quelli a seguire sono gli script SQL di migrazione che rappresentano rispettivamente le versioni del database: 1.0.0, 1.1.0, 2.0.0 e 2.0.1.

<v-clicks>

```sql
-- Code 1 - Script di migrazione V1.0.0__create_users_table.sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(50) NOT NULL
);
```

</v-clicks>

<v-clicks>

```sql
-- Code 2 - Script di migrazione V1.1.0__add_email_to_users.sql
ALTER TABLE users ADD COLUMN email VARCHAR(100);
```

</v-clicks>

<v-clicks>

```sql
-- Code 3 - Script di migrazione V2.0.0__create_orders_table.sql
CREATE TABLE orders (
    id SERIAL PRIMARY KEY,
    user_id INT NOT NULL,
    order_date TIMESTAMP NOT NULL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

</v-clicks>

<v-clicks>

```sql
-- Code 4 - Script di migrazione V2.0.1__add_foreign_key_to_orders.sql
ALTER TABLE orders ADD CONSTRAINT fk_user
FOREIGN KEY (user_id) REFERENCES users(id);
```

</v-clicks>

---
level: 2
---

# Esempio di progetto di migrazione con Flyway 7/8

Prima di eseguire il processo di migrazione, proviamo a vedere lo stato attuale del database eseguendo il comando `flyway info`.

<v-clicks>

```console {lineNumers: false}
Flyway OSS Edition 10.13.0 by Redgate

See release notes here: https://rd.gt/416ObMi
Database: jdbc:postgresql://localhost:5432/migration_db (PostgreSQL 16.3)
Schema history table "public"."flyway_schema_history" does not exist yet
Schema version: << Empty Schema >>

+-----------+---------+---------------------------+------+--------------+---------+----------+
| Category  | Version | Description               | Type | Installed On | State   | Undoable |
+-----------+---------+---------------------------+------+--------------+---------+----------+
| Versioned | 1.0.0   | create users table        | SQL  |              | Pending | No       |
| Versioned | 1.1.0   | add email to users        | SQL  |              | Pending | No       |
| Versioned | 2.0.0   | create orders table       | SQL  |              | Pending | No       |
| Versioned | 2.0.1   | add foreign key to orders | SQL  |              | Pending | No       |
+-----------+---------+---------------------------+------+--------------+---------+----------+
```

</v-clicks>

<v-clicks>

L'output mostrato è quello atteso, dato che il database è praticamente _"nuovo"_, ovvero, non ha ancora subito nessun processo di migrazione.

</v-clicks>

---
level: 2
---

<style scoped>
.centered-image {
  display: flex;
  justify-content: center;
  align-items: center;
}

</style>

# Esempio di progetto di migrazione con Flyway 8/8

A seguire un video che mostra l'esecuzione di una serie di migrazioni partendo da zero. Il video è accelerato 5 volte per questioni di tempo. Qui https://asciinema.org/a/660361 puoi trovare il video completo.

<div class="centered-image">
<img v-click width="70%" height="70%" src="/images/asciinema/demo_esecuzione_prima_migrazione_full_5x.gif" alt="Esecuzione della prima migrazione del database"/>
</div>


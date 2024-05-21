---
layout: default
---

# Esempio di script di migrazione

<v-clicks  depth="2">

- Script SQL (esempio Flyway)
  - Versione 1.0.0: Crea la tabella users con campi id, username e email.
  - Versione 1.1.0: Aggiunge il campo last_login alla tabella users.

<br>

```sql
-- Versione 1.0.0
CREATE TABLE users (
    id INT PRIMARY KEY,
    username VARCHAR(50) NOT NULL,
    email VARCHAR(100) NOT NULL
);

-- Versione 1.1.0
ALTER TABLE users ADD COLUMN last_login TIMESTAMP;
```

</v-clicks>

<br>

<v-clicks>

  Per eseguire la migrazione è sufficiente eseguire il comando `flyway migrate` nella directory contenente gli script di migrazione.

</v-clicks>
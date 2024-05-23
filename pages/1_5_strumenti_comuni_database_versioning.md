---
layout: default
---

# Strumenti comuni per il database versioning

<v-clicks depth="2">

- **Flyway**
  - Uno strumento di migrazione del database open-source che utilizza script SQL o Java per definire le migrazioni. È noto per la sua semplicità e facilità di integrazione con i processi CI/CD.
- **Liquibase**
  - Un altro strumento di migrazione del database open-source che supporta una varietà di formati di definizione delle migrazioni, tra cui SQL, XML, YAML e JSON. È potente e flessibile, con una buona integrazione con gli strumenti DevOps.
- **Alembic**
  - Uno strumento per la gestione delle migrazioni del database, spesso utilizzato con SQLAlchemy in progetti Python. Fornisce un framework per la creazione, l'applicazione e la gestione delle migrazioni del database.

</v-clicks>

<!--
Esistono diversi strumenti a supporto delle attività di versioning del database; qui mostrerò quelli più comuni per l'ambienti Java e Python.
Flyway e Liquibase sono integrati con i framework Java cloud-native più conosciuti come Spring Boot e Quarkus.
-->

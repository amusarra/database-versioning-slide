---
layout: default
---

# Componenti chiave del database versioning

<v-clicks depth="2">

- **Controllo delle versioni degli schemi**
  - Gestione delle versioni degli schemi di database, che include tabelle, indici, viste, procedure, trigger, e altri oggetti di database. Ogni modifica a questi oggetti viene tracciata e documentata.
- **Migrazioni del database**
  - È uno script che apporta una modifica specifica allo schema del database, come l'aggiunta di una nuova tabella, la modifica di una colonna, o l'eliminazione di un indice. Le migrazioni possono essere applicate in sequenza per aggiornare lo schema del database da una versione precedente a una nuova versione.
- **Rollback**
  - La capacità di annullare una migrazione, tornando a una versione precedente dello schema. Questo è utile per gestire errori o modifiche non desiderate.
- **Script di seed e fixture**
  - Script utilizzati per popolare il database con dati iniziali o di esempio, necessari per testare l'applicazione (vedi integration test).

</v-clicks>

<!--
Per la documentazione è preferibile usare l'approccio doc-as-code di cui recentemente ho fatto un post sul gruppo Ready2Learn di Viva Engage o Yammer.
-->

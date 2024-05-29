---
layout: default
---

# La sicurezza delle Migrazioni 1/3

Per migliorare la sicurezza quando si utilizzano strumenti di <span v-mark.red="1">Database Migration</span> <span v-click>**senza concedere privilegi di livello DBA agli utenti delle applicazioni**, si possono adottare diverse strategie.</span> 

<v-clicks depth="2">

- **Account separati per le migrazioni**
  - Utilizza un account separato con privilegi elevati esclusivamente per le migrazioni. Questo account dovrebbe essere utilizzato solo durante il processo di deployment o aggiornamento del database e non essere accessibile all'applicazione stessa.
- **Utilizzo di un servizio intermedio**
    - Implementa un servizio intermedio o un job runner che ha i privilegi necessari per eseguire le migrazioni. L'applicazione comunica con questo servizio quando è necessario eseguire una migrazione. Questo permette di mantenere i privilegi elevati isolati dall'applicazione.
- **Gestione delle migrazioni tramite CI/CD**
    - Integra le migrazioni del database nella pipeline di Continuous Integration/Continuous Deployment (CI/CD). I sistemi CI/CD possono essere configurati con credenziali di amministratore del database, riducendo la necessità per gli utenti applicativi di avere tali privilegi.

</v-clicks>

<!--
Per la seconda strategia "Utilizzo di un servizio intermedio", è possibile utilizzare tre possibili pattern k8s (Kubernetes) che sono:
1. Job
2. Init Container
3. Operator

Nel caso in cui la propria applicazione sia sviluppata tramite il framework Java Quarkus, questo, prevede OOTB dei pattern per assolvere nel modo ottimale all'esecuzione dei task di migrazione.
-->

---
level: 2
---

# La sicurezza delle Migrazioni 2/3

<v-clicks depth="2">

- **Ruoli con privilegi limitati**
    - Configura ruoli specifici con i minimi privilegi necessari per eseguire migrazioni. Per esempio, puoi creare un ruolo che ha solo i permessi per modificare schemi specifici o eseguire particolari comandi DDL (Data Definition Language).
- **Migrazioni supervisionate**
    - Esegui migrazioni manualmente o semi-automaticamente sotto la supervisione di un DBA. Questo approccio è più sicuro ma può essere meno pratico per ambienti con frequenti rilasci.
- **Sandbox per test e approvazione**
    - Prima di eseguire migrazioni sul database di produzione, esegui tutte le migrazioni in un ambiente di sandbox o staging. Questo ambiente può essere una copia del database di produzione dove è possibile testare le migrazioni senza rischi. Una volta verificate, le migrazioni possono essere applicate in produzione da un DBA.

</v-clicks>

---
level: 2
---

# La sicurezza delle Migrazioni 3/3

<v-clicks depth="2">

- **Logging e auditing**
  - Abilita il logging e l'auditing delle migrazioni per tracciare quali modifiche sono state fatte, quando e da chi. Questo non solo migliora la sicurezza, ma aiuta anche nella diagnosi di eventuali problemi.
- **Gestione delle chiavi di accesso**
  - Usa strumenti di gestione delle chiavi di accesso come HashiCorp Vault, AWS Secrets Manager o Azure Key Vault per gestire e distribuire le credenziali di accesso verso i database in modo sicuro.
</v-clicks>

<br>
<br>

<div v-click>

  Implementando queste strategie, è possibile ridurre significativamente il rischio associato alla concessione di privilegi elevati agli utenti delle applicazioni durante le migrazioni del database, mantenendo al contempo un flusso di lavoro efficiente per la gestione delle migrazioni stesse.

</div>

<!--
Immagino che tutti sappiate che le secret standard di k8s non sono realmente sicure in quanto sfrutta l'encode in base64 per i valori memorizzato al suo interno, motivo per noi non ho fatto menzione.
-->

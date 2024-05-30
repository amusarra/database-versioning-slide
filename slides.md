---
# theme id or package name
# Learn more: https://sli.dev/themes/use.html
theme: seriph
layout: cover
background: '/images/cover/database_versioning_cover_1-min.png'
# Metadata for the slides
info: |
  ## Database Versioning
  Presentazione sul database versioning che illustra i benefici, gli strumenti comuni e le best practices per gestire le versioni delle strutture e dei dati di un database.

  Autore: Antonio Musarra

  Tag: v1.0.1

author: Antonio Musarra
keywords: database,sql,versioning,devops,flyway,liquibase,alembic,sqlalchemy,python,java
title: Database Versioning
favicon: /images/favicon.jpeg

# Define the transitions between slides
transition: slide-left

# syntax highlighter, can be 'prism', 'shiki'
highlighter: shiki

# fonts will be auto imported from Google fonts
# Learn more: https://sli.dev/custom/fonts
fonts:
  sans: Open Sans
  serif: Cambria
  mono: Hack
  provider: none

# Enable or disable the Markdown Components feature
mdc: true

# enable twoslash, can be boolean, 'dev' or 'build'
twoslash: true

# show line numbers in code blocks
lineNumbers: true

# enable monaco editor, can be boolean, 'dev' or 'build'
monaco: true

# Where to load monaco types from, can be 'cdn', 'local' or 'none'
monacoTypesSource: local

# force color schema for the slides, can be 'auto', 'light', or 'dark'
colorSchema: auto

# router mode for vue-router, can be "history" or "hash"
routerMode: history

# aspect ratio for the slides
aspectRatio: 16/9

# real width of the canvas, unit in px
canvasWidth: 980

# drawing options
# Learn more: https://sli.dev/guide/drawing.html
drawings:
  enabled: true
  persist: false
  presenterOnly: false
  syncAll: true

# HTML tag attributes
htmlAttrs:
  dir: ltr
  lang: it
---

<style>
.slidev-page {
  padding: 0;
  background: url("/images/cover/database_versioning_cover_1-min.png");
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}
</style>

<!--
Buon pomeriggio a tutti e grazie per la partecipazione a questa sessione che potremmo definire di formazione.

Con questa presentazione, vorrei discutere insieme a voi di un tema su cui sono abbastanza sensibile e su cui ne abbiamo parlato tempo addietro con qualcuno di voi; credo che sia giunto il momento di affrontarlo in modo concreto e fare quel passo in più necessario per iniziare il processo di automazione anche per quel che riguarda le basi di dati applicative.

Questa presentazione vuole essere l'introduzione a un argomento conteso tra più aree di competenza e fondamentale per la gestione di un database in un contesto di sviluppo software di tipo collaborativo (o di social coding).

Detto ciò, per facilitare lo svolgimento di questa presentazione, vi pregherei  di mettere da parte tutte le vostre domande che affronteremo alla fine di questa presentazione.

La presentazione durerà non più di 40 minuti, lasciando il resto del tempo alle domande e approfondimenti.

Come ultima cosa vi chiedo il consenso per la registrazione di questa sessione per poi poterla condividerla successivamente.

Bene! Iniziamo
-->

---
src: ./pages/1_1_introduzione.md
---

---
src: ./pages/1_2_componenti_chiave_database_versioning.md
---

---
src: ./pages/1_3_benefici_database_versioning.md
---

---
src: ./pages/1_4_sicurezza_operazioni_deployment.md
---

---
src: ./pages/1_5_strumenti_comuni_database_versioning.md
---

---
src: ./pages/1_6_esempio_script_flyway.md
---

---
src: ./pages/1_7_esempio_progetto_migrazione_flyway.md
---

---
src: ./pages/1_8_conclusioni.md
---

---
src: ./pages/1_9_riferimenti.md
---

---
src: ./pages/1_10_domande.md
---

---
src: ./pages/1_11_about_me.md
---

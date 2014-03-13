Test Interessi Moratori
=======================

### Into

L'obiettivo è quello di, dati i file YAML con tutte le informazioni, ottenere il calcolo degli interessi moratori maturati ad oggi e il saldo ancora da pagare delle fatture.

### Funzionalità

Ogni fattura (invoices.yml) ha una data di scadenza, a partire da essa il netto della fattura ancora da pagare (esclusi i payments.yml effettuati prima) matura un interesse percentuale annuo nel range descritto dal file interests.yml.
Ad ogni nuovo pagamento l'interesse moratorio viene calcolato sul netto del valore della fattura.

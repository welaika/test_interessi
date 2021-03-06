Test Interessi Moratori
=======================

### Introduzione

L'obiettivo dell'esercizio è calcolare i saldi delle fatture e gli interessi moratori maturati; le informazioni necessarie sono fornite dai seguenti file YAML:

```
invoices.yml: fatture emesse
payments.yml: pagamenti già effettuati
interest_rates.yml: interessi moratori (percentuale in un range temporale definito e non sovrapposto)
```

I dati nei file YAML non sono ordinati cronologicamente.

### Funzionalità

Ogni fattura è composta così:

```yaml
- id: "1/2012"
  customer: "Mario Rossi"
  expire_at: 2012-02-28
  amount: 400.0
```

Ogni pagamento si riferisce a una fattura:

```yaml
- invoice_id: "1/2013"
  payed_at: 2013-03-15
  amount: 400.0
```

Ogni tasso di interesse è così composto:

```yaml
- start_at: 2012-01-01
  end_at: 2013-01-14
  percentage: 2
```

Ogni fattura ha una data di scadenza: a partire da questa data, comincia a maturare un interesse moratorio (indicato come percentuale annua). Se una fattura viene pagata solo in parte, l'interesse moratorio viene calcolato solo più sul netto ancora da pagare.

### Risultato atteso

Eseguendo il programma il giorno 13/03/2014, questi dovrebbero essere i risultati attesi:

``` ruby
{
  "1/2012" => {
    pending_invoice_amount: 400.0,
    moratory_interest: 14.66
  },
  "2/2012" => {
    pending_invoice_amount: 300.0,
    moratory_interest: 16.08
  },
  "1/2013" => {
    pending_invoice_amount: 300.0,
    moratory_interest: 9.98
  },
  "2/2013" => {
    pending_invoice_amount: 0.0,
    moratory_interest: 17.09
  }
}
```



# Ensembl VEP: conseguenze delle varianti

Umano, GRCh38, filamento diretto, solo sostituzioni di un singolo nucleotide. Fino a 10 varianti. L’allele di riferimento viene verificato nella sequenza genomica. Nessuna conversione GRCh37 o inferenza di patogenicità.

## Ambito

Analisi computazionale per ricerca. Non determina diagnosi, patogenicità, efficacia o trattamento. Verifica popolazione, fonte, versione e ambito prima di interpretare.

Interfaccia e contratti implementati in ELUCENIA. L’analisi dipende dalla disponibilità del servizio responsabile. La revisione clinica indipendente e la revisione linguistica professionale non sono complete.

## Ricerca

- Varianti: cromosoma posizione REF ALT, una per riga
- Assemblaggio di riferimento
- Cromosoma
- Posizione genomica
- Allele di riferimento
- Allele alternativo
- Confermo che invierò solo dati di ricerca pubblici o sintetici, senza dati di pazienti o informazioni riservate.

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "assembly": {
      "const": "GRCh38"
    },
    "variants": {
      "type": "array",
      "minItems": 1,
      "maxItems": 10,
      "uniqueItems": true,
      "items": {
        "$schema": "https://json-schema.org/draft/2020-12/schema",
        "type": "object",
        "properties": {
          "chromosome": {
            "type": "string",
            "pattern": "^(?:[1-9]|1[0-9]|2[0-2]|X|Y|MT)$"
          },
          "position": {
            "type": "integer",
            "minimum": 1,
            "maximum": 250000000
          },
          "reference": {
            "type": "string",
            "pattern": "^[ACGT]$"
          },
          "alternate": {
            "type": "string",
            "pattern": "^[ACGT]$"
          }
        },
        "required": [
          "chromosome",
          "position",
          "reference",
          "alternate"
        ],
        "additionalProperties": false
      }
    },
    "publicResearchData": {
      "const": true,
      "description": "Only public or synthetic research inputs; no patient/confidential data."
    }
  },
  "required": [
    "assembly",
    "variants",
    "publicResearchData"
  ],
  "additionalProperties": false
}
```

I nomi ufficiali dei termini e gli identificatori scientifici conservano la lingua della fonte; le etichette dell’interfaccia sono tradotte.

## Risultati

- Cromosoma
- Posizione genomica
- Allele di riferimento
- Allele alternativo
- Conseguenza
- Trascritto
- Gene
- Canonico
- Impatto
- Amminoacidi
- Posizione nella proteina

L’esportazione conserva fonti, attribuzione, versioni e limiti. I dati originali mantengono la propria licenza.

## Versione

`Ensembl 116 · REST 15.12 · GRCh38`

## Fonti

I dati generati da Ensembl possono essere utilizzati senza restrizioni secondo la dichiarazione del progetto. Questa interfaccia omette le annotazioni di terzi e non valuta la patogenicità.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## Limiti di attesa

Ogni richiesta a questo fornitore ha un limite di 60 secondi. Il flusso completo ha un limite di 120 secondi; l’interfaccia attende al massimo 125 secondi. Le richieste condividono il tempo rimanente del flusso. Non sono previsti tentativi automatici. Se il fornitore non risponde in tempo, l’analisi termina con un errore esplicito; nessun risultato viene stimato o sostituito.

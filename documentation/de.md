# Ensembl VEP: Variantenfolgen

Mensch, GRCh38, Vorwärtsstrang, ausschließlich einzelne Nukleotidsubstitutionen. Bis zu 10 Varianten. Das Referenzallel wird an der Genomsequenz geprüft. Keine GRCh37-Umrechnung oder Pathogenitätsbewertung.

## Umfang

Computergestützte Forschungsanalyse. Sie begründet keine Diagnose, Pathogenität, Wirksamkeit oder Behandlung. Prüfen Sie Population, Herkunft, Version und Umfang vor der Interpretation.

Oberfläche und Schnittstellenverträge sind in ELUCENIA implementiert. Die Analyse hängt von der Verfügbarkeit des zuständigen Dienstes ab. Die unabhängige klinische Prüfung und die professionelle sprachliche Prüfung sind nicht abgeschlossen.

## Abfrage

- Varianten: Chromosom Position REF ALT, eine pro Zeile
- Referenzassembly
- Chromosom
- Genomische Position
- Referenzallel
- Alternatives Allel
- Ich bestätige, dass ich ausschließlich öffentliche oder synthetische Forschungsdaten ohne Patienten- oder vertrauliche Daten übermittle.

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

Offizielle Begriffsnamen und wissenschaftliche Kennungen bleiben in der Quellsprache; die Oberflächenbeschriftungen sind übersetzt.

## Ergebnisse

- Chromosom
- Genomische Position
- Referenzallel
- Alternatives Allel
- Folge
- Transkript
- Gen
- Kanonisch
- Auswirkung
- Aminosäuren
- Proteinposition

Der Export erhält Quellen, Attribution, Versionen und Grenzen. Quelldaten behalten ihre Lizenz.

## Version

`Ensembl 116 · REST 15.12 · GRCh38`

## Quellen

Von Ensembl erzeugte Daten dürfen laut Projekterklärung uneingeschränkt verwendet werden. Diese Oberfläche lässt Anmerkungen Dritter weg und bewertet keine Pathogenität.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## Wartezeitbegrenzungen

Jede Anfrage an diesen Anbieter ist auf 60 Sekunden begrenzt. Der gesamte Ablauf ist auf 120 Sekunden begrenzt; die Oberfläche wartet höchstens 125 Sekunden. Die Anfragen teilen sich die verbleibende Zeit des Ablaufs. Es gibt keine automatische Wiederholung. Antwortet der Anbieter nicht rechtzeitig, endet die Analyse mit einer ausdrücklichen Fehlermeldung; es wird kein Ergebnis geschätzt oder ersetzt.

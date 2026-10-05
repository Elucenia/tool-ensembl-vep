# Ensembl VEP : conséquences des variants

Humain, GRCh38, brin direct, substitutions d’un seul nucléotide uniquement. Jusqu’à 10 variants. L’allèle de référence est vérifié dans la séquence génomique. Aucune conversion GRCh37 ni inférence de pathogénicité.

## Périmètre

Analyse informatique pour la recherche. Elle ne détermine ni diagnostic, ni pathogénicité, ni efficacité, ni traitement. Vérifiez population, source, version et périmètre avant interprétation.

Interface et contrats implémentés dans ELUCENIA. L’analyse dépend de la disponibilité du service responsable. La révision clinique indépendante et la révision linguistique professionnelle ne sont pas achevées.

## Requête

- Variants : chromosome position REF ALT, un par ligne
- Assemblage de référence
- Chromosome
- Position génomique
- Allèle de référence
- Allèle alternatif
- Je confirme que je transmettrai uniquement des données de recherche publiques ou synthétiques, sans données de patients ni données confidentielles.

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

Les noms officiels des termes et identifiants scientifiques conservent la langue de la source ; les libellés de l’interface sont traduits.

## Résultats

- Chromosome
- Position génomique
- Allèle de référence
- Allèle alternatif
- Conséquence
- Transcrit
- Gène
- Canonique
- Impact
- Acides aminés
- Position dans la protéine

L’export conserve les sources, l’attribution, les versions et les limites. Les données sources conservent leur licence.

## Version

`Ensembl 116 · REST 15.12 · GRCh38`

## Sources

Les données produites par Ensembl peuvent être utilisées sans restriction selon la déclaration du projet. Cette interface exclut les annotations de tiers et n’évalue pas la pathogénicité.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## Limites d’attente

Chaque requête à ce fournisseur est limitée à 60 secondes. Le traitement complet est limité à 120 secondes ; l’interface attend au maximum 125 secondes. Les requêtes partagent le temps restant du traitement. Aucune nouvelle tentative n’est automatique. Si le fournisseur ne répond pas à temps, l’analyse se termine par une erreur explicite ; aucun résultat n’est estimé ni substitué.

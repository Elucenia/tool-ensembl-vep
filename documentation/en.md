# Ensembl VEP: variant consequences

Human, GRCh38, forward strand, single nucleotide substitutions only. Up to 10 variants. The reference allele is checked against the genomic sequence. No GRCh37 conversion or pathogenicity inference.

## Scope

Computational research analysis. It does not establish diagnosis, pathogenicity, efficacy or treatment. Check population, provenance, version and scope before interpreting.

Interface and contracts implemented on ELUCENIA. Analysis depends on the responsible service being available. Independent clinical review and professional language review are incomplete.

## Query

- Variants: chromosome position REF ALT, one per line
- Reference assembly
- Chromosome
- Genomic position
- Reference allele
- Alternate allele
- I confirm that I will submit only public or synthetic research data, without patient or confidential data.

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

Official term names and scientific identifiers retain the source language; interface labels are translated.

## Results

- Chromosome
- Genomic position
- Reference allele
- Alternate allele
- Consequence
- Transcript
- Gene
- Canonical
- Impact
- Amino acids
- Protein position

Export preserves sources, attribution, versions and limitations. Source data retain their license.

## Version

`Ensembl 116 · REST 15.12 · GRCh38`

## Sources

Ensembl-generated data may be used without restriction under the project disclaimer. This interface omits third-party annotations and does not assess pathogenicity.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## Waiting limits

Each request to this provider has a 60-second limit. The complete workflow has a 120-second limit; the interface waits at most 125 seconds. Requests share the workflow’s remaining time. There is no automatic retry. If the provider does not respond in time, analysis ends with an explicit error; no result is estimated or substituted.

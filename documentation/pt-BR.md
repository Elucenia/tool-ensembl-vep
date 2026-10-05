# Ensembl VEP: consequências de variantes

Humanos, GRCh38, fita direta, apenas substituições de um nucleotídeo. Até 10 variantes. O alelo de referência é conferido na sequência genômica. Não converte GRCh37 nem infere patogenicidade.

## Escopo

Análise computacional para pesquisa. Não determina diagnóstico, patogenicidade, eficácia ou tratamento. Confira população, fonte, versão e escopo antes de interpretar.

Interface e contratos implementados na ELUCENIA. A análise depende da disponibilidade do serviço responsável. Revisão clínica independente e revisão linguística profissional não concluídas.

## Consulta

- Variantes: cromossomo posição REF ALT, uma por linha
- Genoma de referência
- Cromossomo
- Posição genômica
- Alelo de referência
- Alelo alternativo
- Confirmo que enviarei somente dados públicos ou sintéticos de pesquisa, sem dados de pacientes ou dados confidenciais.

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

Nomes oficiais de termos e identificadores científicos são preservados no idioma da fonte; os rótulos da interface estão traduzidos.

## Resultados

- Cromossomo
- Posição genômica
- Alelo de referência
- Alelo alternativo
- Consequência
- Transcrito
- Gene
- Canônico
- Impacto
- Aminoácidos
- Posição na proteína

A exportação conserva fontes, atribuição, versões e limites. Dados de origem mantêm sua licença.

## Versão

`Ensembl 116 · REST 15.12 · GRCh38`

## Fontes

Dados gerados pelo Ensembl podem ser usados sem restrição conforme a declaração do projeto. Esta interface omite anotações de terceiros e não avalia patogenicidade.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## Limites de espera

Cada requisição a este provedor tem limite de 60 segundos. O fluxo completo tem limite de 120 segundos; a interface espera no máximo 125 segundos. Os pedidos compartilham o tempo restante do fluxo. Não há repetição automática. Se o provedor não responder a tempo, a análise termina com um erro explícito; nenhum resultado é estimado ou substituído.

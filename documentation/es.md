# Ensembl VEP: consecuencias de variantes

Humanos, GRCh38, hebra directa, solo sustituciones de un nucleótido. Hasta 10 variantes. Se comprueba el alelo de referencia con la secuencia genómica. No convierte GRCh37 ni infiere patogenicidad.

## Alcance

Análisis computacional para investigación. No establece diagnóstico, patogenicidad, eficacia ni tratamiento. Revise población, fuente, versión y alcance antes de interpretar.

Interfaz y contratos implementados en ELUCENIA. El análisis depende de la disponibilidad del servicio responsable. No se han completado la revisión clínica independiente ni la revisión lingüística profesional.

## Consulta

- Variantes: cromosoma posición REF ALT, una por línea
- Ensamblaje de referencia
- Cromosoma
- Posición genómica
- Alelo de referencia
- Alelo alternativo
- Confirmo que enviaré solo datos públicos o sintéticos de investigación, sin datos de pacientes ni información confidencial.

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

Los nombres oficiales de términos e identificadores científicos conservan el idioma de la fuente; las etiquetas de interfaz están traducidas.

## Resultados

- Cromosoma
- Posición genómica
- Alelo de referencia
- Alelo alternativo
- Consecuencia
- Transcrito
- Gen
- Canónico
- Impacto
- Aminoácidos
- Posición en la proteína

La exportación conserva fuentes, atribución, versiones y límites. Los datos de origen mantienen su licencia.

## Versión

`Ensembl 116 · REST 15.12 · GRCh38`

## Fuentes

Los datos generados por Ensembl pueden usarse sin restricciones según la declaración del proyecto. Esta interfaz omite anotaciones de terceros y no evalúa patogenicidad.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## Límites de espera

Cada solicitud a este proveedor tiene un límite de 60 segundos. El flujo completo tiene un límite de 120 segundos; la interfaz espera como máximo 125 segundos. Las solicitudes comparten el tiempo restante del flujo. No hay reintentos automáticos. Si el proveedor no responde a tiempo, el análisis termina con un error explícito; no se estima ni se sustituye ningún resultado.

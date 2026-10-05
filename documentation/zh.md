# Ensembl VEP：变异后果

人类、GRCh38、正向链，仅支持单核苷酸替换。最多 10 个变异。参考等位基因会与基因组序列核对。不转换 GRCh37，也不推断致病性。

## 适用范围

用于研究的计算分析。不能据此确定诊断、致病性、疗效或治疗。解释前请核对人群、来源、版本与适用范围。

ELUCENIA已实现界面及请求和响应契约。分析依赖相应服务的可用性。独立临床审核和专业语言审核尚未完成。

## 查询

- 变异：染色体 位置 REF ALT，每行一个
- 参考基因组组装
- 染色体
- 基因组位置
- 参考等位基因
- 替代等位基因
- 我确认仅提交公开或合成研究数据，不含患者数据或保密信息。

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

官方术语名称和科学标识符保留来源语言；界面标签已翻译。

## 结果

- 染色体
- 基因组位置
- 参考等位基因
- 替代等位基因
- 后果
- 转录本
- 基因
- 标准转录本
- 影响
- 氨基酸
- 蛋白质位置

导出保留来源、署名、版本和限制。原始数据保留其许可证。

## 版本

`Ensembl 116 · REST 15.12 · GRCh38`

## 来源

根据项目声明，Ensembl生成的数据可不受限制地使用。本界面不提供第三方注释，也不评估致病性。

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## 等待时限

向此服务提供方发送的每个请求限时 60 秒。整个工作流程限时 120 秒，界面最多等待 125 秒。各请求共享工作流程的剩余时间。不会自动重试。如果服务提供方未及时响应，分析将以明确的错误结束；不会估算或替换任何结果。

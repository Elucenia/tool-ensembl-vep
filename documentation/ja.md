# Ensembl VEP：バリアントの影響

ヒト、GRCh38、順方向鎖の単一塩基置換のみ。最大10バリアント。参照アレルをゲノム配列と照合します。GRCh37からの変換や病原性の推定は行いません。

## 適用範囲

研究用の計算解析です。診断、病原性、有効性、治療を確定するものではありません。解釈前に対象集団、出典、バージョン、範囲を確認してください。

ELUCENIA内に画面とリクエスト・レスポンスの契約を実装しています。解析には提供元サービスの稼働が必要です。独立した臨床レビューと専門家による言語レビューは完了していません。

## クエリ

- バリアント：染色体 位置 REF ALT、1行に1件
- 参照ゲノムアセンブリ
- 染色体
- ゲノム上の位置
- 参照アレル
- 代替アレル
- 患者データや機密情報を含まない、公開または合成の研究データのみを送信することを確認します。

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

公式の用語名と科学的識別子は情報源の言語を保持します。インターフェースのラベルは翻訳済みです。

## 結果

- 染色体
- ゲノム上の位置
- 参照アレル
- 代替アレル
- 影響
- 転写産物
- 遺伝子
- 代表的転写産物
- 影響度
- アミノ酸
- タンパク質上の位置

エクスポートには出典、帰属、バージョン、制限を保持します。原データのライセンスは引き継がれます。

## バージョン

`Ensembl 116 · REST 15.12 · GRCh38`

## 情報源

プロジェクトの声明により、Ensemblが生成したデータは制限なく利用できます。この画面では第三者の注釈を除外し、病原性を評価しません。

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## 待機時間の上限

この提供元への各リクエストの上限は60秒です。処理全体の上限は120秒で、画面は最大125秒待機します。各リクエストは処理全体の残り時間を共有します。自動再試行は行いません。提供元が時間内に応答しない場合、分析は明示的なエラーで終了し、結果の推定や代替は行いません。

# Ensembl VEP: عواقب المتغيرات

الإنسان، GRCh38، الشريط المباشر، استبدالات نوكليوتيد واحد فقط. حتى 10 متغيرات. يُفحص الأليل المرجعي مقابل التسلسل الجينومي. لا يُحوّل GRCh37 ولا يستنتج الإمراضية.

## النطاق

تحليل حاسوبي لأغراض البحث. لا يحدد التشخيص أو الإمراضية أو الفعالية أو العلاج. تحقّق من المجموعة والمصدر والإصدار والنطاق قبل التفسير.

تم تنفيذ الواجهة وعقود الطلب والاستجابة داخل ELUCENIA. يعتمد التحليل على توفر الخدمة المسؤولة. لم تكتمل المراجعة السريرية المستقلة ولا المراجعة اللغوية المهنية.

## الاستعلام

- المتغيرات: الكروموسوم الموضع REF ALT، متغير في كل سطر
- التجميع الجينومي المرجعي
- الكروموسوم
- الموضع الجينومي
- الأليل المرجعي
- الأليل البديل
- أؤكد أنني سأرسل بيانات بحثية عامة أو اصطناعية فقط، دون بيانات مرضى أو معلومات سرية.

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

تُحفظ الأسماء الرسمية للمصطلحات والمعرّفات العلمية بلغة المصدر؛ تسميات الواجهة مترجمة.

## النتائج

- الكروموسوم
- الموضع الجينومي
- الأليل المرجعي
- الأليل البديل
- العاقبة
- النسخة المنسوخة
- الجين
- مرجعي قياسي
- التأثير
- الأحماض الأمينية
- الموضع في البروتين

يحفظ التصدير المصادر والنسب والإصدارات والحدود. تحتفظ البيانات الأصلية بترخيصها.

## الإصدار

`Ensembl 116 · REST 15.12 · GRCh38`

## المصادر

يمكن استخدام البيانات التي ينتجها Ensembl دون قيود وفق بيان المشروع. تستبعد هذه الواجهة تعليقات الجهات الأخرى ولا تقيّم الإمراضية.

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## حدود الانتظار

الحد الزمني لكل طلب إلى هذا المزوّد هو 60 ثانية. الحد الزمني لسير العمل الكامل هو 120 ثانية، وتنتظر الواجهة 125 ثانية كحد أقصى. تتشارك الطلبات الوقت المتبقي لسير العمل. لا توجد إعادة محاولة تلقائية. إذا لم يستجب المزوّد في الوقت المحدد، ينتهي التحليل بخطأ صريح؛ ولا تُقدَّر أي نتيجة ولا تُستبدل.

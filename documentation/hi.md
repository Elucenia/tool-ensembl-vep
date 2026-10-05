# Ensembl VEP: वेरिएंट के परिणाम

मानव, GRCh38, आगे की स्ट्रैंड, केवल एक न्यूक्लियोटाइड प्रतिस्थापन। अधिकतम 10 वेरिएंट। संदर्भ एलील का जीनोम अनुक्रम से मिलान किया जाता है। GRCh37 रूपांतरण या रोगजनकता का अनुमान नहीं होता।

## दायरा

अनुसंधान के लिए संगणकीय विश्लेषण। यह निदान, रोगजनकता, प्रभावकारिता या उपचार निर्धारित नहीं करता। व्याख्या से पहले जनसमूह, स्रोत, संस्करण और दायरा जाँचें।

ELUCENIA में इंटरफ़ेस और अनुरोध तथा प्रतिक्रिया अनुबंध लागू हैं। विश्लेषण संबंधित सेवा की उपलब्धता पर निर्भर है। स्वतंत्र नैदानिक समीक्षा और पेशेवर भाषा समीक्षा पूरी नहीं हुई हैं।

## प्रश्न

- वेरिएंट: गुणसूत्र स्थान REF ALT, प्रत्येक पंक्ति में एक
- संदर्भ जीनोम असेंबली
- गुणसूत्र
- जीनोम में स्थान
- संदर्भ एलील
- वैकल्पिक एलील
- मैं पुष्टि करता हूँ कि केवल सार्वजनिक या कृत्रिम अनुसंधान डेटा भेजूँगा, जिसमें रोगी या गोपनीय डेटा नहीं होगा।

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

आधिकारिक शब्द-नाम और वैज्ञानिक पहचानकर्ता स्रोत की भाषा में सुरक्षित रहते हैं; इंटरफ़ेस के लेबल अनूदित हैं।

## परिणाम

- गुणसूत्र
- जीनोम में स्थान
- संदर्भ एलील
- वैकल्पिक एलील
- परिणाम
- ट्रांसक्रिप्ट
- जीन
- मानक ट्रांसक्रिप्ट
- प्रभाव
- अमीनो अम्ल
- प्रोटीन में स्थान

निर्यात में स्रोत, श्रेय, संस्करण और सीमाएँ सुरक्षित रहते हैं। मूल डेटा का लाइसेंस बना रहता है।

## संस्करण

`Ensembl 116 · REST 15.12 · GRCh38`

## स्रोत

परियोजना की घोषणा के अनुसार Ensembl द्वारा उत्पन्न डेटा बिना प्रतिबंध इस्तेमाल किया जा सकता है। यह इंटरफ़ेस तृतीय-पक्ष एनोटेशन छोड़ देता है और रोगजनकता का आकलन नहीं करता।

- [https://rest.ensembl.org/documentation/info/vep_region_post](https://rest.ensembl.org/documentation/info/vep_region_post)
- [https://rest.ensembl.org/documentation/info/sequence_region](https://rest.ensembl.org/documentation/info/sequence_region)
- [https://www.ensembl.org/info/about/legal/disclaimer.html](https://www.ensembl.org/info/about/legal/disclaimer.html)

## प्रतीक्षा की समय-सीमाएँ

इस प्रदाता को भेजे गए हर अनुरोध की सीमा 60 सेकंड है। पूरी कार्यप्रक्रिया की सीमा 120 सेकंड है; इंटरफ़ेस अधिकतम 125 सेकंड प्रतीक्षा करता है। सभी अनुरोध कार्यप्रक्रिया का बचा हुआ समय साझा करते हैं। अपने-आप दोबारा प्रयास नहीं किया जाता। यदि प्रदाता समय पर जवाब नहीं देता, तो विश्लेषण स्पष्ट त्रुटि के साथ समाप्त होता है; किसी परिणाम का अनुमान नहीं लगाया जाता और न ही कोई वैकल्पिक परिणाम दिया जाता।

# قاموس الذكاء الاصطناعي بالعربي

**٢٬٠٠٢ مصطلح في الذكاء الاصطناعي، كل واحد مشروح بعربي بسيط — مفتوح ومجاني وقابل لإعادة الاستخدام.**

المصطلحات التقنية في الذكاء الاصطناعي تُكتب بالإنجليزية، وترجمتها الحرفية غالباً تزيد الغموض بدل أن تزيله. هذا القاموس يشرح المصطلح بلغة يفهمها القارئ العربي، ويُبقي المصطلح اللاتيني كما هو لأنه الصيغة التي سيصادفها في أي مرجع.

| | |
|---|---|
| **المجموع** | ٢٬٠٠٢ مصطلح |
| **مفاهيم** | [١٬٤٩٤](terms/concept.md) |
| **نماذج** | [٢٥٩](terms/model.md) |
| **مقاييس** | [١٤١](terms/metric.md) |
| **مجموعات بيانات** | [١٠٨](terms/dataset.md) |
| **مصطلحات جوهرية ⭐** | ١١٢ — لها شرح موسّع في مقالة مستقلة |

## الملفّات

| الملف | الاستخدام |
|---|---|
| [`data/glossary.json`](data/glossary.json) | للبرمجة والتطبيقات |
| [`data/glossary.csv`](data/glossary.csv) | للجداول وExcel (بترميز UTF-8 BOM) |
| [`terms/*.md`](terms/) | للتصفّح والقراءة مباشرة هنا |

### بنية المدخلة

```json
{
  "term": "benchmark",
  "type": "concept",
  "level": "core",
  "definition": "اختبار قياسي موحّد تُقاس به النماذج...",
  "article": "https://ai.salamthabet.com/lesson.php?slug=what-is-a-benchmark",
  "source": "https://ai.salamthabet.com/glossary.php?q=benchmark"
}
```

## الاستخدام

```python
import json, urllib.request

url = "https://raw.githubusercontent.com/USER/arabic-ai-glossary/main/data/glossary.json"
data = json.load(urllib.request.urlopen(url))

terms = {t["term"].lower(): t for t in data["terms"]}
print(terms["benchmark"]["definition"])
```

```javascript
const res  = await fetch("https://raw.githubusercontent.com/USER/arabic-ai-glossary/main/data/glossary.json");
const data = await res.json();
const find = q => data.terms.filter(t => t.term.toLowerCase().includes(q.toLowerCase()));
```

## الترخيص والنسب

المحتوى تحت رخصة **[CC BY-SA 4.0](LICENSE)**. لك أن تنسخه وتعدّله وتستخدمه تجارياً، بشرطين:

1. **النسب** — اذكر المصدر: قاموس الذكاء الاصطناعي بالعربي — [ai.salamthabet.com](https://ai.salamthabet.com/glossary.php)
2. **المشاركة بالمثل** — إذا عدّلت ووزّعت، وزّع بنفس الرخصة.

## كيف صُنع هذا القاموس

المصطلحات تُستخرج آلياً من ملخّصات الأوراق البحثية اليومية في نشرة [«شو في AI؟»](https://ai.salamthabet.com)، ثم تُشرح وتُراجَع.

**وهذا يعني أن جودة المدخلات متفاوتة، ونقولها بصراحة:** هذه النسخة منتقاة لا شاملة. من أصل ٤٬٧٣٤ مدخلاً في قاعدة البيانات، نُشر هنا ٢٬٠٠٢ فقط — واستُبعد الباقي لأنه أسماء نماذج وإصدارات ومجموعات بيانات مفردة (مثل `StereoWorldBench-v2`) لا مصطلحات عامة، أو شروح أقصر من أن تفيد.

المصطلحات المعلّمة بـ ⭐ هي الأعلى ثقة: وردت في مقالات تعليمية مكتوبة ومراجَعة، ولكل منها رابط شرح موسّع.

**إذا وجدت شرحاً ناقصاً أو خاطئاً، [افتح issue](../../issues) أو pull request** — المراجعة البشرية هي ما ينقص هذا النوع من الموارد.

## المصدر

- الموقع: **[ai.salamthabet.com](https://ai.salamthabet.com)** — نشرة ومقالات تعليمية بالعربي عن الذكاء الاصطناعي
- القاموس الكامل والبحث فيه: [ai.salamthabet.com/glossary.php](https://ai.salamthabet.com/glossary.php)
- الإعداد: **سلام ثابت** — باحثة دكتوراه في علوم الحاسوب، معالجة اللغات الطبيعية

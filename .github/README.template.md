# قاموس الذكاء الاصطناعي بالعربي

**{{TOTAL}} مصطلح في الذكاء الاصطناعي، كل واحد مشروح بعربي بسيط — مفتوح ومجاني وقابل لإعادة الاستخدام.**

المصطلحات التقنية في الذكاء الاصطناعي تُكتب بالإنجليزية، وترجمتها الحرفية غالباً تزيد الغموض بدل أن تزيله. هذا القاموس يشرح المصطلح بلغة يفهمها القارئ العربي، ويُبقي المصطلح اللاتيني كما هو لأنه الصيغة التي سيصادفها في أي مرجع.

<table dir="rtl">
<tr><td><b>المجموع</b></td><td>{{TOTAL}} مصطلح</td></tr>
<tr><td>مفاهيم</td><td><a href="terms/concept.md">{{CONCEPT}}</a></td></tr>
<tr><td>نماذج</td><td><a href="terms/model.md">{{MODEL}}</a></td></tr>
<tr><td>مقاييس</td><td><a href="terms/metric.md">{{METRIC}}</a></td></tr>
<tr><td>مجموعات بيانات</td><td><a href="terms/dataset.md">{{DATASET}}</a></td></tr>
<tr><td><b>مصطلحات جوهرية ⭐</b></td><td>{{CORE}} — لكلٍّ منها مقالة شرح موسّع</td></tr>
</table>

## الملفّات

<table dir="rtl">
<tr><th>الملف</th><th>الاستخدام</th></tr>
<tr><td><a href="data/glossary.json"><code>data/glossary.json</code></a></td><td>للبرمجة والتطبيقات</td></tr>
<tr><td><a href="data/glossary.csv"><code>data/glossary.csv</code></a></td><td>للجداول وبرنامج Excel — مُرمَّز <code>UTF-8 BOM</code></td></tr>
<tr><td><a href="terms/"><code>terms/*.md</code></a></td><td>للتصفّح والقراءة هنا مباشرة</td></tr>
</table>

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

## شبكة المصطلحات

المصطلحات لا تعيش منفردة: `attention` أساس `transformer`، و`RAG` تجمع `embedding` مع قاعدة بيانات متّجهة. ملف [`data/graph.json`](data/graph.json) يمثّل هذه العلاقات شبكةً غير موجّهة.

<table dir="rtl">
<tr><td><b>العقد</b></td><td>{{G_NODES}} — منها {{G_CONN}} موصولة</td></tr>
<tr><td><b>الحوافّ</b></td><td>{{G_EDGES}}</td></tr>
</table>

**كل حافّة مقيسة لا مُولّدة.** لم يُسأل نموذج لغة «ما علاقة س بـص» — ذلك يُنتج شبكة مقنعة الشكل خاطئة المضمون. مصدر كل حافّة تواجد فعلي محفوظ، ومعها حقل `via` يذكر مصدرها:

<table dir="rtl">
<tr><th>قيمة <code>via</code></th><th>معناها</th><th>الوزن</th></tr>
<tr><td><code>cluster</code></td><td>وردا في عنقود مُرتَّب يدوياً</td><td>×٥</td></tr>
<tr><td><code>lesson</code></td><td>وردا ضمن مصطلحات المقالة نفسها</td><td>×٣</td></tr>
<tr><td><code>issue</code></td><td>وردا في أوراق اليوم نفسه</td><td>×١</td></tr>
</table>

ويُصدَّر أيضاً [`data/graph_edges.csv`](data/graph_edges.csv) بأعمدة `Source,Target,Weight,Via` — يُفتح مباشرة في Gephi أو Cytoscape.

```python
import json, networkx as nx

g = json.load(open("data/graph.json"))
G = nx.Graph()
G.add_nodes_from((n["id"], n) for n in g["nodes"])
G.add_weighted_edges_from((e["source"], e["target"], e["weight"]) for e in g["edges"])

print(sorted(G.degree, key=lambda x: -x[1])[:10])   # الأكثر مركزية
print(list(G.neighbors("llm"))[:20])                # جيران مصطلح
```

**معرّفات العقد هي `slug` نفسها في `glossary.json`** فيمكن ربط الملفّين مباشرة. والعقد المعزولة مُبقاة عمداً: إخفاؤها يموّه أن أغلب القاموس لم يُربط بعد.

## الاستخدام

```python
import json, urllib.request

url = "https://raw.githubusercontent.com/salamthabet95/arabic-ai-glossary/main/data/glossary.json"
data = json.load(urllib.request.urlopen(url))

terms = {t["term"].lower(): t for t in data["terms"]}
print(terms["benchmark"]["definition"])
```

```javascript
const res  = await fetch("https://raw.githubusercontent.com/salamthabet95/arabic-ai-glossary/main/data/glossary.json");
const data = await res.json();
const find = q => data.terms.filter(t => t.term.toLowerCase().includes(q.toLowerCase()));
```

## الترخيص والنسب

المحتوى تحت رخصة **[CC BY-SA 4.0](LICENSE)**. لك أن تنسخه وتعدّله وتستخدمه تجارياً، بشرطين:

1. **النسب** — اذكر المصدر: قاموس الذكاء الاصطناعي بالعربي — [ai.salamthabet.com](https://ai.salamthabet.com/glossary.php)
2. **المشاركة بالمثل** — إذا عدّلت ووزّعت، وزّع بنفس الرخصة.

## كيف صُنع هذا القاموس

المصطلحات تُستخرج آلياً من ملخّصات الأوراق البحثية اليومية في نشرة [«شو في AI؟»](https://ai.salamthabet.com)، ثم تُشرح وتُراجَع.

**وهذا يعني أن جودة المدخلات متفاوتة، ونقولها بصراحة:** هذه النسخة منتقاة لا شاملة. من أصل {{RAW}} مدخلاً في قاعدة البيانات، نُشر هنا {{TOTAL}} فقط — واستُبعد الباقي لأنه أسماء نماذج وإصدارات ومجموعات بيانات مفردة (مثل `StereoWorldBench-v2`) لا مصطلحات عامة، أو شروح أقصر من أن تفيد.

المصطلحات المعلّمة بـ ⭐ هي الأعلى ثقة: وردت في مقالات تعليمية مكتوبة ومراجَعة، ولكل منها رابط شرح موسّع.

**إذا وجدت شرحاً ناقصاً أو خاطئاً، [افتح issue](../../issues) أو pull request** — المراجعة البشرية هي ما ينقص هذا النوع من الموارد.

## المصدر

- الموقع: **[ai.salamthabet.com](https://ai.salamthabet.com)** — نشرة ومقالات تعليمية بالعربي عن الذكاء الاصطناعي
- القاموس الكامل والبحث فيه: [ai.salamthabet.com/glossary.php](https://ai.salamthabet.com/glossary.php)
- الإعداد: **سلام ثابت** — باحثة دكتوراه في علوم الحاسوب، معالجة اللغات الطبيعية


---

*آخر تحديث: {{UPDATED}} — هذا الملف يُولَّد آلياً من قاعدة البيانات، والأرقام فيه تتحدّث مع كل تصدير.*

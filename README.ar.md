# Claude Code × OpenCode Zen API — دليل إعداد متعدد المنصات، بدون proxy، بدون rate limiting، وبدون كلام فارغ.

> **إشعار الخصوصية أولًا:** قد تستخدم النماذج المجانية في OpenCode Zen أو أي مزود LLM مجاني آخر مطالباتك لتحسين نماذجها.
> تجنب إرسال الكود الحساس أو بيانات الاعتماد أو أي معلومات خاصة.
> راجع [وثائق خصوصية Zen](https://opencode.ai/docs/zen/#privacy) و[سياسة الخصوصية](https://opencode.ai/legal/privacy-policy) للتفاصيل.

---

## ما هو OpenCode Zen؟

OpenCode Zen هو بوابة API مجانية ومتوافقة مع Anthropic، وتقوم بمقارنة أفضل النماذج والمزودين لوكلاء البرمجة. وعلى الرغم من أنه مصمم للعمل مع OpenCode، فإنه **يعمل مع أي وكيل** — بما في ذلك Claude Code — بمجرد ضبط `ANTHROPIC_BASE_URL` على `https://opencode.ai/zen`.

الهدف المعلن له هو:

> *"مقارنة أفضل النماذج/المزودين لوكلاء البرمجة."*
> — [opencode.ai/docs/zen/#goals](https://opencode.ai/docs/zen/#goals)

---

## النماذج التي تعمل

تم تأكيد أن نموذجين فقط يعملان بشكل موثوق حاليًا:

| النموذج | الملاحظات |
|---|---|
| `big-pickle` | **مُوصى به.** اربط جميع خانات Anthropic بهذا النموذج. |
| `minimax-m2.5-free` | بديل مجاني. قد تُستخدم البيانات لتدريب النماذج. |

النماذج الأخرى لن تعمل الآن.
[إذا كان الأمر مهمًا لك، أبلغ عن المشكلة هنا](https://github.com/anomalyco/opencode/issues/new).
تم الإبلاغ عن المشكلة لدى المشرفين، وتحقق هنا من أي تحديثات.

---

## القيود المعروفة

- ❌ إضافة **Claude for Chrome** غير مدعومة، لأن Zen يعمل كواجهة API فقط.
- ❌ تكاملات القنوات مثل **Slack** و**Telegram** غير مدعومة.
- ❌ يعمل فقط نموذجا `big-pickle` و`minimax-m2.5-free`.
- ❌ مرة أخرى، بما أن هذه نماذج مجانية، فقد تُستخدم المطالبات للتدريب، لذا لا ترسل كودًا حساسًا أو خاصًا.

---

## أفضل إعداد معروف

هذا هو الإعداد الموصى به الذي يربط جميع مستويات Anthropic بـ `big-pickle`:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://opencode.ai/zen",
    "ANTHROPIC_AUTH_TOKEN": "sk-In....", # الصق مفتاح Zen API هنا
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "big-pickle"
  },
  "model": "big-pickle"
}
```

---

## دليل الإعداد

### الخطوة 1 — تثبيت Claude Code

زر [مستودع Claude Code على GitHub](https://github.com/anthropics/claude-code)

### الخطوة 2 — احصل على مفتاح Zen API

زر [opencode.ai/zen](https://opencode.ai/docs/zen/#how-it-works)، أنشئ حسابًا وانسخ مفتاح API الخاص بك، ولا حاجة لتفعيل الفوترة.
ضعه بدل `PASTE_YOUR_KEY` في ملف `config.json`.

### الخطوة 3 — اضبط بيئتك

هذه الطريقة عبر **ملف config** هي الطريقة الوحيدة التي أوصي بها لأنها قابلة للنقل ومستقلة عن المنصة.

خذ نسخة احتياطية من إعداداتك الحالية أولًا، لأنك ستحتاج إلى الاستبدال.

أنشئ أو عدل الملف `.claude/config.json` في مجلد المنزل:

```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://opencode.ai/zen",
    "ANTHROPIC_AUTH_TOKEN": "PASTE_YOUR_KEY",
    "ANTHROPIC_DEFAULT_SONNET_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_OPUS_MODEL": "big-pickle",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "big-pickle"
  },
  "model": "big-pickle"
}
```

```text
# macOS / Linux
~/.claude/config.json

# Windows
%USERPROFILE%\.claude\config.json
```

### الخطوة 4 — شغّل Claude Code

```bash
cd /your/project
claude /logout
claude
```

سيستخدم Claude Code Zen كخلفية تلقائيًا. اطرح عليه سؤالًا بسيطًا للتأكد من أنه يعمل.

---

## كيف يعمل

يعمل Zen كبديل مباشر لواجهة Anthropic API. لا يدرك Claude Code أي فرق — إذ تُربط جميع المستويات الثلاثة للنماذج (Sonnet وOpus وHaiku) بـ `big-pickle`، وهو اسم مستعار يستخدمه Zen داخليًا. قد يختلف النموذج الفعلي في الخلفية، لأن Zen يقارن النماذج بشكل مجهول لتقليل التحيز.

---

## الروابط

- [لوحة تحكم Zen](https://opencode.ai/zen)
- [وثائق خصوصية Zen](https://opencode.ai/docs/zen/#privacy)
- [أهداف Zen](https://opencode.ai/docs/zen/#goals)
- [سياسة الخصوصية](https://opencode.ai/legal/privacy-policy)
- [شروط الخدمة](https://opencode.ai/legal/terms-of-service)
- [الإبلاغ عن مشكلة](https://github.com/anomalyco/opencode/issues/new)
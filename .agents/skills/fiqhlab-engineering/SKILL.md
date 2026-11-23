---
name: fiqhlab-engineering
description: FiqhLab (مختبر الفقه) engineering rules for mwqwf/FiqhLab and fiqhlab-packs — interactive comparative fiqh knowledge layer (reference, issue graph, corrected training lab, student level map) built on classical sources; the factory pipeline (extract → claims/lock → trust → adjudicate → i18n → compile → pack), the faraid solver plugin and golden sets, invariants (AI assists, the source is the authority), cloud-first execution, paid-Actions budget gate, release via ops/release-request.json, and the reading order START_HERE → STATE → INVARIANTS → ROADMAP. Use for any FiqhLab task: factory steps, claims, packs, solver, app (com.ali.fiqhlab), release, or planning. هندسة مختبر الفقه.
license: Proprietary (mwqwf) — internal
---

# مختبر الفقه (FiqhLab)

طبقة معرفية تفاعلية فوق التراث الفقهيّ: مرجع مقارن + رسم معرفيّ للمسائل + مختبر تدريب مصحَّح + خريطة مستوى للطالب — كل دعوى منسوبة لمصدرها من كتب المتقدّمين والمذاهب.

## ابدأ هكذا (كل جلسة، كل منصّة)
```
git fetch origin main && git merge --no-edit origin/main   # لا rebase (قاعدة المشروع)
bash scripts/check.sh --no-android                          # يجب أن يخرج أخضر قبل أن تلمس شيئاً
```
ثم اقرأ بالترتيب: `START_HERE.md` ⇒ `docs/STATE.md` (DONE/CURRENT/NEXT/BLOCKED) ⇒ `docs/INVARIANTS.md` ⇒ `docs/ROADMAP.md` (المرجع الأعلى) ⇒ `docs/DECISIONS.md` ⇒ `docs/CLOUD_FIRST.md`. خطّة البرنامج: `docs/PLAN_FIQH_MUSHAFAK.md`. والحالة الحيّة المختصرة: `docs/PROJECT_STATE.md`.

## ثوابت
- **الذكاء الاصطناعي مساعدٌ في المصنع لا مرجعٌ للفقه (INV-02):** المرجع هو المصدر؛ لا دعوى بلا موضعها (كتاب، جزء، صفحة/فقرة). لا تختلق نصّاً أو نسبةً لمذهب. النصوص الشرعية تخضع لـ`arabic-rtl-and-islamic-typography` §٣.
- لا إعادة تخطيط: الفكرة الجديدة تمرّ بـ`docs/PROPOSALS.md`، والتجربة الفاشلة تُسجّل في `docs/FAILED_EXPERIMENTS.md`، والقرار المفوَّض يُقضى ويُسجّل `D-xxx` بسببه (ولا تنتحل شهادة لم تقع).
- لا تبدأ مرحلة قبل تحقّق شروط إكمال سابقتها (إلا المتوازي في الخارطة).
- **«لا تتوقّف أبداً» (أمر 2026-09-20):** المتعذّر يُسجّل ويُتجاوز: ما يحتاج المالك ⇒ بند `O-xx` في `CLOUD_FIRST.md` §٦؛ ما يحتاج جهازاً ⇒ استنفد البدائل السحابية ثم `L-xx` في `docs/LOCAL_TASKS.md`؛ ثم امضِ.

## المصنع
- خطوات حتمية تعمل في أي حاوية: الحرّاس · `claims` · `trust` · `i18n` · `compile` · `pack` · المحرّك و`:plugins:faraid` (`./gradlew -Pfiqhlab.android=off`) واختبارات المصنع.
- ⛔ بعد أي `claims --lock` أودِع `claims/ids.lock` مع الدعاوى في الإيداع نفسه.
- تقرير مرحلة من الأرقام الحيّة: `cd factory && python -m fiqhlab_factory.phase_report faraid`.
- الخطوات ذات نداء النماذج تحتاج أسرار Actions (لا مفاتيح في الحاويات).

## الإنفاق (مستودع خاص — يدفع المالك فعلاً)
- كل وظيفة Actions خلف `vars.FIQHLAB_ACTIONS_BUDGET == 'ok'`، والسقف ≤ 900 دقيقة/شهر. لا تُطلق شوطاً بلا حاجة، ولا تزد محفّزات، ولا ترفع سقوفاً، ولا تشغّل `all`.
- مسارات `factory-daily` و`app-build` معطّلة تلقائياً بأمر المالك (2026-09-20) — يدوية فقط.
- لا تُعِد تفعيل مهمّة Windows `FiqhLab-resume-extract` (كاتبٌ ثانٍ على `claims/`).
- بناء `:app` يحتاج `dl.google.com` (محجوب في بعض الحاويات) ⇒ يبنى في CI أو على حاسوب الوكيل الدائم إن أتاحه.

## الإصدار
`com.ali.fiqhlab` — تعديل `ops/release-request.json` في `main` يُطلق `release.yml` (الافتراضي `internal`؛ الإنتاج يتطلّب `"confirm": "production:<versionCode>"`). التفصيل في `docs/agents/PLAY_APP.md` ومهارة `google-play-publish`. `fiqhlab-packs` (عام) ينشر صفحات الحزم وسياسة الخصوصية عبر GitHub Pages.

## «أُنجز»
`scripts/check.sh` أخضر + الحرّاس الحتمية + تحديث `docs/STATE.md` (وDECISIONS/CHANGELOG عند الحاجة) + لقطة بصرية للواجهة عند مسّها. القاعدة: لو انقطعت الجلسة الآن، هل تعرف جلسةٌ جديدة الحقيقة من الملفات وحدها؟

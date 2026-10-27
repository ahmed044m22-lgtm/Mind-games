# ألعاب العقل | Mind Games

**Premium offline-first cognitive training foundation**  
**من المطور / أحمد ابراهيم**

هذه الحزمة هي النواة البرمجية الأولى الفعلية للمشروع الكبير: ليست مجرد Mockup، بل تحتوي واجهات Responsive/Adaptive، تنقل متعدد الأحجام، حفظ محلي، إعدادات عربية/إنجليزية، تقدم وXP، مكتبة ألعاب، وأربع آليات لعب Procedural قابلة للتشغيل.

## ما تم تنفيذه الآن

- هوية Dark / OLED / Light أولية مع Design Tokens موحدة.
- Arabic RTL + English LTR وتبديل اللغة من داخل التطبيق.
- Splash فاخر مع اسم التطبيق واسم المطور.
- Onboarding لأول تشغيل.
- Adaptive navigation:
  - Phone: Bottom Navigation.
  - Tablet: Navigation Rail.
  - Desktop/Large: Extended Rail / Sidebar.
  - Ultra-wide: لوحة مؤشرات جانبية إضافية.
- Home Dashboard مع Daily Training وSkill Map وتحديات.
- Training Center مع Presets.
- Games Library مع Search + Filters.
- Game Detail / Start / Pause / Results داخل Game Hub.
- Desktop keyboard shortcuts داخل اللعبة:
  - Space: Start/Pause/Resume.
  - Esc: Back.
  - Enter: Start.
- أربع آليات لعب فعلية Procedural:
  1. Neural Reaction — سرعة الاستجابة.
  2. Signal Hunt — التركيز والبحث البصري.
  3. Sequence Vault — الذاكرة التسلسلية.
  4. Math Rush — الحساب الذهني.
- Variants إضافية في الكتالوج مبنية على نفس المحركات.
- XP + Level + Skill Score update بعد نهاية اللعبة.
- حفظ محلي تلقائي للإعدادات والتقدم باستخدام ملف JSON ذري داخل Application Support Directory.
- Progress & Analytics dashboard أولي.
- Profile + Achievements + Settings + About.
- عبارة واضحة بأن المؤشرات ليست تشخيصاً طبياً.
- صفحة About تعرض بوضوح:
  - ألعاب العقل / Mind Games
  - من المطور / أحمد ابراهيم

## التشغيل لأول مرة

> يتطلب Flutter SDK حديثاً متوافقاً مع Dart 3.12+.

من داخل مجلد المشروع:

```bash
flutter create --platforms=android,windows .
flutter pub get
flutter run
```

لتشغيل Windows مباشرة:

```bash
flutter run -d windows
```

ولبناء APK:

```bash
flutter build apk --release
```

ولبناء Windows:

```bash
flutter build windows --release
```

## البنية

```text
lib/
  app/
    mind_games_app.dart
    router.dart
  core/
    adaptive/
    design/
    localization/
    storage/
  features/
    splash/
    onboarding/
    home/
    train/
    games/
      engine/
      models/
      screens/
      widgets/
    progress/
    achievements/
    profile/
    settings/
    about/
    shared/
```

## نقطة مهمة قبل التوسع الكبير

التخزين الحالي مقصود به تشغيل النواة بسرعة وبلا Code Generation. قبل إضافة آلاف سجلات History وFlashcards وMemory Palace ومراجعات Spaced Repetition، انقل طبقة التخزين إلى **SQLite/Drift** مع الحفاظ على نفس Repository boundary. لا تربط شاشات اللعب مباشرة بقاعدة البيانات.

## المرحلة التالية ذات الأولوية

1. إضافة Database layer بـDrift للجلسات، النتائج، الإنجازات، المراجعات، Memory Palace، وسجل التحديات.
2. إنشاء `CognitiveEngine` مستقل يحسب adaptive difficulty، fatigue signal، error patterns، وrecommended session.
3. إضافة 8–12 Game Engines جديدة بدلاً من تكرار نفس اللعب بقوالب مختلفة.
4. إضافة Daily/Weekly Challenges generator وSeed history لمنع التكرار.
5. إضافة Calendar/History/Heatmap وRadar Chart.
6. إضافة Active Recall + Spaced Repetition + Memory Palace.
7. إضافة Local notifications وBackup export/import مشفر.
8. إضافة Sound/Haptics service وLow/Ultra Visual modes.

## المبدأ المعماري

كل لعبة يجب أن تكون Plugin داخلياً يعرف:

- ID
- Category
- Rules
- Difficulty
- Scoring
- Procedural generator
- Adaptive parameters
- Analytics events
- Accessibility behavior
- Supported input: touch/mouse/keyboard

وبهذا يمكن إضافة عشرات الألعاب دون تحويل المشروع إلى كتلة واحدة يصعب صيانتها.

# Dirassaty (دراساتي) — النشر على Vercel

## 1) ارفع المحتوى بشكل صحيح
افتح ضغط الملف، وارفع **محتوى** المجلد مباشرة لجذر المستودع (يجب أن يكون `package.json` و`index.html` في الجذر، لا داخل مجلد فرعي).
وإن وُضعت داخل مجلد فرعي فاضبط Root Directory في Vercel على ذلك المجلد.

## 2) Supabase
- SQL Editor: شغّل `supabase.sql` مرة واحدة.
- Authentication ← Providers ← Google: فعّله وأدخل Client ID/Secret من Google Cloud Console.
  في Google Cloud أضف Authorized redirect URI: `https://<مشروعك>.supabase.co/auth/v1/callback`
- Authentication ← URL Configuration: Site URL = رابط موقعك، وأضف في Redirect URLs: `https://<نطاقك>/**` (ولمعاينات Vercel: `https://*-<فريقك>.vercel.app/**`).

### التسجيل وتأكيد البريد (أكثر أسباب فشل إنشاء الحساب)
- Authentication ← Sign In / Providers: فعّل Email وأبقِ «Allow new users to sign up» مفعّلاً.
- بريد التأكيد: خدمة البريد الافتراضية في Supabase محدودة جداً (قد ترفض عناوين خارج فريقك أو تتجاوز الحد بسرعة).
  لإنتاج حقيقي اضبط SMTP مخصصاً: Authentication ← Emails ← SMTP Settings (يوجد مزوّدون بخطة مجانية).
- Site URL وRedirect URLs يجب أن تحتوي رابط موقعك بالضبط، وإلا يفتح رابط التأكيد صفحة خاطئة (غالباً localhost).
- على شاشة الدخول زر «فحص إعدادات الاتصال» يعرض ما يمكن فحصه من المتصفح.

## 3) Vercel
- Framework Preset: Other (يقرأ الإعداد من `vercel.json`: Build `npm run build`، Output `dist`).
- Settings ← Environment Variables (Production وPreview):
  `SUPABASE_URL` و`SUPABASE_ANON_KEY` (مفتاح anon/publishable فقط، لا service_role أبداً).
- **أعد النشر (Redeploy) بعد أي تغيير في المتغيرات**: القيم تُدمج وقت البناء.
- البناء في الإنتاج يفشل برسالة واضحة إذا كانت المتغيرات ناقصة أو المفتاح سرّياً أو أي صورة/ملف مفقود.

## 4) تجربة محلية
`SUPABASE_URL=... SUPABASE_ANON_KEY=... npm run build` ثم `npx serve dist`.

## بعد النشر تحقق من
فتح `/config.js` (يجب أن يظهر رابط مشروعك)، ثم تسجيل الدخول بالبريد وبـ Google، وأن الصفحة لا تعرض رسالة حمراء/تنبيه أعلى نموذج الدخول.
دوال الذكاء الاصطناعي `ai` و`ai-image` (Supabase Edge Functions) غير مضمّنة بعد.

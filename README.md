# Dirassaty (دراساتي)
1. Supabase: شغّل `supabase.sql` في SQL Editor، ثم فعّل Google من Auth > Providers.
2. ضع Project URL و anon key في `config.js` (لا تضع service_role أبداً).
3. انشر المجلد كما هو على Vercel (ملف `vercel.json` يضبط رؤوس الأمان وCSP). بدون Build.
4. أضف Redirect URL لموقعك في Supabase > Auth > URL Configuration.
5. Edge Functions المطلوبة للذكاء الاصطناعي: `ai` و`ai-image` (غير مضمّنة بعد).
المحتوى (فروض/فيديوهات): أضف صفوفاً في جدول `content` وملفات في bucket `content`.

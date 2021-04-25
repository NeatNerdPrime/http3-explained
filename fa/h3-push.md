# فشارِ سرورِ HTTP/3

فشار سرور HTTP/3 شبیه به آن چیزیست که در HTTP/2 ([RFC
7540](https://httpwg.org/specs/rfc7540.html)) توصیف شده است، اما از ساز و کار
متفاوتی بهره می‌گیرد.

یک فشار سرور (server push) در واقع پاسخ به درخواستی است که کارخواه هرگز ارسال
نکرد!

فشار‌های سرور تنها در صورتی ایجاد می‌شوند که از سمت کارخواه با آنها
موافقت شده باشد. در HTTP/3 کارخواه حتی محدودیتی برای تعداد فشارهایی که قبول
می‌کند با اعلام بیشترین شناسه‌ی جریانِ فشار برای کارساز ایجاد
می‌کند. و از آن حد بالاتر رفتن موجب خطا در اتصال می‌گردد. 

حتی هنگامی که که از پیش گفته شده باشد که فشار‌ها توسط کارخواه مورد قبول
هستند، هر جریانِ فشار می‌تواند در هر زمان که کارخواه صلاح بداند لغو گردد. که
در این صورت یک قاب CANCEL_PUSH به سمت سرور فرستاده می‌شود.

## دشواری

از همان زمانی که این ویژگی برای نخستین بار در توسعه‌ی HTTP/2 مطرح شد و
بعد‌تر که پروتکل بر روی بستر اینترنت توسعه پیدا کرد و توزیع شد، در خصوص این
ویژگی بحث شد، انتقاد شد و به کرّات به روش‌های گوناگون مورد حمله قرار گرفت تا
که به حالتی قابل استفاده درآید.

فشار هرگز ”رایگان“ نیست چرا که در ذخیره و نگاه‌داشت یک نیم round-trip هنوز
هم از پهنای باند استفاده می‌کند. این معمولاً‌ برای سمت کارساز سخت یا
ناممکن است که به درستی و با سطح بالایی از اطمینان بداند که یک منبع آیا به فشار
نیاز دارد یا خیر.
# World 9 — TiTi Strategic Advisory Ledger Index

این پوشه حافظه بیرونی و عمومیِ **غیرکاننیکال** برای continuity فکری TiTi است.

## لینک ثابت آخرین گزارش

`advisory/titi/TITI_LATEST_FA.md`

نسخه raw عمومی بعد از merge روی main:

`https://raw.githubusercontent.com/saeedfaai/World-9/main/advisory/titi/TITI_LATEST_FA.md`

## قانون استفاده

- همیشه `TITI_LATEST_FA.md` را کامل بخوان.
- اگر به durable source زنده دسترسی داری، source برنده است.
- اگر نداری، در تحلیل بنویس `LEDGER-BASED ONLY`.
- این دفتر Task / Permit / Admission / PASS / Run Authority / Integration / Promotion / Runtime / Production authority ایجاد نمی‌کند.

## آرشیو

- [TITI_0001_FA](./archive/TITI_0001_FA.md) — آغاز مدل HOT LANE + SHELF LANE + BUILD FAN-OUT / PUBLISH FAN-IN؛ epoch 0012؛ Q1–Q6.

## پروتکل به‌روزرسانی

هر بار که HumanRoot می‌گوید **«TiTi فکرت را بنویس»**:

1. TiTi ابتدا durable source قابل‌دسترسی را fresh-check می‌کند.
2. گزارش قبلی را مرور می‌کند و تصمیم‌های superseded را مشخص می‌کند.
3. یک گزارش مفصل فارسی جدید با شماره بعدی می‌نویسد.
4. نسخه شماره‌دار در `archive/` حفظ می‌شود.
5. `TITI_LATEST_FA.md` با همان آخرین گزارش جایگزین می‌شود.
6. این `INDEX.md` یک entry جدید می‌گیرد.
7. هیچ‌کدام canonical source نمی‌شوند.

## محتوای اجباری هر گزارش

- مرور گذشته نزدیک و علت تصمیم‌ها
- source snapshot و سطح اطمینان
- وضعیت جاری پروژه
- مدل ذهنی/معماری TiTi
- تصمیم‌های ACCEPT / MODIFY / REJECT
- critical path
- safe parallel work / shelf opportunities
- ریسک‌های معماری و raceها
- سؤال‌های باز برای مشاوران
- برنامه حرکت‌های بعدی
- ADRهای جدید یا superseded
- reminder ثابت: `Candidate != Bug Gate PASS != Integration != Promotion != Runtime != Production`

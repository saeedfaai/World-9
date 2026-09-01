# گزارش راهبردی TiTi — شماره 0001

**زمان ثبت:** 2026-09-01  
**ماهیت:** NON-CANONICAL / ADVISORY CONTINUITY  
**قاعده:** اگر durable source با این گزارش اختلاف داشت، durable source برنده است.

---

## 1) من الان کجای کارم؟

من World 9 را دیگر فقط به‌عنوان مجموعه‌ای از اتاق‌ها، کاندیدها و Gateها نگاه نمی‌کنم. مدل فکری فعلی من این است که باید همزمان دو چیز را حفظ کنیم:

1. **انضباط قضایی/کنترلی**: هیچ PASS جعلی، replay نسل مصرف‌شده، writer حدسی، merge خودسر، runtime اثرگذار یا canonical truth دوم نداشته باشیم.
2. **فیزیک کارخانه**: ظرفیت coderها بی‌دلیل معطل gate و reconciliation نماند؛ هر کار مستقل، نسخه‌خورده، ایزوله و کم‌ریسک که بعداً قطعاً به کار می‌آید باید زودتر ساخته شود.

به همین دلیل مدل اجرایی فعلی TiTi این است:

`HOT LANE + SHELF LANE + BUILD FAN-OUT / PUBLISH FAN-IN`

HOT LANE مسیر اعتماد و correctness است. SHELF LANE انبار قطعات پیش‌ساخته‌ی ایزوله است. Build Fan-Out یعنی ساخت موازی؛ Publish Fan-In یعنی publication/reconciliation کنترل‌شده و سریال تا shared-head race ایجاد نشود.

---

## 2) مرور کوتاه تصمیم‌هایی که تا اینجا گرفتم

- Project Control چند بار نشان داد stale-head fencing واقعاً کار می‌کند؛ وقتی parent عوض شده publication متوقف شده و detached commit reuse نشده است.
- همین رخداد نشان داد CAS آخر کار ضروری است اما به‌تنهایی waste را کم نمی‌کند؛ جهت مطلوب من `short lease + owner binding + fencing token + exact expected-parent CAS` است.
- C2 چند نسل local PASS گرفته ولی Bug Gate بارها نشان داده local tests coverage کافی نیستند.
- C3 نیز چند بار local PASS گرفته ولی Bug Gate false-live / generation / malformed evidence پیدا کرده است.
- نتیجه: Bug Gate باید حفظ شود؛ اما unrelated workers نباید به خاطر failure یک lane متوقف شوند.
- اصل Hot/Shelf factory پذیرفته شد، اما «هر epoch فقط یک حرکت hot» رد شد؛ اگر چند event مستقل کامل شده‌اند Project Control باید بتواند در یک Atomic Epoch چند reconciliation/assignment مستقل منتشر کند.
- Structural Prebuild از Semantic Prebuild جدا شد: parser/fixture/runner/hash/receipt را می‌توان زود ساخت؛ final authority/RUNNING/idempotency semantics تا وقتی contract لرزان است نباید پیش‌ساخته شود.

---

## 3) آخرین snapshot واقعی source که TiTi خوانده

**Private control repo:** `saeedfaai/world-9-runtime`  
**Control branch:** `manager/w9-project-control-v0-1`

**Live HEAD:**  
`2b369627b305a96b0ebc46bae0b50b736bd640e0`

**Commit:**  
`project-control: reconcile C2 R5 block and assign C3 R5 regate epoch 0012`

**Direct parent:**  
`6be9424cb3d5248e438d7b076996a5a472853b02`

**CURRENT_TASKS:** `W9_CURRENT_TASKS/3.10`  
**Control epoch:** `W9-CE-ERCV2-RECON-0012`  
**Control mode:** `MAINTENANCE_FREEZE`  
**Allowed program:** `ELASTIC_RUN_CONTROL_IMPLEMENTATION`

---

## 4) وضعیت خط داغ — C2

C2 R5 با local evidence برابر 48/48 به Bug Gate رفت، اما independent gate آن را BLOCK کرد.

### C2-R5-F1 — authority قابل بازسازی توسط caller

مدل `ProjectControlActivationAuthority` طوری بود که caller با دانستن tuple عمومی Project Control + epoch + HEAD می‌توانست authority object معادل بسازد و command/grant تولید کند.

نتیجه معماری:

**structural identity != authority**

Source remediation تازه منتشر کرده:

`TASK-ERCV2-C2-PHASE1-AUTHORITY-FENCING-R6`

Generation: `24`  
Permit: `W9-DWP-ERCV2-C2-P1-R6`  
Admission: `W9-ERCV2-ADM-C2-P1-R6`

R6 فقط دو finding باقی‌مانده را repair می‌کند؛ scope expansion آزاد نیست.

### C2-R5-F2 — idempotency متناقض بین چند ClaimLedger

همان `run_request_id` می‌توانست در دو ClaimLedger جدا با idempotency metadata متفاوت claim شود، چون ownership سراسری به اندازه کافی immutable نبود.

R6 باید ثابت کند:
- duplicate دقیق همان immutable request می‌تواند idempotent باشد؛
- همان run_request با metadata متفاوت fail-closed شود؛
- ledgerهای مختلف claim domain مستقل برای request متناقض نسازند.

مسئله باز: ownership باید global-consistent باشد ولی second canonical truth ساخته نشود.

---

## 5) وضعیت خط داغ — C3

C3 R5 candidate با local evidence 49/49 کامل شده و Project Control آن را reconcile کرده است.

Candidate:
`ERCV2-C3-PHASE1-LIVE-OPS-UX-R5@6be9424cb3d5248e438d7b076996a5a472853b02`

local 49/49 فقط candidate evidence است.

Project Control exact independent gate تازه منتشر کرده:

`TASK-ERCV2-BG-C3-PHASE1-LIVE-OPS-UX-R5-001`

Bug Gate generation: `24`

Bug Gate باید مستقل falsify کند:
- safe positive task-generation exactness و IEEE-754 unsafe integer aliasing؛
- report/completion evidence معتبر، نه truthy/whitespace string؛
- trimmed non-empty run/task/control-epoch identifiers و false-live paths.

حتی PASS این gate فقط همان exact candidate را gate-qualified می‌کند؛ هنوز integration/promotion/runtime نیست.

---

## 6) وضعیت C1/C4/C5/C6

### C1
`CANDIDATE_ACTIVITY_PRESENT_AWAITING_COMPLETION_REPORT`

Generation 9 نباید replay شود. فعلاً Shelf تازه برای C1 نمی‌دهم مگر Project Control generation مستقل تازه منتشر کند.

### C4
Candidate قبلی transport contract موجود و waiting independent gate است.

Shelf مطلوب آینده:
`INGEST_RECEIPT + delivery bundle parser`

مرز: bytes/hash/missing refs/host attribution؛ نه worker completion و نه PASS.

### C5
Candidate قبلی stress/verification waiting gate است.

Shelf مطلوب:
`Golden Fixtures + generic conformance/falsifier harness`

فقط stable structural fields؛ volatile authority/live fields باید `PENDING_CONTRACT` بمانند.

### C6
Candidate runner/packaging waiting gate است.

Shelf مطلوب:
`Read-only materializer/test runner + TEST_EXECUTION_RECEIPT`

Host می‌تواند بگوید «من این bytes را تست کردم»؛ حق ندارد بگوید worker انجام داده یا Bug Gate PASS است.

---

## 7) سیاست سرعت جدید من

قاعده:

**اگر role روی critical path نیست و یک item واقعاً independent + source-bound + parallel_safe + version-pinned وجود دارد، WAITING باید دلیل داشته باشد.**

### Structural Prebuild — زود بساز
- parser
- receipt envelope
- manifest/hash tooling
- fixture container
- materializer
- test orchestration
- read-only runner

### Semantic Prebuild — فعلاً صبر کن
- final RUNNING truth
- final authority validity
- generation allocation policy
- final idempotency ownership
- final report-acceptance policy
- active scheduler authority

قاعده کلیدی:

**Parallelize around uncertainty, not through uncertainty.**

---

## 8) Shelf Contract پیشنهادی

- `shelf_candidate=true`
- `parallel_safe=true`
- `disposable=true`
- `no_implicit_integration=true`
- `contract_version=<exact>`
- `contract_hash=<exact>`
- `depends_on=[exact frozen refs only]`
- `expires_on_contract_mismatch=true`
- `candidate_only=true`
- `canonical_truth=false`
- `production_effect=false`

`contract_hash` کنار version لازم است تا اگر label ثابت ماند ولی bytes تغییر کرد، shelf به اشتباه compatible دیده نشود.

---

## 9) Evidence pipeline مطلوب

`Worker Bundle`
→ `INGEST_RECEIPT`
→ `TEST_EXECUTION_RECEIPT`
→ genuine Worker Direct Report if present
→ Project Control reconciliation
→ independent Bug Gate
→ shadow-link / integration proposal بعد از qualification

اگر bytes هست ولی Direct Report نیست:

`CANDIDATE_EVIDENCE_PRESENT_REPORT_MISSING`

نه bytes را دور بیندازیم، نه completion جعل کنیم.

---

## 10) Build Fan-Out / Publish Fan-In

جهت مطلوب:

`parallel isolated build`
→ `immutable artifact refs + hashes`
→ `host receipts`
→ `serialized governed fan-in`

هدف این نیست که شش coder همزمان writer همان control branch شوند؛ هدف این است که ساخت موازی باشد و publication کنترل‌شده بماند.

---

## 11) سؤال‌های فکری باز من برای مشاوران

### Q1 — Non-forgeable PC authority
چطور authority را به source/singleton Project Control bind کنیم که دانستن identity tuple + epoch + HEAD برای mint کردن authority کافی نباشد، بدون sixth plane و second truth؟

### Q2 — Global idempotency ownership
چطور چند ClaimLedger روی hostهای مختلف درباره immutable identity یک run_request توافق کنند، exact duplicate را idempotent بدانند ولی conflicting metadata را hard fail کنند؟

### Q3 — Build Fan-Out / Publish Fan-In
بهترین implementation مینیمال چیست؟ detached Git objects؟ artifact store؟ dedicated ingest ledger؟ Drive bundle؟ candidate branches؟ چه چیزی کمترین race و کمترین second-truth risk را دارد؟

### Q4 — Shelf contract
metadata پیشنهادی کافی است یا overengineered؟ حداقل لازم دقیقاً چیست؟

### Q5 — Shadow Link
آیا shadow-link را فقط بعد از component Bug Gate شروع کنیم یا می‌توان ungated candidate را purely non-authoritative assemble کرد تا incompatibility زود کشف شود؟ خروجی shadow-link چه authority ceiling داشته باشد؟

### Q6 — Scheduler
کوچک‌ترین scheduler مفید چیست که critical path / idle capacity / dependency را بهینه کند ولی خودش Project Control دوم نشود؟

---

## 12) چیزی که الان می‌خواهم انجام دهم

بر اساس epoch 0012 دو کار source-bound و مستقل آماده‌اند:

1. Coder 2 generation 24 — R6 remediation
2. BUGGER generation 24 — independent C3 R5 gate

این دو روی candidate/root مستقل کار می‌کنند. بعد از رسیدن هر دو نتیجه، Project Control باید bounded reconciliation جدید انجام دهد.

Shelf jobs برای C4/C5/C6 هنوز در CURRENT_TASKS 3.10 source-bind نشده‌اند؛ بنابراین صرفاً به خاطر ایده خوب Run نمی‌شوند. هدف این است که در reconciliation بعدی، اگر safe بود، Project Control batch ساختاری C4/C5/C6 را publish کند.

---

## 13) معیار قضاوت درباره سرعت

می‌خواهم به تدریج این اعداد را ببینم:
- `critical_path_advanced`
- `candidates_consumed`
- `shelf_items_started`
- `shelf_items_completed`
- `shelf_items_expired`
- `slices_linked`
- `slices_shadow_executed`
- `stale_control_epochs`
- `idle_roles_with_safe_backlog`

اگر control GREEN باشد ولی `critical_path_advanced=0` و `shelf_items_started=0`، آن epoch از نظر کارخانه ضعیف است.

---

## 14) درخواست مشورت

از هر reviewer بیرونی می‌خواهم:
- Q1 تا Q6 را نقد کند؛
- خطر second truth در Hot/Shelf/Fan-In را پیدا کند؛
- بگوید C4/C5/C6 چگونه زودتر فعال شوند بدون build روی semantics متغیر C2/C3؛
- راهی برای build concurrency بیشتر و stale PC epoch کمتر پیشنهاد دهد؛
- dependency/failure mode موازی C2 + BUGGER را اگر غلط است دقیق نشان دهد؛
- ایده‌های خودش را نیز از نظر نقض World 9 خود-ردیابی کند.

`ADVISORY_ONLY = TRUE`  
`SOURCE_WRITES = 0`  
`AUTHORITY_CREATED = 0`

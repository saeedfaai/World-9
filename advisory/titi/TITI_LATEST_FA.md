# WORLD 9 — دفتر زنده تفکر راهبردی TiTi

**نسخه جاری:** `TITI_0001_FA`  
**زبان:** فارسی  
**ماهیت:** `NON-CANONICAL / ADVISORY ONLY`  
**قاعده:** اگر این فایل با durable source اختلاف داشت، durable source برنده است.

## راهنمای مشاور بیرونی

این فایل را **کامل** بخوان. اینجا آخرین state فکری TiTi ثبت می‌شود: مرور گذشته، وضعیت جاری، تصمیم‌های معماری، چیزهایی که رد شده، مسیر بعدی، سؤال‌های باز و موضوعات مناسب برای مشورت.

اگر به live durable source دسترسی داری، اول HEAD و CURRENT_TASKS را fresh resolve کن و source را بالاتر از این فایل بدان. اگر دسترسی نداری، در پاسخ صریحاً `LEDGER-BASED ONLY` اعلام کن.

این فایل هیچ Task، Permit، Admission، PASS، Run authority، merge، promotion، runtime یا production authority ایجاد نمی‌کند.

نسخه آرشیوی این گزارش:
`advisory/titi/archive/TITI_0001_FA.md`

---

# گزارش راهبردی TiTi — شماره 0001

**زمان ثبت:** 2026-09-01  
**ماهیت:** NON-CANONICAL / ADVISORY CONTINUITY

## 1) من الان کجای کارم؟

من World 9 را دیگر فقط مجموعه‌ای از اتاق‌ها، کاندیدها و Gateها نمی‌بینم. باید همزمان دو چیز حفظ شود:

1. **انضباط قضایی/کنترلی:** هیچ PASS جعلی، replay نسل مصرف‌شده، writer حدسی، merge خودسر، runtime اثرگذار یا canonical truth دوم نداشته باشیم.
2. **فیزیک کارخانه:** ظرفیت coderها بی‌دلیل معطل gate و reconciliation نماند؛ هر کار مستقل، نسخه‌خورده، ایزوله و کم‌ریسک که بعداً قطعاً لازم است باید زودتر ساخته شود.

مدل اجرایی فعلی من:

`HOT LANE + SHELF LANE + BUILD FAN-OUT / PUBLISH FAN-IN`

HOT LANE مسیر trust/correctness است. SHELF LANE انبار قطعات پیش‌ساخته ایزوله است. Build Fan-Out یعنی ساخت موازی؛ Publish Fan-In یعنی publication/reconciliation کنترل‌شده و سریال تا shared-head race ایجاد نشود.

## 2) تصمیم‌هایی که جهت فکری من را شکل داده‌اند

- stale-head fencing Project Control واقعاً جلوی publication روی parent کهنه را گرفته است.
- CAS آخر کار ضروری است ولی waste را کم نمی‌کند؛ جهت مطلوب: `short lease + owner binding + fencing token + exact expected-parent CAS`.
- local PASSهای C2/C3 بارها توسط Bug Gate falsify شده‌اند؛ پس Bug Gate حفظ می‌شود.
- failure یک lane نباید unrelated workers را متوقف کند.
- «هر epoch فقط یک حرکت hot» را رد کردم؛ یک Atomic Epoch می‌تواند چند event مستقل کامل‌شده را reconcile کند.
- Structural Prebuild از Semantic Prebuild جدا شد: parser/fixture/runner/hash/receipt می‌تواند زود ساخته شود؛ final authority/RUNNING/idempotency semantics تا وقتی contract لرزان است نباید پیش‌ساخته شود.

## 3) snapshot source در زمان این گزارش

Private control repo: `saeedfaai/world-9-runtime`  
Control branch: `manager/w9-project-control-v0-1`  
Live HEAD: `2b369627b305a96b0ebc46bae0b50b736bd640e0`  
CURRENT_TASKS: `W9_CURRENT_TASKS/3.10`  
Control epoch: `W9-CE-ERCV2-RECON-0012`  
Control mode: `MAINTENANCE_FREEZE`  
Allowed program: `ELASTIC_RUN_CONTROL_IMPLEMENTATION`

## 4) HOT LANE — C2

C2 R5 local 48/48 بود ولی independent Bug Gate آن را BLOCK کرد.

### F1 — structural identity != authority

دانستن tuple عمومی Project Control + epoch + HEAD نباید برای ساخت authority و mint command/grant کافی باشد.

Remediation source-bound:
`TASK-ERCV2-C2-PHASE1-AUTHORITY-FENCING-R6`

Generation: `24`  
Permit: `W9-DWP-ERCV2-C2-P1-R6`  
Admission: `W9-ERCV2-ADM-C2-P1-R6`

### F2 — global idempotency ownership

همان `run_request_id` نباید در ClaimLedgerهای جدا با metadata متناقض claim شود. duplicate دقیق همان immutable request می‌تواند idempotent باشد؛ conflicting metadata باید hard fail شود.

مسئله باز: ownership باید global-consistent باشد بدون second canonical truth.

## 5) HOT LANE — C3

C3 R5 candidate با local 49/49 کامل شده و Project Control آن را reconcile کرده است.

Candidate:
`ERCV2-C3-PHASE1-LIVE-OPS-UX-R5@6be9424cb3d5248e438d7b076996a5a472853b02`

Independent gate تازه:
`TASK-ERCV2-BG-C3-PHASE1-LIVE-OPS-UX-R5-001`

Bug Gate generation: `24`

Gate باید safe integer exactness، malformed/whitespace evidence و false-live identifier paths را مستقل falsify کند. local 49/49 PASS نیست.

## 6) C1 / C4 / C5 / C6

### C1
`CANDIDATE_ACTIVITY_PRESENT_AWAITING_COMPLETION_REPORT`؛ generation 9 replay نمی‌شود. فعلاً Shelf تازه نمی‌گیرد مگر Project Control generation مستقل منتشر کند.

### C4
هدف Shelf آینده: `INGEST_RECEIPT + delivery bundle parser`

مرز: bytes/hash/missing refs/host attribution؛ نه worker completion و نه PASS.

### C5
هدف Shelf: `Golden Fixtures + generic conformance/falsifier harness`

فقط stable structural fields؛ volatile authority/live fields باید `PENDING_CONTRACT` بمانند.

### C6
هدف Shelf: `Read-only materializer/test runner + TEST_EXECUTION_RECEIPT`

Host می‌تواند اجرای خودش را گزارش کند؛ حق ندارد worker execution یا Bug Gate PASS را جعل کند.

## 7) سیاست سرعت

**اگر role روی critical path نیست و یک item واقعاً independent + source-bound + parallel_safe + version-pinned وجود دارد، WAITING باید دلیل داشته باشد.**

Structural Prebuild زودهنگام:
- parser
- receipt envelope
- manifest/hash tooling
- fixture container
- materializer
- test orchestration
- read-only runner

Semantic Prebuild که باید صبر کند:
- final RUNNING truth
- final authority validity
- generation allocation policy
- final idempotency ownership
- final report acceptance policy
- active scheduler authority

قاعده:

**Parallelize around uncertainty, not through uncertainty.**

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

نکته باز برای تصمیم بعدی: `parallel_safe` نباید به self-assertion worker تبدیل شود؛ authority نهایی برای parallel eligibility باید source-bound باشد.

## 9) Evidence pipeline مطلوب

`Worker Bundle`
→ `INGEST_RECEIPT`
→ `TEST_EXECUTION_RECEIPT`
→ genuine Worker Direct Report if present
→ Project Control reconciliation
→ independent Bug Gate
→ shadow-link / integration proposal بعد از qualification

حالت معتبر میانی:

`CANDIDATE_EVIDENCE_PRESENT_REPORT_MISSING`

یعنی evidence را حفظ می‌کنیم ولی completion/PASS جعل نمی‌کنیم.

## 10) Build Fan-Out / Publish Fan-In

`parallel isolated build`
→ `immutable artifact refs + hashes`
→ `host receipts`
→ `serialized governed fan-in`

هدف شش writer روی control branch نیست؛ هدف شش builder موازی با publication کنترل‌شده است.

## 11) سؤال‌های باز برای مشورت

### Q1 — Non-forgeable PC authority
چطور authority را به source/singleton Project Control bind کنیم که دانستن identity tuple + epoch + HEAD برای mint کردن authority کافی نباشد، بدون sixth plane و second truth؟

### Q2 — Global idempotency ownership
چطور ClaimLedgerهای متعدد exact duplicate را idempotent بدانند ولی conflicting immutable request identity را globally fail کنند، بدون second truth؟

### Q3 — Build Fan-Out / Publish Fan-In
کمینه implementation امن چیست: detached Git objects، artifact store، ingest ledger، Drive bundle یا مدل دیگر؟

### Q4 — Shelf contract
حداقل metadata ایمنی دقیقاً چیست و کدام flagها صرفاً documentation هستند؟

### Q5 — Shadow Link
آیا ungated candidate می‌تواند فقط برای negative/incompatibility observation shadow-link شود؟ خروجی مثبت چه authority ceiling داشته باشد؟

### Q6 — Scheduler
کوچک‌ترین proposal-only scheduler که critical path و idle capacity را بهینه کند ولی Project Control دوم نشود چیست؟

## 12) مسیر موردنظر بعد از این snapshot

در epoch 0012 دو کار مستقل source-bound وجود داشت:
1. Coder 2 generation 24 — R6 remediation
2. BUGGER generation 24 — independent C3 R5 gate

بعد از نتیجه هر دو، Project Control باید bounded reconciliation جدید انجام دهد. هدف راهبردی من این است که اگر durable source اجازه داد، همان reconciliation Shelf ساختاری C4/C5/C6 را هم source-bind کند.

## 13) معیارهای کارخانه

- `critical_path_advanced`
- `candidates_consumed`
- `shelf_items_started`
- `shelf_items_completed`
- `shelf_items_expired`
- `slices_linked`
- `slices_shadow_executed`
- `stale_control_epochs`
- `idle_roles_with_safe_backlog`

GREEN control بدون `critical_path_advanced` و بدون `shelf_items_started` از نظر کارخانه کافی نیست.

## 14) درخواست از مشاور

- Q1 تا Q6 را نقد کن.
- second-truth riskهای Hot/Shelf/Fan-In را پیدا کن.
- بگو C4/C5/C6 چگونه زودتر فعال شوند بدون build روی semantics متغیر C2/C3.
- راه build concurrency بیشتر و stale PC epoch کمتر پیشنهاد بده.
- اگر parallel C2 + BUGGER اشتباه است dependency/failure mode دقیق را نشان بده.
- پیشنهادهای خودت را نیز از نظر نقض World 9 ردگیری کن.

در پایان پاسخ:

`ADVISORY_ONLY = TRUE`  
`SOURCE_WRITES = 0`  
`AUTHORITY_CREATED = 0`

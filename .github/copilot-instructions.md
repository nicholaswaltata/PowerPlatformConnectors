# Quickstart for AI coding agents

This repository is Microsoft Power Platform Connectors — a large collection of connector packages (custom, certified, independent) plus templates, schemas and tools. Use this guide to become productive quickly.

1) Big picture
- Connectors are independent units under `custom-connectors/`, `certified-connectors/`, and `independent-publisher-connectors/`.
- Each connector package is expected to contain three core files: an OpenAPI (Swagger v2) spec (e.g. `apiDefinition.swagger.json`), an `apiProperties.json`, and a `README.md` with usage and OAuth setup.
- Schemas and validators that define project rules live in `schemas/` (notably `schemas/apiDefinition.swagger.schema.json` and `schemas/paconn-apiProperties.schema.json`). CI uses these to validate PRs.

2) Important project conventions (discoverable and enforced)
- `independent-publisher-connectors` **must** set `iconBrandColor` in `apiProperties.json` to `"#da3b01"`.
- Certified connector changes target `dev` branch first; `master` is updated by the certification process.
- PR titles for independent publishers should follow the pattern: `Connector Name (Independent Publisher)` to help CI reviewers and automation.

3) Connector structure examples
- See `custom-connectors/AzureKeyVault/Readme.md` for a typical connector layout and OAuth instructions.
- Templates are under `templates/` (readme + deployment templates); use these when adding new connectors.

4) Validation, CI and breaking-change rules
- The repo CI runs a **Swagger Validator** and a **Breaking Change Detector** on PRs. PRs that fail these checks should be fixed before merging.
- Response schemas should be explicit where possible; ambiguous/missing response schemas are common causes for CI failures.
- There is no reliable local validator provided in the repo; rely on CI messages for final validation. If you need local checks, inspect the validator configuration under `tools/` and `scripts/`.

5) Developer workflows (how to be effective)
- When modifying a connector, update the three required files and run CI via a PR — CI is the authoritative validator.
- For certified connectors: branch from `dev`, open PR to `dev`; maintainers handle promotion to `master`.
- Breaking changes: be conservative. If changing operationIds, paths, or response schemas, add notes to the connector README and explain rationale in the PR.

6) Integration points & cross-component patterns
- Connectors are validated against the JSON schemas in `schemas/` and use common templates from `templates/`.
- Many automation scripts and helpers live in `tools/` and `scripts/` — inspect these before adding new automation.

7) Where to look for examples & quick checks
- Connector example: `custom-connectors/AzureKeyVault/Readme.md`.
- Schema rules: `schemas/apiDefinition.swagger.schema.json` and `schemas/paconn-apiProperties.schema.json`.
- Readme templates: `templates/certified-connectors/readme.md` and `templates/Independent Publisher/readme.md`.

8) What agents should not assume
- Do not assume a runnable local validator or a fixed local build/test command — CI is authoritative and may run additional checks not present locally.
- Avoid making unilateral changes to schema rules or CI workflows; those are centralized and affect all connectors.

9) Common tasks examples (short)
- Add a connector: copy a template from `templates/`, populate `apiDefinition.swagger.json`, `apiProperties.json`, `README.md`, then open PR.
- Fix a validator error: check the schema in `schemas/` that corresponds to the failure and update the connector's OpenAPI/props to comply.

If any part of this file is unclear or you want more examples (e.g. a completed connector commit walk-through), tell me which area and I will expand it.
## Quickstart for AI coding agents

Bu repo Microsoft Power Platform Connectors projesidir — büyük bir koleksiyon "connectors" (custom, certified, independent) ve ilgili şablon/şema/tool'ları içerir. Aşağıdaki yönergeler, bir AI ajanının hızlıca üretken olması için keşfedilebilir ve uygulanabilir bilgiler sağlar.

### Repository ana hatları
- **Büyük yapı:** üç ana ürün alanı: `custom-connectors/`, `certified-connectors/`, `independent-publisher-connectors/`.
- **Her connector klasörü** tipik olarak: bir OpenAPI/Swagger dosyası (ör. `apiDefinition.swagger.json`), bir API properties dosyası (ör. `apiProperties.json`) ve bir `README.md` içerir.
- **Şablonlar ve şemalar:** `templates/` örnek readme ve deploy şablonları; `schemas/` JSON şemaları (özellikle `schemas/apiDefinition.swagger.schema.json` ve `schemas/paconn-apiProperties.schema.json`) proje doğrulamasının kaynağıdır.

### Neden böyle yapılandırıldı
- Connector paketleri bağımsız dağıtılabilir birimlerdir; OpenAPI + properties + README üçlüsü sayesinde otomatik doğrulama, CI ve sertifikasyon süreçleri çalışır.

### Kritik kurallar ve konvansiyonlar (kesin)
- `independent-publisher-connectors` için `iconBrandColor` zorunludur ve değeri `"#da3b01"` olmalıdır (apiProperties içinde).
- Certified connector değişiklikleri önce `dev` branch'e gönderilir; `master`'a geçiş sertifikasyon süreci ve takım tarafından yapılır.
- PR başlığı: bağımsız yayıncılar için önerilen biçim örneği: `Connector Name (Independent Publisher)`.
- Her PR CI'da **Swagger Validator** ve **Breaking Change Detector** çalışır; PR'lar validator uyarı/hatalarını çözmeden kabul edilmez.

### Dosya / içerik beklentileri
- Zorunlu dosyalar per-connector: OpenAPI (v2 swagger) + API properties + `README.md` (kullanım, oauth adımları, örnek flow'lar). Örnek: `custom-connectors/AzureKeyVault/Readme.md`.
- `README.md` içinde OAuth gerektiren connector'lar için adım adım uygulama oluşturma ve izin talimatı sağlanmalı — sertifikasyon ekibi bu adımları kullanır.
- Response şemaları mümkün olduğunca açık olmalı; dinamik olmayan cevaplarda schema eklenmelidir (Breaking Change Detector buna bakar).

### Geliştirici iş akışları ve komutlar (elde edilen bilgiler)
- Fork → feature branch → PR (certified için `dev` branch hedeflenir). `git fetch upstream` + `git merge upstream/master` kullanılarak güncel tutulur (README.md'de örnek komutlar vardır).
- CI doğrulamaları otomatik; yerelde özel validator yoksa PR üzerinden çıkan hatalara göre düzeltme yapılır. (Repo README, Swagger Validator ve Breaking Change Detector hakkında bilgi içerir.)

### Örnek dosya referansları (hızlı kontrol noktaları)
- Şema ve validator kuralları: `schemas/apiDefinition.swagger.schema.json`, `schemas/paconn-apiProperties.schema.json`.
- Readme şablonları: `templates/certified-connectors/readme.md`, `templates/Independent Publisher/readme.md`.
- Connector örneği: `custom-connectors/AzureKeyVault/Readme.md`.

### Neden otomatik değişiklik yaparken dikkatli olmalı?
- Bir connector Swagger'ını veya API properties'i değiştirmek geriye dönük uyumluluğu bozabilir — Breaking Change Detector bunu işaretler. Değişiklikleri minimal tutun ve response schema/operation id değişikliklerini açıkça belgeleyin.

### İletişim / doğrulama notları
- Bilinmeyen veya eksik: yerel geliştirme araçları veya özel CI adımları (ör. validator'ın local runner'ı) repoda açıkça bulunmuyor; bu yüzden PR CI çıktıları en güvenilir doğrulama kaynağıdır.

---
Eğer isterseniz, bu taslağı sizin onayınıza göre güncelleyip daha fazla örnek (örneğin popüler bir connector klasörünün tam dosya listesi) eklerim.

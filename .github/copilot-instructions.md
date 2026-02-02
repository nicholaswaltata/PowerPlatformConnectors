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

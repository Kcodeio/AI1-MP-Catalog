# ⚡ AI1 - Modüler Masaüstü Çalışma İstasyonu & Eklenti Platformu

<p align="center">
  <img src="assets/icon.png" alt="AI1 Logo" width="128" height="128">
</p>

<p align="center">
  <b>Python ve CustomTkinter tabanlı; dinamik modül mimarisi, izin tabanlı güvenlik katmanı ve entegre topluluk mağazası barındıran masaüstü platformu.</b>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows-blue?style=flat-square&logo=windows" alt="Platform">
  <img src="https://img.shields.io/badge/Python-3.11+-3776AB?style=flat-square&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/GUI-CustomTkinter-blueviolet?style=flat-square" alt="GUI">
  <img src="https://img.shields.io/badge/Paket_Formatı-.aio-success?style=flat-square" alt="Package Format">
  <img src="https://img.shields.io/badge/Lisans-MIT-green?style=flat-square" alt="License">
</p>

---

## 📌 Genel Bakış

**AI1**, kullanıcıların bağımsız araçları tek bir çatı altında çalıştırmasını, yönetmesini ve geliştirmesini sağlayan modüler bir masaüstü çalışma istasyonudur. Sıradan masaüstü araçlarının aksine AI1; dinamik paket yükleme motoru, Android benzeri açık izin (permission) modeli, doğrudan GitHub tabanlı eklenti mağazası ve Windows dosya ilişkilendirme altyapısı sunar.

---

## ✨ Temel Özellikler

- **📦 `.aio` Modül Formatı:** Eklentiler, Base64 şifreli ve sıkıştırılmış tek parça `.aio` arşivleri halinde paketlenir ve dağıtılır.
- **🖱️ Windows Çift Tıklama Desteği (File Association):** Sistemdeki herhangi bir `.aio` dosyasına çift tıklandığında AI1 doğrudan devreye girer ve kurulum ekranını açar.
- **🛡️ İzin Tabanlı Güvenlik Katmanı:** Eklentiler ağa bağlanma, dosya indirme veya çekirdeğe müdahale etme gibi kritik yetkileri manifest üzerinde açıkça talep etmek zorundadır. Yetkisiz işlemler `SecurityPermissionError` ile engellenir.
- **🛍️ Entegre Eklenti Mağazası (Marketplace):** [Kcodeio/AI1-MP-Catalog](https://github.com/Kcodeio/AI1-MP-Catalog) deposu üzerinden modülleri listeleyin, arayın ve tek tıkla kurun.
- **🔄 Çoklu Sürüm ve Otomatik Güncelleme:** Eklentilerin geçmiş veya güncel sürümlerini dropdown menüden seçip yükleyin, sürüm güncellemelerini anında takip edin.
- **🔍 Gelişmiş Filtreleme:** Eklentileri kategoriye (Verimlilik, Araçlar, Güvenlik vb.) veya geliştiriciye (Creator) göre anlık filtreleyin.
- **🔒 Tek Örnek (Single-Instance) Kilidi:** Uygulama açıkken yeni `.aio` dosyaları açıldığında birden fazla kopya başlatılmaz, mevcut oturum üzerinden yönetilir.
- **🚨 Dahili Sistem Koruması:** İzinsiz müdahaleleri algılayan çekirdek nöbetçi alarmı ve tam ekran şifreli kilit mekanizması.

---

## 🔒 Güvenlik & İzin Matrisi

Modüller `manifest.json` dosyasında belirttikleri izin sınırları içinde çalışır:

| İzin | Tanım | Yetkilendirilen API Çağrısı |
| :--- | :--- | :--- |
| `network:connect` | Dış ağlara HTTP/HTTPS istekleri veya TCP soket bağlantıları açar. | `api.fetch_url()`, `api.create_socket()` |
| `filesystem:download` | İnternetten modül dizinine dosya indirir. | `api.download_file()` |
| `plugin:interact` | Yüklü diğer eklentilerin nesnelerine erişir veya fonksiyon enjekte eder. | `api.get_sibling_plugin()`, `api.inject_sibling_plugin()` |
| `core:inject` | AI1 ana motor olaylarına (hook) dinleyici bağlar. | `api.inject_core()` |
| `marketplace:install` | Başka bir eklenti paketini programatik olarak kurar. | `api.auto_install_aio()` |
| `marketplace:publish` | Doğrudan markete yayınlama talebi oluşturur. | `api.publish_module()` |

---

## 🛠️ Kurulum & Geliştirme Ortamı

### Gereksinimler

- Windows 10 / 11
- Python 3.11 veya üzeri

### 1. Repoyu Klonlayın

```bash
git clone [https://github.com/Kcodeio/AI1.git](https://github.com/Kcodeio/AI1.git)
cd AI1

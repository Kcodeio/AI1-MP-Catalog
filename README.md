# ⚡ AI1 - Modular Workstation Platform

<p align="center">
  <img src="assets/icon.png" alt="AI1 Logo" width="130" height="130">
</p>

<p align="center">
  <b>Python & CustomTkinter mimarisi üzerine kurulu; mikro-çekirdek modül yönetimi, granüler izin denetimi, otomatik dosya ilişkilendirmesi ve merkezi pazar yeri barındıran yeni nesil masaüstü çalışma platformu.</b>
</p>

<p align="center">
  <a href="https://github.com/Kcodeio/AI1/releases/latest"><img src="https://img.shields.io/github/v/release/Kcodeio/AI1?style=for-the-badge&color=238636&logo=github" alt="Release"></a>
  <img src="https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="Platform">
  <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/GUI-CustomTkinter-blueviolet?style=for-the-badge" alt="GUI">
  <img src="https://img.shields.io/badge/Paket-.aio%20(V2)-orange?style=for-the-badge" alt="Package">
  <a href="LICENSE"><img src="https://img.shields.io/badge/Lisans-MIT-green?style=for-the-badge" alt="License"></a>
</p>

---

## 📑 İçindekiler

- [Giriş ve Vizyon](#-giriş-ve-vizyon)
- [Hızlı Kurulum & İndirme](#-hızlı-kurulum--indirme)
- [Temel Mimari ve Çalışma Mantığı](#-temel-mimari-ve-çalışma-mantığı)
- [Öne Çıkan Özellikler](#-öne-çıkan-özellikler)
- [Güvenlik ve İzin (Permission) Katmanı](#-güvenlik-ve-izin-permission-katmanı)
- [Kapsamlı PluginAPI Referansı](#-kapsamlı-pluginapi-referansı)
- [Adım Adım Eklenti Geliştirme Rehberi](#-adım-adım-eklenti-geliştirme-rehberi)
- [Mağaza & Dağıtım Mimarisi (Marketplace)](#-mağaza--dağıtım-mimarisi-marketplace)
- [Geliştirici Kurulumu (Source Build)](#-geliştirici-kurulumu-source-build)
- [Production Dağıtımı (PyInstaller & Inno Setup)](#-production-dağıtımı-pyinstaller--inno-setup)
- [Klavye Kısayolları](#-klavye-kısayolları)
- [Sıkça Sorulan Sorular (SSS)](#-sıkça-sorulan-sorular-sss)
- [Lisans & Katkıda Bulunma](#-lisans--katkıda-bulunma)

---

## 💡 Giriş ve Vizyon

Masaüstü kullanıcıları ve geliştiriciler genellikle not tutma, ağ araçları, sistem izleyicileri, API test araçları veya özel betikler için onlarca bağımsız uygulama açmak zorunda kalır. **AI1**, bu araç kirliliğini ortadan kaldırmak için tasarlandı.

AI1; işletim sistemini yormayan, dinamik bellek yönetimine sahip, genişletilebilir bir platformdur. Kullanıcılar yalnızca ihtiyaç duydukları araçları entegre mağazadan indirir; her araç izole bir modül olarak çalışır, çekirdek kaynakları korur ve güvenli bir sandboxing prensibiyle işletim sistemiyle haberleşir.

---

## 📥 Hızlı Kurulum & İndirme

AI1, Windows ortamı için iki farklı dağıtım modeliyle sunulur:

<p align="center">
  <a href="[https://github.com/Kcodeio/AI1/releases/latest/download/AI1_Setup_v1.0.0.exe](https://github.com/Kcodeio/AI1-MP-Catalog/releases/download/setup/AI1_Setup_v1.0.0.exe)">
    <img src="https://img.shields.io/badge/Windows%20Setup-Kurulum%20Sihirbazı%20(.exe)-238636?style=for-the-badge&logo=windows&logoColor=white" alt="Setup İndir">
  </a>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <a href="[https://github.com/Kcodeio/AI1/releases/latest/download/AI1.zip](https://github.com/Kcodeio/AI1-MP-Catalog/releases/download/source/AI1.zip)">
    <img src="https://img.shields.io/badge/Taşınabilir-Portable%20(.zip)-1f6feb?style=for-the-badge&logo=archive&logoColor=white" alt="Zip İndir">
  </a>
</p>

| Paket | Format | Boyut | Özellikler |
| :--- | :--- | :--- | :--- |
| **Inno Setup Installer** *(Önerilen)* | `.exe` | ~25 MB | Otomatik `.aio` dosya ilişkilendirmesi, masaüstü simgesi, Windows başlangıç kaydı, temiz kaldırma (uninstaller). |
| **Portable Zip** | `.zip` | ~30 MB | Kurulum gerektirmez, doğrudan USB veya yerel klasörden çalışır, bağımsızdır. |

> ℹ️ *Eski sürümlere, ek varlıklara ve sürüm değişiklik loglarına [GitHub Releases](https://github.com/Kcodeio/AI1/releases) sayfasından ulaşabilirsiniz.*

---

## 🏛️ Temel Mimari ve Çalışma Mantığı

AI1, **Mikro-Çekirdek (Microkernel)** tasarım kalıbını benimser:

```text
┌─────────────────────────────────────────────────────────────┐
│                      AI1 Çekirdek (GUI)                     │
│        (CustomTkinter Engine, AppUserModelID, Single-Instance)        │
└──────────────┬───────────────────────────────┬──────────────┘
               │                               │
       ┌───────▼────────┐             ┌────────▼───────┐
       │ AI1Engine Core │             │ ModuleLoader   │
       │  (Event Bus)   │             │ (Dynamic Spec) │
       └───────┬────────┘             └────────┬───────┘
               │                               │
               ├───────────────────────────────┤
               │                               │
       ┌───────▼────────┐             ┌────────▼───────┐
       │ Security Gate  │             │ AIOInstaller   │
       │ (Permission)   │             │ (.aio unpack)  │
       └───────┬────────┘             └────────┬───────┘
               │                               │
   ┌───────────┴───────────────────────────────┴───────────┐
   │                  PluginAPI Katmanı                    │
   ├───────────────────┬───────────────────┬───────────────┤
   │ 📝 quick_notes    │ 🌐 net_monitor    │ 🔧 custom_mod │
   └───────────────────┴───────────────────┴───────────────┘

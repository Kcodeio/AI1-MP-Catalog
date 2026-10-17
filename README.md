# ⚡ AI1 - Modular Workstation Platform WE ARE NEW V1.0.1 WE ADDED LANGUAGE SUPPORT

<p align="center">
  <img src="assets/icon.png" alt="AI1 Logo" width="130" height="130">
</p>

<p align="center">
  <b>A next-generation desktop workstation built on Python & CustomTkinter, featuring microkernel module management, granular permission control, automatic file associations, and a centralized marketplace.</b>
</p>

<p align="center">
  <a href="https://github.com/Kcodeio/AI1/releases/latest"><img src="https://img.shields.io/github/v/release/Kcodeio/AI1?style=for-the-badge&color=238636&logo=github" alt="Release"></a>
  <img src="https://img.shields.io/badge/Platform-Windows%2010%20%7C%2011-0078D6?style=for-the-badge&logo=windows&logoColor=white" alt="Platform">
  <img src="https://img.shields.io/badge/Python-3.11%2B-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/GUI-CustomTkinter-blueviolet?style=for-the-badge" alt="GUI">
  <img src="https://img.shields.io/badge/Package-.aio%20(V2)-orange?style=for-the-badge" alt="Package">
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License"></a>
</p>

---

## 📑 Table of Contents

- [Introduction & Vision](#-introduction--vision)
- [Quick Download & Installation](#-quick-download--installation)
- [Architecture & Core Concepts](#-architecture--core-concepts)
- [Key Features](#-key-features)
- [Security & Permission Layer](#-security--permission-layer)
- [PluginAPI Reference](#-pluginapi-reference)
- [Plugin Development Guide](#-plugin-development-guide)
- [Marketplace & Distribution](#-marketplace--distribution)
- [Developer Setup (Source Build)](#-developer-setup-source-build)
- [Production Deployment (PyInstaller & Inno Setup)](#-production-deployment-pyinstaller--inno-setup)
- [Keyboard Shortcuts](#-keyboard-shortcuts)
- [FAQ](#-faq)
- [License & Contributing](#-license--contributing)

---

## 💡 Introduction & Vision

Desktop users and developers often keep dozens of standalone applications open just for taking notes, inspecting network traffic, monitoring system stats, testing APIs, or running custom utility scripts. **AI1** is designed to eliminate this workspace clutter.

AI1 is a lightweight, dynamically managed, and extensible desktop environment. Users download only the tools they need directly from the integrated marketplace; each tool runs as an isolated module, conserving core system resources and communicating with the OS through a sandboxed permission architecture.

---

## 📥 Quick Download & Installation

AI1 is distributed for Windows in two ready-to-use packages:

<p align="center">
  <a href="https://github.com/Kcodeio/AI1-MP-Catalog/releases/download/setup/AI1_Setup_v1.0.0.exe">
    <img src="https://img.shields.io/badge/Windows%20Setup-Installer%20Wizard%20(.exe)-238636?style=for-the-badge&logo=windows&logoColor=white" alt="Download Setup">
  </a>
  &nbsp;&nbsp;&nbsp;&nbsp;
  <a href="https://github.com/Kcodeio/AI1-MP-Catalog/releases/download/source/AI1.zip">
    <img src="https://img.shields.io/badge/Portable-Archive%20(.zip)-1f6feb?style=for-the-badge&logo=archive&logoColor=white" alt="Download Zip">
  </a>
</p>

| Package | Format | Size | Highlights |
| :--- | :--- | :--- | :--- |
| **Inno Setup Installer** *(Recommended)* | [AI1_Setup_v1.0.0.exe](https://github.com/Kcodeio/AI1-MP-Catalog/releases/download/setup/AI1_Setup_v1.0.0.exe) | ~25 MB | Automatic `.aio` file association, desktop shortcut, Windows startup entry, and clean uninstaller. |
| **Portable Zip** | [AI1.zip](https://github.com/Kcodeio/AI1-MP-Catalog/releases/download/source/AI1.zip) | ~30 MB | No installation required; run directly from a USB drive or any local directory. |

> ℹ️ *Previous releases, additional assets, and full changelogs are available on the [GitHub Releases](https://github.com/Kcodeio/AI1/releases) page.*

---

## 🏛️ Architecture & Core Concepts

AI1 implements a decoupled **Microkernel** architectural pattern:

```text
┌─────────────────────────────────────────────────────────────┐
│                       AI1 Core (GUI)                        │
│        (CustomTkinter Engine, AppUserModelID, Single-Instance) │
└──────────────┬───────────────────────────────┬──────────────┘
               │                               │
        ┌───────▼────────┐              ┌────────▼───────┐
        │ AI1Engine Core │              │ ModuleLoader   │
        │  (Event Bus)   │              │ (Dynamic Spec) │
        └───────┬────────┘              └────────┬───────┘
               │                               │
               ├───────────────────────────────┤
               │                               │
        ┌───────▼────────┐              ┌────────▼───────┐
        │ Security Gate  │              │ AIOInstaller   │
        │ (Permission)   │              │ (.aio unpack)  │
        └───────┬────────┘              └────────┬───────┘
               │                               │
    ┌───────────┴───────────────────────────────┴───────────┐
    │                    PluginAPI Layer                    │
    ├───────────────────┬───────────────────┬───────────────┤
    │ 📝 quick_notes    │ 🌐 net_monitor    │ 🔧 custom_mod │
    └───────────────────┴───────────────────┴───────────────┘

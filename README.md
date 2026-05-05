<!-- Language Toggle -->
<div align="center">

[![English](https://img.shields.io/badge/Language-English-blue?style=for-the-badge)](#english-documentation)
[![العربية](https://img.shields.io/badge/اللغة-العربية-green?style=for-the-badge)](#arabic-documentation)

</div>

---

<div id="english-documentation">

<div align="center">

# 🤖 WhatsApp AI Agent — n8n Multimodal Workflow

### Project #01 — AI Automation Series by Yousef ElSherbiny

[![YouTube Tutorial](https://img.shields.io/badge/▶_Watch_Full_Tutorial-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3)
[![n8n](https://img.shields.io/badge/Built_with-n8n-EA4B71?style=for-the-badge)](https://n8n.io)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT_4o_mini-412991?style=for-the-badge&logo=openai)](https://openai.com)
[![Groq](https://img.shields.io/badge/Groq-Whisper-F55036?style=for-the-badge)](https://groq.com)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)
[![Stars](https://img.shields.io/github/stars/YousefAutomates/01-whatsapp-ai-agent-n8n?style=for-the-badge&color=gold)](https://github.com/YousefAutomates/01-whatsapp-ai-agent-n8n/stargazers)

</div>

---

## 📖 Overview

A production-ready **Multimodal WhatsApp AI Agent** built entirely with **n8n** (no custom backend required).
The agent intelligently processes **3 types of messages** and executes real-world tasks using AI-powered tools.

```
WhatsApp Message
      │
      ├── 📝 Text   → AI Agent → Google Search / Send Email
      ├── 🎤 Voice  → Groq Whisper → Text → AI Agent → Execute Task  
      └── 🖼️ Image  → GPT-4o-mini Analysis → AI Agent → Answer / Price Search
```

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🎤 **Voice Understanding** | Converts voice notes to text using Groq Whisper (faster & cheaper than OpenAI) |
| 🖼️ **Image Analysis** | Analyzes any image using GPT-4o-mini or Claude and answers questions about it |
| 🔍 **Google Search** | Searches the web in real-time using SerpAPI for up-to-date information |
| 📧 **Email Automation** | Sends emails via Gmail on your behalf from a voice command |
| 📊 **Contact Lookup** | Reads contact emails from Google Sheets before sending |
| 🧠 **Conversation Memory** | Remembers last N messages per user (isolated per WhatsApp number) |
| 🔒 **Security Layer** | Phone number whitelist using If Node + environment variables |
| ♻️ **Error Handling** | Retry logic on API failures + graceful error responses |

---

## 🏗️ Workflow Architecture

```
┌─────────────────────────────────────────────────────────┐
│                   WhatsApp Trigger                      │
│              (Incoming Message Webhook)                 │
└──────────────────────┬──────────────────────────────────┘
                       │
              ┌────────▼────────┐
              │   If Node       │
              │ (Security Check)│
              │ Whitelist Phone │
              └────────┬────────┘
                       │ ✅ Authorized
              ┌────────▼────────┐
              │  Switch Node    │
              │ (Message Router)│
              └──┬──────┬───┬───┘
                 │      │   │
         ┌───────▼─┐ ┌──▼──┐ ┌▼──────────┐
         │  TEXT   │ │VOICE│ │   IMAGE   │
         │ Branch  │ │Branch│ │  Branch   │
         └───┬─────┘ └──┬──┘ └─────┬─────┘
             │          │          │
             │   ┌──────▼──────┐   │
             │   │Groq Whisper │   │
             │   │Speech→Text  │   │
             │   └──────┬──────┘   │
             │          │    ┌─────▼──────┐
             │          │    │GPT-4o-mini │
             │          │    │Image Analys│
             │          │    └─────┬──────┘
             │          │          │
         ┌───▼──────────▼──────────▼───┐
         │      Edit Fields Node       │
         │   (Unify message format)    │
         └──────────────┬──────────────┘
                        │
              ┌─────────▼─────────┐
              │     AI Agent      │
              │  (GPT-5-mini LLM) │
              │  + System Prompt  │
              └──┬──────┬──────┬──┘
                 │      │      │
          ┌──────▼─┐ ┌──▼───┐ ┌▼──────────┐
          │SerpAPI │ │Gmail │ │  Google   │
          │ Search │ │ Send │ │  Sheets   │
          └──────┬─┘ └──┬───┘ └┬──────────┘
                 │      │      │
         ┌───────▼──────▼──────▼───┐
         │   WhatsApp Send Node    │
         │  (Reply to User)        │
         └─────────────────────────┘
```

---

## 🛠️ Tech Stack

| Tool | Purpose | Why This Choice |
|------|---------|-----------------|
| **n8n** | Automation Platform | Visual workflow, self-hostable, powerful |
| **WhatsApp Business API** | Message interface | Official Meta API, reliable |
| **Groq + Whisper** | Speech-to-Text | 10x faster than OpenAI, much cheaper |
| **GPT-4o-mini** | Image Analysis | Cost-effective vision model |
| **GPT-5-mini** | AI Agent Brain | Fast reasoning, tool use |
| **SerpAPI** | Google Search | Real-time web results |
| **Gmail API** | Email Sending | OAuth2 secure, reliable |
| **Google Sheets** | Contact Database | Simple, no-DB-needed solution |

---

## 📁 Project Structure

```
01-whatsapp-ai-agent-n8n/
│
├── 📄 README.md                    # This file
├── 📄 LICENSE                      # MIT License
├── 📄 .gitignore                   # Git ignore rules
│
├── 📂 workflow/
│   └── 📄 whatsapp_ai_agent.json   # n8n Workflow (import this)
│
├── 📂 docs/
│   ├── 📄 SETUP.md                 # Step-by-step setup guide
│   ├── 📄 SYSTEM_PROMPT.md         # AI Agent system prompt template
│   └── 📄 TROUBLESHOOTING.md       # Common issues & fixes
│
├── 📂 assets/
│   └── 📄 workflow-diagram.png     # Visual workflow diagram
│
└── 📂 examples/
    └── 📄 sample_contacts.csv      # Sample Google Sheets structure
```

---

## 🚀 Quick Start

### Prerequisites
- [ ] n8n instance (Cloud or Self-Hosted)
- [ ] Meta Developer Account + WhatsApp Business API
- [ ] OpenAI API Key
- [ ] Groq API Key (free tier available)
- [ ] SerpAPI Key (free tier: 100 searches/month)
- [ ] Google Account (for Sheets + Gmail)

### Installation

**1. Import the Workflow**
```bash
# In n8n: Settings → Import Workflow
# Select: workflow/whatsapp_ai_agent.json
```

**2. Configure Credentials**
```
Required in n8n Credentials:
├── WhatsApp OAuth (from Meta Developer)
├── OpenAI API Key
├── Groq API Key (as Bearer Token)
├── SerpAPI Key
├── Google Sheets OAuth2
└── Gmail OAuth2
```

**3. Set Environment Variables**
```bash
# In n8n Variables:
phone = YOUR_WHATSAPP_NUMBER  # e.g., 201234567890
```

**4. Activate & Test**
```
Workflow → Activate → Send a WhatsApp message → Done! 🎉
```

---

## 📺 Full Tutorial

> 🎬 **Watch the complete 2+ hour step-by-step tutorial:**

[![Watch Tutorial](https://img.shields.io/badge/▶_Full_Tutorial_%7C_2hrs+-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3)

**What's covered in the video:**
- 0:00 — Live demo (Text, Voice, Image)
- 34:03 — Building from scratch
- 46:04 — Image download & authentication
- 58:56 — Voice-to-text with Groq
- 1:13:18 — AI Agent setup
- 2:14:07 — Security & error handling

---

## 🤝 Professional Automation Services

> 💼 **Need a custom automation solution for your business?**
>
> Built by **Yousef ElSherbiny** — providing professional automation services
> tailored to your business needs.
>
> [![Hire Me](https://img.shields.io/badge/🚀_Get_Professional_Automation-EA4B71?style=for-the-badge)](https://yousefautomates.pages.dev/)

---

## 📄 License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) for details.

---

<div align="center">

⭐ **If this helped you, please give it a star!** ⭐

[![Star this repo](https://img.shields.io/badge/⭐_Star_This_Repo-gold?style=for-the-badge)](https://github.com/YousefAutomates/01-whatsapp-ai-agent-n8n)

</div>

</div>

---
---

<div id="arabic-documentation" dir="rtl">

<div align="center">

# 🤖 وكيل واتساب بالذكاء الاصطناعي — سير عمل n8n متعدد الوسائط

### المشروع #01 — سلسلة أتمتة الذكاء الاصطناعي بقلم يوسف الشربيني

[![شاهد الشرح كاملاً](https://img.shields.io/badge/▶_شاهد_الشرح_كاملاً-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3)

</div>

---

## 📖 نظرة عامة

وكيل واتساب متعدد الوسائط **جاهز للإنتاج** مبني بالكامل بـ **n8n** دون الحاجة إلى خادم خلفية مخصص.
يعالج الوكيل **3 أنواع من الرسائل** بذكاء وينفذ مهام حقيقية باستخدام أدوات مدعومة بالذكاء الاصطناعي.

---

## ✨ المميزات

| الميزة | الوصف |
|--------|-------|
| 🎤 **فهم الصوت** | تحويل الرسائل الصوتية لنص باستخدام Groq Whisper |
| 🖼️ **تحليل الصور** | تحليل أي صورة بـ GPT-4o-mini والإجابة على الأسئلة |
| 🔍 **البحث في جوجل** | بحث فوري على الإنترنت باستخدام SerpAPI |
| 📧 **أتمتة الإيميل** | إرسال إيميلات عبر Gmail بأمر صوتي واحد |
| 📊 **قاعدة جهات الاتصال** | قراءة إيميلات الاتصالات من Google Sheets |
| 🧠 **ذاكرة المحادثة** | تذكر آخر N رسالة لكل مستخدم بشكل منفصل |
| 🔒 **طبقة الأمان** | قائمة بيضاء لأرقام الهاتف + متغيرات البيئة |
| ♻️ **معالجة الأخطاء** | منطق إعادة المحاولة عند فشل الـ API |

---

## 🛠️ الأدوات المستخدمة

| الأداة | الغرض |
|--------|-------|
| **n8n** | منصة الأتمتة |
| **WhatsApp Business API** | واجهة الرسائل |
| **Groq + Whisper** | تحويل الصوت لنص |
| **GPT-4o-mini** | تحليل الصور |
| **GPT-5-mini** | عقل الوكيل الذكي |
| **SerpAPI** | البحث في جوجل |
| **Gmail API** | إرسال الإيميلات |
| **Google Sheets** | قاعدة بيانات جهات الاتصال |

---

## 🚀 البدء السريع

**1. استيراد الـ Workflow**
```
في n8n: الإعدادات ← استيراد Workflow
اختر: workflow/whatsapp_ai_agent.json
```

**2. إعداد الاعتمادات**
```
المطلوب في n8n Credentials:
├── WhatsApp OAuth
├── OpenAI API Key
├── Groq API Key
├── SerpAPI Key
├── Google Sheets OAuth2
└── Gmail OAuth2
```

**3. تفعيل الـ Workflow واختباره**
```
Workflow ← تفعيل ← أرسل رسالة واتساب ← استمتع! 🎉
```

---

## 📺 الشرح الكامل على يوتيوب

> 🎬 **شاهد الشرح التفصيلي الكامل (أكثر من ساعتين):**

[![شاهد الشرح](https://img.shields.io/badge/▶_الشرح_الكامل_أكثر_من_ساعتين-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://youtu.be/4bQXpGNTSF4?si=EH2bKWULNY9oFXO3)

---

## 🤝 خدمات الأتمتة الاحترافية

> 💼 **تحتاج حلول أتمتة احترافية لعملك؟**
>
> **يوسف الشربيني** — لتقديم خدمات أتمتة احترافية
> مصممة خصيصاً لاحتياجات عملك
>
> [![تواصل معنا](https://img.shields.io/badge/🚀_تواصل_معنا_الآن-EA4B71?style=for-the-badge)](https://yousefautomates.pages.dev/)

---

<div align="center">

⭐ **إذا أفادك المشروع، أعطه نجمة!** ⭐

</div>

</div>

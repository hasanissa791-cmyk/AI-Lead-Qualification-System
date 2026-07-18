# AI Lead Qualification System

An end-to-end AI-powered automation system that qualifies incoming leads using **n8n**, **OpenRouter** (LLM), **Gmail**, **Telegram**, and **Google Sheets**.

## 📌 Problem Statement
Manually filtering and scoring leads from multiple channels is time-consuming and inconsistent. This system automates the entire process:
- Receives lead data via webhook or manual input.
- Uses an LLM (via OpenRouter) to analyze the lead’s answers, intent, and budget.
- Assigns a qualification score (Hot/Warm/Cold).
- Logs all data to Google Sheets.
- Sends real-time notifications via Telegram and summary emails via Gmail.

## 🛠️ Tech Stack
- **n8n** – Workflow orchestration
- **OpenRouter** – Access to multiple LLMs (GPT, Claude, Llama, etc.)
- **Gmail API** – Send qualification reports
- **Telegram Bot API** – Instant alerts
- **Google Sheets API** – Data storage and tracking

## 🚀 How It Works (Flow)
1. Trigger: Manual or incoming webhook (e.g., from a landing page).
2. LLM Agent: Parses lead message, extracts key fields (name, company, need, budget, timeline).
3. Scoring: Assigns a score from 0–100 and a category.
4. Actions:
   - Append row to Google Sheets.
   - Send Telegram message to the sales team.
   - (Optional) Send a detailed email to the manager.

## 📁 Repository Structure
📐 الهيكل المعماري للمشروع (Project Architecture)
1. نظرة عامة (Overview)
الاسم: نظام تأهيل العملاء المحتملين بالذكاء الاصطناعي (AI Lead Qualification System).

الوظيفة الأساسية: استقبال بيانات عميل محتمل (الاسم، الشركة، الميزانية، التحدي)، تحليلها بواسطة الذكاء الاصطناعي، ومنحها درجة (0-100)، ثم توجيهها إلى مسارين:

High (≥ 70): إرسال بريد إلكتروني + رسالة تلغرام + طلب HTTP خارجي.

Low (< 70): حفظ البيانات في Google Sheets.

قنوات التشغيل: 3 مشغلات (Manual, Webhook, Schedule).

2. هيكل البيانات الأساسي (Core Data Schema)
جميع العقد تتعامل مع كائن JSON واحد يحمل هذه المفاتيح:

الحقل	النوع	المصدر	مثال
full_name	نص	مدخلات المستخدم	"أحمد"
email	نص	مدخلات المستخدم	"ahmed@web.com"
company	نص	مدخلات المستخدم	"شركة التقنية"
website	نص (اختياري)	مدخلات المستخدم	"https://tech.com"
service	نص (اختياري)	مدخلات المستخدم	"استشارات آلية"
budget	رقم	مدخلات المستخدم	6000
challenge	نص (اختياري)	مدخلات المستخدم	"نضيع وقتاً في تأهيل العملاء"
lead_score	رقم	مستخرج من الذكاء الاصطناعي	85
summary	نص	مستخرج من الذكاء الاصطناعي	"عميل عالي القيمة بميزانية كبيرة..."
recommendation	نص	مستخرج من الذكاء الاصطناعي	"خدمة الأتمتة المتقدمة"
classification	نص	مضافة بواسطة Code	"High" أو "Low"
3. مكونات النظام (System Components)
ينقسم الوركفلو إلى 4 طبقات رئيسية:

الطبقة 1: المدخلات (Input Layer)
المشغلات:

Manual Trigger (للتطوير والاختبار).

Webhook (لاستقبال البيانات من أنظمة خارجية).

Schedule Trigger (للبيانات الوهمية/التجارب التلقائية).

محولات البيانات:

Code in JavaScript1 (تنسيق بيانات Webhook).

Code in JavaScript2 (توليد بيانات وهمية للتشغيل التلقائي).

الطبقة 2: المعالجة الذكية (Processing Layer)
دمج المدخلات: Merge (يجمع الـ 3 مشغلات في مسار واحد).

الذكاء الاصطناعي: AI Agent (يحلل النص ويستخرج الدرجة والتوصية).

استخراج النتائج: Code in JavaScript (يستخرج lead_score, summary, recommendation من نص الـ AI ويدمجها مع البيانات الأصلية).

الطبقة 3: المنطق والتوجيه (Logic Layer)
التفرع الشرطي: If (يقسم العملاء إلى مسار High أو Low بناءً على lead_score > 70).

التصفية: Filter (يزيل العناصر الفارغة قبل إرسال تلغرام).

الطبقة 4: الإجراءات والمخرجات (Action Layer)
المسار العالي:

Send a message (Gmail): إرسال بريد منسق.

Wait + Send a text message (Telegram): إرسال تنبيه متأخر 10 ثوانٍ.

HTTP Request: إرسال نسخة من البريد إلى Webhook.site (للتكامل مع أنظمة أخرى).

المسار المنخفض:

Append row in sheet (Google Sheets): حفظ البيانات.

التجميع النهائي:

Merge1 (يجمع مخرجات المسارين).

Aggregate (يحول المصفوفة إلى عنصر واحد بمفاتيح مصفوفة).

Code in JavaScript3 (يختار العنصر الصحيح ويضيف classification).

Respond to Webhook (يرد بـ JSON للمرسل الخارجي).



## ⚙️ Setup Instructions
1. Clone the repository.
2. Import `workflow.json` into your n8n instance.
3. Set up the following credentials in n8n:
   - OpenRouter API Key
   - Gmail OAuth2
   - Telegram Bot Token
   - Google Sheets Service Account
4. Adjust the prompt in the HTTP Request node (OpenRouter) to match your qualification criteria.
5. Execute the workflow.

## 📈 Future Improvements
- Add a CRM integration (HubSpot, Pipedrive).
- Support for email-based lead ingestion.
- Dashboard using Streamlit or Retool.

## 👤 Author
**Hasan Issa** – AI Automation Engineer  
[LinkedIn](https://l.instagram.com/?u=https%3A%2F%2Fwww.linkedin.com%2Fin%2Fhasan-issa30%2F%3Futm_source%3Dig%26utm_medium%3Dsocial%26utm_content%3Dlink_in_bio%26fbclid%3DPAZXh0bgNhZW0CMTEAc3J0YwZhcHBfaWQPOTM2NjE5NzQzMzkyNDU5AAGnJgIbMY_VZGCL-omZPvp7A9n_1wp0SohXbi8rpLzKjv-bNLraYovDw2k_d_8_aem_uRBRqK8S2sq9u7W_5GrSgQ&e=AUCRmAumMaUmOP7a6y6hLE3gf3afIZ6QoVxwMFdcYB1weU6kkOiUYD3OHAGh8N7xRnK72tAi_TrYuyTi9hTMpDUiXUEbo_IaY6kERTAU-SoAQld8ZK3A1kuX8n13fohKtvM9kgs) | [Instagram](https://www.instagram.com/hasan._._issa?igsh=MWllMHUwYzc3cW9nbw%3D%3D)
[GitHub](https://github.com/hasanissa791-cmyk) 
## ⭐ Show Your Support
If this project helps you, please give it a star!

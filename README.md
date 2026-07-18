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

## ⭐ Show Your Support
If this project helps you, please give it a star!

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
📐 Project Architecture
1. Overview
Name: AI Lead Qualification System

Primary Function: Receives lead data (name, company, budget, challenge), analyzes it using AI, assigns a score (0-100), and then directs it to one of two paths:

High (≥ 70): Sends email + Telegram message + external HTTP request.

Low (< 70): Saves data to Google Sheets.

Operation Channels: 3 triggers (Manual, Webhook, Scheduled).

2. Core Data Schema
All nodes interact with a single JSON object that holds these keys:

Field Type Source Example
full_name User input text "Ahmed"
email User input text "ahmed@web.com"
company User input text "Tech Company"
website User input text "https://tech.com"
service User input text "Automated Consulting"
budget User input number 6000
challenge User input text "We waste time on customer onboarding"
lead_score AI-generated score 85
summary AI-generated text "High-value customer with a large budget..."
recommendation AI-generated text "Advanced Automation Service"
classification Text added by Code "High" or "Low"
3. System Components
Workflow is divided into 4 main layers:

Layer 1: Inputs (Input Layer)
Triggers:

Manual Trigger (for development and testing).

Webhook (for receiving data from external systems).

Schedule Trigger (for dummy data/automated testing).

Data Transformers:

Code in JavaScript1 (Webhook data format).

Code in JavaScript2 (Generates dummy data for automation).

Layer 2: Processing Layer
Input Merge: Merge (Combines the 3 triggers into a single path).

AI Agent: AI Agent (Analyzes the text and extracts the score and recommendation).

Outcome Extraction: Code in JavaScript (Extracts the lead_score, summary, and recommendation from the AI ​​text and merges them with the original data).

Layer 3: Logic Layer
Conditional Branching: If (Sorts clients into a High or Low path based on a lead_score > 70).

Filter: Filter (Removes empty elements before sending a Telegram). Layer 4: Actions and Outputs

High Path:

Send a message (Gmail): Sends a formatted email.

Wait + Send a text message (Telegram): Sends a 10-second delay alert.

HTTP Request: Sends a copy of the email to Webhook.site (for integration with other systems).

Low Path:

Append row in sheet (Google Sheets): Saves data.

Final Aggregate:

Merge1 (Combines the outputs of both paths).

Aggregate (Converts an array to a single element with array keys).

Code in JavaScript 3 (Selects the correct element and adds classification).

Respond to Webhook (Responds with JSON to the external sender).


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
[LinkedIn](https://l.instagram.com/?u=https%3A%2F%2Fwww.linkedin.com%2Fin%2Fhasan-issa30%2F%3Futm_source%3Dig%26utm_medium%3Dsocial%26utm_content%3Dlink_in_bio%26fbclid%3DPAZXh0bgNhZW0CMTEAc3J0YwZhcHBfaWQPOTM2NjE5NzQzMzkyNDU5AAGnJgIbMY_VZGCL-omZPvp7A9n_1wp0SohXbi8rpLzKjv-bNLraYovDw2k_d_8_aem_uRBRqK8S2sq9u7W_5GrSgQ&e=AUCRmAumMaUmOP7a6y6hLE3gf3afIZ6QoVxwMFdcYB1weU6kkOiUYD3OHAGh8N7xRnK72tAi_TrYuyTi9hTMpDUiXUEbo_IaY6kERTAU-SoAQld8ZK3A1kuX8n13fohKtvM9kgs) | [Instagram](https://www.instagram.com/hasan._._issa?igsh=MWllMHUwYzc3cW9nbw%3D%3D) |
[GitHub](https://github.com/hasanissa791-cmyk) 
## ⭐ Show Your Support
If this project helps you, please give it a star!

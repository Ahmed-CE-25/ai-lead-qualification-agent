# AI-Powered Lead Qualification & Routing Agent

An intelligent, event-driven automation pipeline that captures inbound business leads, utilizes an LLM to dynamically score and analyze intent, filters leads through conditional logic routers, and executes targeted database updates and email delivery sequences.

## 💡 The Problem
Sales teams waste up to 50% of their time chasing low-quality leads, spam, or looky-loos who can't afford their services. Conversely, high-value enterprise leads often sit waiting in a generic inbox for days. Businesses need a system that instantly separates high-intent buyers from tire-kickers the second a form is submitted.

## ⚙️ Architecture & How It Works
This workflow functions as an automated sales operations manager inside n8n:

1. **Inbound Trigger:** Captures incoming prospective customer data via the `On form submission` webhook node.
2. **AI Analysis & Scoring:** Passes the lead's project details and budget over to the `Message a Model` node (powered by Gemini). The AI evaluates buyer intent, urgency, and budget fit, generating a qualification score from 1-10.
3. **Data Normalization:** The `Edit Fields` node parses the LLM's unstructured text output into clean, structured data objects (Score, Reasoning, Fit Type).
4. **Conditional Routing:** An `If` router evaluates the AI's metrics. 
   - **True (High-Value Lead):** Triggers an immediate priority routing sequence.
   - **False (Low-Value/Spam):** Filters the lead into a standard nurture or automated rejection loop.
5. **Database Sync:** The pipeline maps and writes the full lead details, along with the AI's qualification score and reasoning, into a centralized `Google Sheets` dashboard.
6. **Dynamic Follow-Up:** Executes the `Gmail API` node to instantly send a hyper-personalized email contextually tailored to the lead's specific score and requirements.

## 🛠️ Tech Stack
- **Orchestration:** n8n Workflow Automation
- **AI Core:** Google Gemini API (Advanced Language Model Data Parsing)
- **Data Warehousing:** Google Sheets API
- **Communications:** Gmail API
- **Logic:** Conditional IF-Routers & Dynamic Data Transformations

## 📋 What I'd Customize for a Real Client
- **Priority Escalation:** For leads scored 9 or 10, skip email entirely and use a Twilio or Slack webhook to instantly call or text the founder's phone: *"Enterprise lead detected. Tap link to call them back right now."*
- **Calendar Integration:** Dynamically inject a personalized booking link (like Cal.com or Calendly) into the email body, but *only* for the leads that clear the high-value `If` node. 
- **CRM Sync:** Map the structured AI outputs directly into properties inside HubSpot or Pipedrive for immediate tracking by sales reps.

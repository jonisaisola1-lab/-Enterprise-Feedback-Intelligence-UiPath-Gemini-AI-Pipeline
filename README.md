# Automated Customer Feedback Analysis
## Real-time Sentiment Classification & Structured Data Pipeline

> **Portfolio note:** This repository documents a TripleTen AI Automation project. The repo name is awkward (it was auto-generated) — the content itself is the documentation of a working Make.com + Gemini feedback analysis pipeline.

A production-ready workflow that collects customer feedback, analyzes sentiment with AI, extracts structured insights, and routes alerts — all in real time, with zero manual intervention.

---

## 🚀 The Problem

Customer feedback is buried in forms, emails, and support tickets. Manual classification is slow, inconsistent, and misses patterns. Negative sentiment festers without immediate attention.

**This system** captures feedback → analyzes it → structures it → alerts the team on negative sentiment — all automatically, in under a minute.

---

## 🛠️ Technical Architecture & Stack

- **Data Capture:** Google Forms (customer feedback collection)
- **Orchestration:** Make.com (webhook processing, conditional branching)
- **AI Analysis:** Google Gemini 2.5 Flash (sentiment classification & summarization)
- **Storage & Reporting:** Google Sheets (structured output with timestamps)
- **Notifications:** Email alerts on negative sentiment (optional but encouraged)

---

## 🧠 Core Engineering & Logic

**End-to-End Pipeline:**

1. **Google Form Submission** → New response captured
2. **Make Webhook Trigger** → Immediately routes to Gemini for analysis
3. **Gemini Processing** → Returns strict JSON with:
   - `sentiment` — one of: Positive, Neutral, Negative
   - `summary` — one-sentence distillation of the feedback
4. **JSON Parsing** → Make parses the response and validates structure
5. **Google Sheets Entry** → Clean row written with timestamp, original feedback, sentiment, and summary
6. **Conditional Alert** → If sentiment = "Negative", email fired to the manager

**The Critical Engineering Challenge:**

The naive approach is to ask Gemini "analyze this feedback" and hope for JSON back. **This project explicitly handles the failure case**: the prompt is engineered to enforce a strict JSON schema, and the parser is defensive.

Why it matters: If the JSON is malformed, the entire pipeline breaks. The solution is a carefully tuned system prompt that makes Gemini return valid, consistent JSON every time.

**Human-in-the-Loop Safeguards:**

- Email alerts on negative sentiment route immediately to a human reviewer
- Neutral responses are logged but don't trigger actions (no over-alerting)
- Positive feedback is captured for testimonials / NPS tracking
- Every row in Sheets is traceable to the original form submission

---

## 📈 What This Proves

- **Prompt Engineering:** Forcing an LLM to return structured, parseable output in a production system
- **Data Integrity:** End-to-end validation and error handling
- **Business Logic:** Conditional routing and alert thresholds
- **Scalability:** Handles unlimited form submissions without manual work

---

## 🎯 Use Cases

- **SaaS Companies:** Automatic triage of support feedback
- **E-commerce:** Real-time customer sentiment on products and orders
- **Product Teams:** Capture feature requests and bugs, auto-categorized
- **HR / Culture:** Employee feedback loops with automatic escalation on concerns

---

## How to Build It (Step by Step)

### Prerequisites
- Google Forms account
- Make.com account
- Google Sheets for output
- Gemini API access (via Make integration)
- Gmail account (for alerts)

### Workflow Steps

1. **Create a Google Form** with fields like:
   - Email (optional, for follow-up)
   - Feedback (long text)
   - Category (optional dropdown)

2. **Set up Make workflow:**
   - Trigger: Google Forms — New Response
   - Action 1: Gemini (via Make's native Gemini module)
     - Prompt (system): `You are a sentiment analyzer. Analyze the customer feedback and return ONLY valid JSON with keys "sentiment" (one of: Positive, Neutral, Negative) and "summary" (one sentence). Do not include any text outside the JSON.`
     - Input: The feedback text from the form
   - Action 2: Parse JSON
   - Action 3: Google Sheets — Add Row
     - Columns: Timestamp, Original Feedback, Sentiment, Summary, Email (from form)
   - Action 4 (Optional): Gmail — Send Email
     - Condition: If sentiment = "Negative"
     - Email to: manager@company.com
     - Subject: "Alert: Negative Feedback Received"
     - Body: Include summary and original text

3. **Create Google Sheets with headers:**
   - Timestamp | Original Feedback | Sentiment | Summary | Customer Email

4. **Test:**
   - Submit a positive feedback via form
   - Check Sheets for clean entry
   - Submit negative feedback
   - Confirm email alert fires
   - Submit out-of-scope input (e.g., "??????????")
   - Verify it still parses (doesn't break the pipeline)

---

## 📊 Expected Output

Each form submission becomes a single, clean row in Sheets:

| Timestamp | Original Feedback | Sentiment | Summary | Customer Email |
|-----------|-------------------|-----------|---------|-----------------|
| 2025-09-15 14:32 | Your app crashed when I tried... | Negative | App crashed during checkout flow | user@example.com |
| 2025-09-15 14:45 | Love the new dashboard update | Positive | User loves the new dashboard | happy@example.com |

Negative entries trigger immediate email to manager. All entries are logged and queryable.

---

## 🎓 Why This Matters

This is the **first project in your journey** where you built guardrails without knowing the vocabulary yet. You were solving the core problem of production AI: *"Don't hallucinate. Return clean, parseable data. Alert a human if something is wrong."*

The "Automated Feedback Analysis" capstone credit proves:
- You can architect an end-to-end pipeline
- You understand prompt engineering for robustness
- You know how to build alerting into automation
- You think about failure modes and human oversight

---

## 📝 Notes

- **Approved project:** TripleTen AI Automation Program
- **Stack:** Google Forms → Make → Gemini → Sheets
- The real skill is the **prompt engineering** (forcing valid JSON) and the **defensive parsing** (not breaking on malformed AI output)
- Easily extensible to Slack alerts, CRM integrations, or multi-stage triage workflows

---

## 🔧 Troubleshooting

**"JSON parse step is failing"**
- Check that Gemini's response is actually valid JSON (log the raw output in Make)
- Revise the system prompt to be more explicit: "Return ONLY valid JSON. No markdown, no extra text."

**"Negative alerts aren't firing"**
- Verify the conditional path in Make checks for `sentiment` field value exactly as returned (case-sensitive)
- Test with a deliberately negative feedback to confirm the path works

**"Sheets entries are incomplete or inconsistent"**
- Ensure all Gemini fields map to Sheets columns
- Add a validation step in Make that skips rows with missing sentiment/summary

---

## 📚 Related Projects

- **Invoice Processing RPA** — Similar confidence-check pattern for document extraction
- **RAG Hotel Chatbot** — Another "don't hallucinate" guardrail system
- **Omni-Capture OS** — Advanced routing logic building on similar foundations

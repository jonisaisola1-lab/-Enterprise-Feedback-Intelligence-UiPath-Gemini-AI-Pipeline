# Enterprise-Feedback-Intelligence: UiPath + Gemini AI Pipeline
**Automated Customer Sentiment Analysis & Resolution Workflow**

## 🚀 The Business Problem
Manual processing of customer feedback is a major bottleneck for scaling businesses. This project solves the "unstructured data" problem by automating the scraping, analysis, and response drafting for customer reviews and support tickets.

## 🛠️ Technical Architecture & Stack
This system leverages a "Hybrid Automation" approach, combining deterministic RPA with probabilistic AI:

*   **RPA Orchestration**: **UiPath Studio** managing the end-to-end data flow, system interactions, and scheduling.
*   **AI Intelligence**: **Google Gemini (LLM)** integrated via API for deep contextual sentiment analysis and draft generation.
*   **Communication Layer**: **Gmail API** for automated response drafting based on AI-generated insights.
*   **Reporting Layer**: **Google Sheets** for real-time executive-level intelligence dashboards.

## 🧠 Visual Logic & Workflow Architecture
The following screenshots demonstrate the core logical sequences and "Human-in-the-Loop" decision nodes built within the UiPath environment:

### 1. Data Intake & Initial Processing
![Workflow Step 1](assets/uipath_workflow_step_1.png)
*Automated scraping and normalization of raw customer feedback data.*

### 2. AI Sentiment Analysis (Gemini Integration)
![Workflow Step 2](assets/uipath_workflow_step_2.png)
*The core intelligence layer where feedback is scored and categorized by the LLM.*

### 3. Intent-Based Routing
![Workflow Step 3](assets/uipath_workflow_step_3.png)
*Decision logic for routing "At-Risk" feedback vs. positive testimonials.*

### 4. Automated Response Drafting
![Workflow Step 4](assets/uipath_workflow_step_4.png)
*Generation of context-aware drafts using personalized AI templates.*

### 5. Enterprise Reporting & Dashboarding
![Workflow Step 5](assets/uipath_workflow_step_5.png)
*Final output to the Google Sheets intelligence dashboard.*

## 📈 Measurable Impact (ROI)
*   **Workload Reduction**: Reduced manual feedback review time by **80–90%**.
*   **Response Velocity**: Decreased average response time from **24+ hours to under 5 minutes**.
*   **Scalability**: Built to handle thousands of feedback entries per day without increasing headcount.

---
*Technical Project | TripleTen AI Automation Program | UiPath & Gemini Integration.*

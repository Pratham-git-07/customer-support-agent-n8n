# AI Customer Support Auto-Responder V2 (n8n + Gemini AI)

An AI-powered customer support automation workflow built using **n8n**, **Google Gemini AI**, **Google Sheets**, and **Gmail**. The workflow automatically classifies customer queries, routes them to the appropriate department, sends personalized responses, logs all interactions, and gracefully handles AI failures.

---

## Features

- Google Sheets as customer request database
- AI-based query classification using Google Gemini
- Intelligent routing using Switch node
- Automated email responses for:
  - Billing queries
  - Technical issues
  - General feedback
- Google Sheets logging
- AI failure detection and admin alert system
- AI Status tracking (`Success` / `Failed`)
- Timestamp logging
- Continue-on-fail error handling for resilient workflows

---

## Workflow Architecture

```text
Google Sheets Trigger
        ↓
Preprocess Customer Query
        ↓
Basic LLM Chain (Gemini AI)
        ↓
Merge AI Output with Customer Data
        ↓
Switch Node
 ├── Billing → Billing Email
 ├── Technical → Technical Email
 ├── Feedback → Feedback Email
 └── AI Failed → Admin Alert Email
        ↓
Log Support Request
```

---

## Technologies Used

- **n8n**
- **Google Gemini 2.0 Flash**
- **Google AI Studio API**
- **Google Sheets API**
- **Gmail API**
- **JavaScript**

---

## Folder Structure

```text
v2-ai-powered/
│
├── workflow.json
├── README.md
└── screenshots/
    ├── workflow-overview.png
    ├── gemini-classification.png
    ├── switch-routing.png
    ├── ai-failure-email.png
    └── log-sheet.png
```

---

## Workflow Components

### 1. Google Sheets Trigger
Monitors a Google Sheet for newly added customer support requests.

**Input Fields:**
- Name
- Email
- Category
- Message
- Urgency

---

### 2. Preprocess Customer Query
Uses JavaScript to clean and standardize input data before sending it to Gemini AI.

Tasks performed:
- Convert text to lowercase
- Normalize category values
- Extract customer information

---

### 3. Google Gemini AI (Basic LLM Chain)

Gemini AI classifies customer queries into one of the following categories:

- `billing`
- `technical`
- `feedback`

Example:

**Input:**

```text
"I was charged twice on my invoice"
```

**AI Output:**

```json
{
  "text": "billing"
}
```

---

### 4. Merge Node

Combines:

- Original customer data
- AI classification result

This ensures downstream nodes have access to all fields.

---

### 5. Switch Node

Routes queries based on AI-generated categories.

Routes:

- Billing
- Technical
- Feedback
- AI Failed

---

### 6. Gmail Nodes

Automatically send customized email responses based on the detected category.

Example Billing Response:

```text
Hi {{name}},

We've received your billing query regarding:
"{{message}}"

Our finance team will review your request and respond within 24 hours.

Regards,
Support Team
```

---

### 7. AI Failure Alert

If Gemini fails (for example due to API rate limits), the workflow:

- Continues execution
- Sends an admin alert email
- Logs the failure in Google Sheets

This provides production-style fault tolerance.

---

### 8. Google Sheets Logging

Logs:

- Customer Name
- Email
- Category
- Urgency
- Timestamp
- Status
- AI Status

Example:

| Name | Category | Status | AI Status |
|------|----------|--------|-----------|
| Aanya | billing | Email Sent | Success |
| Shanaya | - | AI Failed | Failed |

---

## Screenshots

### Workflow Overview

<img width="1877" height="870" alt="workflow-overview-v2" src="https://github.com/user-attachments/assets/6437b1c7-88b8-4010-9bd1-24136bb89e83" />


### Gemini Classification

<img width="1861" height="882" alt="gemini-classification" src="https://github.com/user-attachments/assets/76e78b9a-2305-42df-8ba3-a25780e8486e" />


### AI Failure Email

<img width="802" height="1600" alt="ai-failure-email" src="https://github.com/user-attachments/assets/49cc9cb7-bf2b-411b-9434-5755a6170be5" />


### Log Sheet

<img width="1153" height="548" alt="log-sheet-v2" src="https://github.com/user-attachments/assets/ae9c3db7-9dba-4137-bcbd-ee6c5c519130" />


---

## Setup Instructions

### Prerequisites

- n8n instance (Cloud or Self-hosted)
- Google AI Studio API Key
- Gmail account
- Google Sheets account

### Configure Credentials

Create credentials for:

- Google Gemini API
- Gmail API
- Google Sheets API

Import:

```text
workflow.json
```

Update:

- API keys
- Sheet IDs
- Gmail credentials

Activate the workflow.

---

## Future Improvements

- AI-generated email responses
- Sentiment analysis
- Priority detection
- Knowledge base integration (RAG)
- Slack/Teams notifications
- Multi-language support

---


## License

This project is licensed under the MIT License.

---

## Author

**Pratham Singh**


---

⭐ If you found this project useful, consider giving it a star!

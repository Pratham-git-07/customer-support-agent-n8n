## Overview

This project is a rule-based customer support automation workflow built using **n8n**, **Google Sheets**, **Gmail**, and **JavaScript**.

The workflow automatically detects new customer requests submitted through Google Sheets, categorizes them into predefined categories, sends automated email responses, and logs processed requests into another Google Sheet.

---

## Features

* Google Sheets Trigger for new customer requests
* JavaScript-based data preprocessing
* Switch-based query routing
* Automated Gmail responses
* Logging of processed requests
* Audit trail for customer interactions

---

## Workflow Architecture

```text
Google Sheets Trigger
        ↓
JavaScript Processing
        ↓
Switch Node
   ┌──────────┬────────────┬───────────┐
 Billing   Technical   Feedback
    ↓          ↓           ↓
 Gmail      Gmail       Gmail
    └──────────┴───────────┘
              ↓
      Append Row in Sheet
```

---

## Categories Supported

* Billing
* Technical
* Feedback

---

## Technologies Used

* n8n
* Google Sheets API
* Gmail API
* JavaScript

---

## Screenshots

### Workflow Overview

<img width="1847" height="851" alt="workflow-overview" src="https://github.com/user-attachments/assets/d848ba2c-6dc0-4bfc-a0fd-37b98f4fee59" />


### Input Sheet

<img width="1441" height="635" alt="google-sheet-input" src="https://github.com/user-attachments/assets/d3443b1a-7c3e-4aee-96fd-61b9b41ca9a6" />

### Log Sheet

<img width="1637" height="573" alt="log-sheet" src="https://github.com/user-attachments/assets/f02a4772-a70d-46ea-97f3-06c56653afd6" />


---

## How It Works

1. A customer request is added to Google Sheets.
2. The workflow is automatically triggered.
3. JavaScript normalizes and processes the data.
4. The Switch node routes the request based on category.
5. An automated email response is sent.
6. The processed request is logged into another Google Sheet.

---

## Future Improvements

* AI-powered query classification
* Dynamic email generation using LLMs
* Sentiment analysis
* Ticket ID generation
* Slack notifications
* Database integration

---

## License

This project is licensed under the MIT License.

## Author

**Pratham Singh**

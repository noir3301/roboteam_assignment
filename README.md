
# 🛠️ Roboteam support system (n8n + Flask)

## 📌 Project Description

Deals with sorting issues and provides responses.

A `Flask-based` web form submits data to an n8n webhook, initiating an automated workflow.

An `n8n workflow` processes incoming issues by classifying them, storing bug reports in Google Sheets, sending notification emails for feature requests, answering general questions and saving logs in MongoDB.

The `Flask server` is responsible for managing the web form and generating embeddings for issues to prevent duplicates.

## 🧩 Project architecture

```plaintext
                [User] → [Flask Web Form]         
                                ↓
       [Webhook to n8n] ← [Flask Server] → [Generate embeddings]
               ↓                                     ↓    
     ┌────────────────────────────────────────────────────────────┐
     │                            n8n                             │
     │                                                            │
     │  - Webhook Trigger                                         │
     │  - Data Transformation                                     │
     │  - Text Classification                                     │
     │  - LLM Node                                                │
     │  - MongoDB Logging                                         │
     │  - Email Notification                                      │
     │  - Google Sheets Record                                    │
     └────────────────────────────────────────────────────────────┘
```

## 🔁 Sample Request

### Option 1
Use the Flask web form at this link to trigger the n8n workflow:
https://support-noir3301.pythonanywhere.com/

### Option 2
To trigger the n8n workflow, you can also send a POST request using another method — to do so, use:
```plaintext
N8N_WEBHOOK_URL="https://noir3301.app.n8n.cloud/webhook/e060d70f-6fb0-4195-813d-a811210e39f8"
```

The web-form collects:

* Name
* Email
* Issue description

So sample data structure sent to n8n webhook:
```json
{
  "name": "Anna",
  "email": "anna@example.com",
  "description": "Payment doesn't work on the website."
}
```

## 🗃️ Additional info

### 1. API credentials

MongoDB is accessible from any IP address
```plaintext
DB_NAME = "n8n_project"
CLUSTER_NAME = "support"
TYPE = "TIME_SERIES_COLLECTION"
DATETIME_FIELD_NAME = "date"
```
```plaintext
MONGO_URI="mongodb+srv://velichkinaleksey3:YS3t0nPR5JJvpxA3
@cluster0.roahiop.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0"
COHERE_API_KEY="y5oUE3gmSE8xx0EvNHgkYbzerFIcqgq058SOQiwy"
```

### 2. Account credentials

Credentials for the email that receives feature requests:
```plaintext
support.test3301@atomicmail.io
Emailtest123
```

Google Sheets with bug reports:
[**LINK**](https://docs.google.com/spreadsheets/d/1zZLxbM117NXJcSzPa5pZtlDhm_Y-yW0RO32DJaB1F4Y/edit?gid=0#gid=0)

### 3. Environment
```plaintext
python 3.13.1

cohere==5.15.0
Flask==3.0.3
pymongo==4.10.1
requests==2.32.3
scikit-learn==1.6.0
```

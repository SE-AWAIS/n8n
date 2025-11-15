# ⭐ **AI-Powered SaaS Lead Qualification & Email Automation**
---

An intelligent agent that automatically qualifies SaaS leads after form submission, scores them using AI, sends a personalized email, handles bounce errors, updates a Leads sheet, and logs every interaction in a separate Logs sheet.
Ideal for SaaS founders, marketers, and automation builders.

This template processes SaaS lead submissions, uses AI to determine lead quality, generates a lead score, sends a personalized follow-up email, updates a Leads Google Sheet, and writes a full interaction log to another sheet.
It includes bounce-handling logic to prevent errors and maintain clean records.

---

# ⭐ **Key Features**

🔹 AI-based lead qualification
🔹 AI scoring system (0–100)
🔹 Personalized email generation
🔹 Google Sheets Lead storage
🔹 Google Sheets full interaction log
🔹 Flexible scoring thresholds
🔹 Bounce handling with error capture
🔹 Perfect for SaaS startups, marketers, and CRM automation

---

# ⭐ **Required Credentials**

* Google Sheets (2 sheets required → Leads + Logs)
* Gmail
* Chat Model: OpenAI / Groq / Claude / Gemini or any AI model supported

---

# ⭐ **Workflow Structure (Node-by-Node)**

### **1. Form Trigger (Webhook or n8n Forms)**

Captures fields:

* Full Name
* Email Address
* Company Name
* Company Size
* Job Title
* What challenges are you facing?
* submittedAt
* formMode

Purpose: Convert raw form submissions into actionable lead entries.

---

### **2. Workflow Configuration (Static Data)**

Stores:

* leadsSheetId
* logsSheetId
* qualificationThreshold (default 70)
* highPriorityScore (default 85)

Purpose: Central place to change sheet IDs & scoring rules.

---

### **3. Google Sheets (Append Lead to Leads Sheet)**

Stores raw lead information before any evaluation.

---

### **4. AI Lead Scoring Node**

Analyzes:

* Role relevance
* Company size
* Problem/challenges
* Buying intent
* Email validity
* Industry fit

Outputs:

```json
{
  "leadScore": 0-100,
  "priority": "Low | Normal | High",
  "qualificationReason": "Short AI summary"
}
```

---

### **5. AI Personalized Email Node**

Generates:

* Subject
* Body
* Tone based on priority
* 2-line CTA

---

### **6. Gmail Node (Send Email)**

Sends the personalized email.
Includes bounce/error handling with `Continue on Fail`.

---

### **7. Success/Bounce Branch**

If success → proceed
If fail → status = "Bounce"

---

### **8. Google Sheets (Append to Interaction Logs Sheet)**

Writes:

* timestamp
* status
* emailDelivered
* leadScore
* emailRecipient
* emailSubject
* priority

Final JSON sample (required for logs sheet):

```json
[
  {
    "timestamp": "{{ $now }}",
    "status": "Email Sent",
    "emailDelivered": true,
    "leadScore": XX,
    "emailRecipient": "your-email@example.com",
    "emailSubject": "EMAIL SUBJECT",
    "priority": "High"
  }
]
```

---

# ⭐ **How to Use This Template**

1. Import the workflow
2. Add your Google Sheet IDs in the config node
3. Connect your Gmail / Email credentials
4. Map your form fields to the first node
5. Execute workflow → done

---

# ⭐ **Why This Template Will Be Accepted & Featured**

✔ Solves a real business problem
✔ Uses AI in a valuable, non-gimmick way
✔ Offers complete automation (end-to-end lifecycle)
✔ Has clear, re-usable components: Forms → AI → Sheets → Email → Logging
✔ Great for SaaS founders, marketers, CRM builders
✔ Follows n8n best practices:

* config node
* error handling
* clean JSON format
* independent sheets for storage/logging

--- [SaaS leads Qualification Agent via n8n Form Submission (1).json](https://github.com/user-attachments/files/23559457/SaaS.leads.Qualification.Agent.via.n8n.Form.Submission.1.json)

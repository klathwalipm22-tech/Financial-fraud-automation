# 🛡️ AI-Powered Financial Fraud Detection Workflow using n8n

> **Real-Time Transaction Risk Scoring for NBFCs & Digital Banking**  
> MBA Applied Finance | AI Agents & Automation | Chitkara University

-----

## 📌 Problem Statement

Mid-sized NBFCs and banks process **hundreds of thousands of UPI/NEFT/IMPS transactions daily**, yet fraud detection remains largely manual:

- ⏱️ Fraud detected **24+ hours later** — money already gone
- 👤 Manual analyst review **misses patterns** at high volume
- 🚨 **No real-time alerts** — risk team notified end of day
- 📋 No structured **audit trail** from manual review
- 📈 UPI volume crossed **₹20L crore/month** — completely unscalable

-----

## 💡 Our Solution

An **n8n automation workflow** that processes financial transactions in real time, applies 12 fraud detection rules, computes a risk score, updates a Google Sheet, and sends automated email alerts — all in **under 1 second**.

|Metric        |Before (Manual)|After (Automated)|
|--------------|---------------|-----------------|
|Detection Time|24+ hours      |< 1 second       |
|Human Effort  |100%           |0%               |
|Audit Trail   |None           |Auto-logged      |
|Alert Speed   |End of day     |Real-time        |

-----

## 🗂️ Dataset

Self-designed dataset with **55 transactions** and **13 input columns + 3 n8n output columns**:

|Column                              |Description                           |
|------------------------------------|--------------------------------------|
|`Transaction_ID`                    |Unique transaction identifier         |
|`Customer_ID`                       |Unique customer identifier            |
|`Amount_(INR)`                      |Transaction amount in rupees          |
|`Transaction_Time`                  |Date and time of transaction          |
|`Location`                          |City / Foreign / Unknown              |
|`Account_Age_(Days)`                |Days since account opened             |
|`Prev_Txn_Count`                    |Previous transaction history          |
|`Outflow_Ratio_%`                   |% of money immediately transferred out|
|`Transaction_Type`                  |UPI / NEFT / IMPS / Wire              |
|`Merchant_Category`                 |Electronics, Food, Crypto, etc.       |
|`Device_Status`                     |Known / New device                    |
|`Impossible_Travel`                 |Yes / No flag                         |
|**`Rules_Triggered`** *(n8n output)*|Which rules fired                     |
|**`Risk_Score`** *(n8n output)*     |Cumulative score (0–100)              |
|**`Fraud_Status`** *(n8n output)*   |LOW / MEDIUM / HIGH RISK              |

-----

## ⚙️ n8n Workflow Architecture

The workflow runs through the following nodes:

```
Google Sheets Trigger
        ↓
   Code Node (JavaScript)
   — Applies 12 fraud detection rules
   — Computes cumulative risk score
        ↓
   IF / Switch Node
   — Routes by risk level (LOW / MEDIUM / HIGH)
        ↓
   Google Sheets Update Node
   — Writes Rules_Triggered, Risk_Score, Fraud_Status
        ↓
   Gmail Node
   — Sends alert emails for MEDIUM + HIGH risk
```

-----

## 🔍 12 Fraud Detection Rules

|Rule|Description                         |
|----|------------------------------------|
|R1  |Amount > ₹50,000                    |
|R2  |Round amount (₹10K / ₹50K / ₹1L)    |
|R3  |Micro probe < ₹10 (new account)     |
|R4  |Foreign location transaction        |
|R5  |Unknown location                    |
|R6  |New device used                     |
|R7  |Impossible travel flag              |
|R8  |High outflow ratio (> 80%)          |
|R9  |Account age < 30 days               |
|R10 |Crypto / high-risk merchant category|
|R11 |Wire transfer (high-risk type)      |
|R12 |Low previous transaction count      |

-----

## 📊 Results

- ✅ **55 transactions** processed automatically
- 📧 **29 alert emails** sent (14 HIGH RISK + 15 MEDIUM RISK)
- ⚡ **16.8 seconds** total processing time vs 3–4 hours manually
- 📉 **99.9% reduction** in detection time
- 🧑‍💼 **100% human effort eliminated**

-----

## 🛠️ Tech Stack

|Tool             |Purpose                             |
|-----------------|------------------------------------|
|**n8n**          |Workflow automation engine          |
|**JavaScript**   |Fraud rule logic in Code Node       |
|**Google Sheets**|Transaction dataset & output logging|
|**Gmail API**    |Automated alert emails              |

-----

## 🚀 Future Scope

- 🤖 Replace static rules with **ML model** (Random Forest / XGBoost)
- 🔮 **Predictive scoring** before transaction completes
- 💬 **WhatsApp alerts** via Twilio integration
- 🏦 **Core Banking System (CBS) API** integration for auto-blocking
- 📱 **Power BI / Looker Studio** live fraud dashboard
- 🌍 **RBI STR filing** and FEMA compliance automation

-----

## ⚠️ Limitations

- Internet dependency — no offline fallback
- Static rules cannot learn new fraud patterns
- Velocity checks use pre-flagged proxy columns
- n8n cloud execution limits at real bank scale
- GDPR / RBI data localisation compliance considerations

-----

## 📚 References

- [n8n Documentation](https://docs.n8n.io)
- [Razorpay Fraud Detection Blog](https://razorpay.com/blog)
- [Stripe Radar Documentation](https://stripe.com/docs/radar)
- [RBI Master Circular on Fraud Classification (2025)](https://rbi.org.in)
- [NPCI UPI Transaction Guidelines 2026](https://npci.org.in)
- [Mastercard Decision Intelligence Whitepaper](https://mastercard.com)

-----

## 📸 Screenshots

<img width="1600" height="900" alt="WhatsApp Image 2026-06-04 at 1 50 20 PM" src="https://github.com/user-attachments/assets/bd4d2110-e0d1-4b72-b124-fc224806514f" />
<img width="1600" height="900" alt="WhatsApp Image 2026-06-04 at 1 52 12 PM" src="https://github.com/user-attachments/assets/fc4de26e-7b2b-4cb5-9d6a-95370eebf292" />
<img width="1600" height="900" alt="WhatsApp Image 2026-06-04 at 1 53 07 PM" src="https://github.com/user-attachments/assets/425765e7-9569-4552-af09-3b8e69b8b199" />



-----

*Built as part of the AI Agents & Automation course — MBA Applied Finance, Chitkara University, 2026*

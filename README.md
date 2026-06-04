# ICMR Database Lookup API

**Developer:** Syed Rehan  
**GitHub:** @rehuux

---

## 📌 Overview

This API provides a lookup interface for **ICMR (Indian Council of Medical Research)** related data. It allows searching by Aadhaar number, Passport number, or Phone number from a structured database.

> ⚠️ **For educational and research purposes ONLY. Strictly not for unauthorized use.**

---

## 🔬 What is ICMR?

| Term | Full Form | Description |
|------|-----------|-------------|
| **ICMR** | Indian Council of Medical Research | India's apex body for biomedical research |
| **Purpose** | Health research, disease surveillance, clinical trials | COVID-19 testing data, medical research |

> This API is for **educational demonstration** of database lookup systems.

---

## ✨ Features

| Feature | Description |
|---------|-------------|
| 🔍 **Aadhaar Lookup** | Search by Aadhaar number |
| 📞 **Phone Lookup** | Search by phone number |
| 🛂 **Passport Lookup** | Search by passport number |
| 📊 **CSV Import** | Automatic CSV to SQLite conversion |
| 🌐 **Web Dashboard** | Clean HTML interface |
| 📱 **JSON API** | RESTful JSON responses |
| 🛡️ **Health Check** | API status endpoint |

---

## 🔍 How It Works

```

1. CSV file (data.csv) is loaded on startup
   ↓
2. API automatically converts to SQLite database
   ↓
3. User sends search request via API or web
   ↓
4. Database queries for matching record
   ↓
5. Returns JSON response with found data

```

---

## 📥 API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/` | Web dashboard interface |
| GET | `/api/search/{aadhaar}` | Search by Aadhaar/Passport |
| GET | `/api/phone/{number}` | Search by phone number |
| GET | `/api/health` | Health check |

---

## 📤 Request/Response Examples

### 🔍 Search by Aadhaar

**Request:**
```http
GET /api/search/123456789012
```

Response (Success):

```json
{
  "success": true,
  "data": {
    "name": "John Doe",
    "fathersName": "Robert Doe",
    "phoneNumber": "9876543210",
    "otherNumber": "8765432109",
    "passportNumber": "Z1234567",
    "aadharNumber": "123456789012",
    "age": "32",
    "gender": "Male",
    "address": "123 Main Street",
    "district": "Mumbai",
    "pincode": "400001",
    "state": "Maharashtra",
    "town": "Andheri East"
  },
  "checked_at": "2026-06-04 10:30:45 UTC",
  "api_info": {
    "developer": "Syed Rehan",
    "github": "@rehuux"
  }
}
```

📞 Search by Phone

Request:

```http
GET /api/phone/9876543210
```

Response (Success):

```json
{
  "success": true,
  "data": {
    "name": "John Doe",
    "phoneNumber": "9876543210",
    "address": "123 Main Street",
    "district": "Mumbai",
    "state": "Maharashtra"
  },
  "checked_at": "2026-06-04 10:30:45 UTC",
  "api_info": {
    "developer": "Syed Rehan",
    "github": "@rehuux"
  }
}
```

❌ Record Not Found

Response:

```json
{
  "success": false,
  "error": "Record not found",
  "api_info": {
    "developer": "Syed Rehan",
    "github": "@rehuux"
  }
}
```

🏥 Health Check

Request:

```http
GET /api/health
```

Response:

```json
{
  "status": "healthy",
  "database_size": "1250.45 KB",
  "timestamp": "2026-06-04T10:30:45.123Z",
  "api_info": {
    "developer": "Syed Rehan",
    "github": "@rehuux"
  }
}
```

---

📊 Database Schema

Column Type Description
name TEXT Full name
fathersName TEXT Father's/Husband's name
phoneNumber TEXT Primary phone number
otherNumber TEXT Secondary phone number
passportNumber TEXT Passport number
aadharNumber TEXT Aadhaar number (12-digit)
age TEXT Age in years
gender TEXT Male/Female/Other
address TEXT Residential address
district TEXT District name
pincode TEXT Postal code
state TEXT State name
town TEXT City/Town name

---

📁 File Structure

```
icmr-database-api/
├── app.py              # Main Flask application
├── data.csv            # Source CSV data file
├── data.db             # SQLite database (auto-generated)
├── requirements.txt    # Dependencies
└── README.md           # Documentation
```

---

📥 Installation

Prerequisites

· Python 3.7+
· pip
· CSV file named data.csv with required columns

Setup Steps

```bash
# 1. Clone or create project
mkdir icmr-database-api
cd icmr-database-api

# 2. Create virtual environment
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# 3. Install dependencies
pip install flask

# 4. Place your data.csv file in the directory

# 5. Run the API
python app.py
```

---

📄 CSV File Format

The data.csv file must have these exact headers:

```csv
name,fathersName,phoneNumber,otherNumber,passportNumber,aadharNumber,age,gender,address,district,pincode,state,town
John Doe,Robert Doe,9876543210,8765432109,Z1234567,123456789012,32,Male,123 Main Street,Mumbai,400001,Maharashtra,Andheri East
```

⚠️ Headers are case-sensitive — must match exactly.

---

🎮 Usage Examples

Using cURL

```bash
# Search by Aadhaar
curl "http://localhost:5000/api/search/123456789012"

# Search by Phone
curl "http://localhost:5000/api/phone/9876543210"

# Health check
curl "http://localhost:5000/api/health"
```

Using Python

```python
import requests

# Search by Aadhaar
response = requests.get(
    "http://localhost:5000/api/search/123456789012"
)
print(response.json())

# Search by Phone
response = requests.get(
    "http://localhost:5000/api/phone/9876543210"
)
print(response.json())
```

Using JavaScript

```javascript
// Search by Aadhaar
fetch('http://localhost:5000/api/search/123456789012')
  .then(res => res.json())
  .then(data => console.log(data));

// Search by Phone
fetch('http://localhost:5000/api/phone/9876543210')
  .then(res => res.json())
  .then(data => console.log(data));
```

---

🌐 Web Interface

Visit http://localhost:5000 for a beautiful web dashboard featuring:

· API documentation
· Sample responses
· Endpoint examples
· Developer information

---

🛠️ Technical Stack

Component Technology
Framework Flask (Python)
Database SQLite3
Data Import CSV module
Frontend Tailwind CSS
Templates HTML + Jinja2

---

📊 API Features

Feature Description
Auto DB Creation Creates SQLite from CSV on first run
Batch Insert Inserts 1000 rows at a time for efficiency
Fallback Search If Aadhaar fails, tries Passport
UTF-8 Support Handles Indian language characters

---

🚀 Deployment

Deploy on Render

```yaml
# render.yaml
services:
  - type: web
    name: icmr-database-api
    runtime: python
    buildCommand: pip install flask
    startCommand: gunicorn app:app
```

Deploy on Railway

```bash
# Add to railway.toml
[build]
  command = "pip install flask gunicorn"

[deploy]
  startCommand = "gunicorn app:app"
```

Deploy on PythonAnywhere

```bash
# Upload app.py and data.csv
# Set up Web app with Flask
# Database will auto-create on first request
```

---

⚠️ Important Warnings

🚫 STRICT PROHIBITIONS

· DO NOT use for stalking or harassment
· DO NOT use for illegal background checks
· DO NOT sell or distribute data from this API
· DO NOT use for identity theft
· DO NOT claim this is official ICMR data

---

📜 Legal Disclaimer

THE DEVELOPER (SYED REHAN) TAKES ABSOLUTELY NO RESPONSIBILITY FOR MISUSE.

By using this API, you acknowledge that:

1. This is for educational purposes only
2. ICMR has NO affiliation with this project
3. Unauthorized access to personal data is illegal
4. You will only use this with your own data or test data
5. You are 100% responsible for your actions

---

🔒 Privacy & Compliance

Regulation Compliance
DPDP Act 2023 Not for production use
IT Act 2000 Educational use only
GDPR Not applicable (demo only)

⚠️ This API does NOT store any real ICMR data. It's a demonstration of database lookup systems.

---

🐛 Troubleshooting

Issue Solution
data.csv not found Place CSV file in same directory
Database will be empty Check CSV file path and permissions
Record not found Verify search value exists in database
UTF-8 encoding error Save CSV as UTF-8 encoding
Port 5000 in use Change port: app.run(port=8080)

---

🔧 Customization Options

Modification How To
Add more search fields Add new query_db calls
Change port Modify port=5000
Add authentication Implement API keys
Add rate limiting Use Flask-Limiter
Add more data fields Update schema and CSV

---

👨‍💻 Developer

Syed Rehan
GitHub: @rehuux

---

📄 License

For educational purposes only. Unauthorized commercial use is prohibited.

---

⚠️ Final Warning

This tool is for LEARNING database systems only.

· 🔴 DO NOT use real personal data
· 🔴 DO NOT claim this is official ICMR
· 🔴 DO NOT deploy for production
· ✅ DO use for learning Flask & SQLite
· ✅ DO use with sample/test data

---

🔴 FOR EDUCATIONAL USE ONLY - NOT AFFILIATED WITH ICMR

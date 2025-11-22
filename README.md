# 📦 Echocart Assistant

**AI-Powered Chrome Extension for Amazon Product Insights**

Echocart Assistant is a powerful Chrome extension that analyzes Amazon product pages using a local Flask backend connected to Groq’s LLaMA models. It extracts product details and reviews automatically, enabling instant AI-generated summaries, sentiment analysis, pros & cons, comparisons, and natural-language Q&A.

---

## 📑 Table of Contents

* [Features](#features)
* [Project Structure](#project-structure)
* [How It Works](#how-it-works)
* [Installation](#installation)
* [Backend Setup](#backend-setup)
* [Chrome Extension Setup](#chrome-extension-setup)
* [API Endpoints](#api-endpoints)
* [Configuration](#configuration)
* [Dependencies](#dependencies)
* [Security Notes](#security-notes)
* [Troubleshooting](#troubleshooting)

---

## ✨ Features

* **Auto-detect product information**
  Extracts title, description, and reviews directly from Amazon.
* **AI-powered insights**
  Powered by Groq’s LLaMA-3.1 models.
* **One-Click Actions**

  * 📚 Summaries
  * 🔍 Sentiment & review analysis
  * ⚖️ Product comparisons
  * 📌 Bullet-point pros & cons
* **Built-in AI Chat**
  Ask custom questions about the product and reviews.
* **Local backend for privacy**
  No external data logging—everything goes through your local Flask server.

---

## 📂 Project Structure

```
NEW ECHOCART/
│
├── ai/
│   ├── app.py                 # Flask backend API
│   ├── groq_client.py         # Groq client wrapper
│   ├── requirements.txt       # Backend dependencies
│   └── __pycache__/
│
├── icons/
│   ├── icon16.png
│   ├── icon48.png
│   └── icon128.png
│
├── background.js               # Chrome extension service worker
├── content.js                  # Scrapes Amazon product info
├── popup.html                  # Extension popup UI
├── popup.js                    # Popup logic + API calls
├── popup.css                   # Popup styling
└── manifest.json               # Chrome extension manifest (MV3)
```

---

## ⚙️ How It Works

### **1. Content Script (content.js)**

Runs on Amazon product pages and gathers:

* Product title
* Description / feature bullets
* Review text

This data flows into the popup UI.

---

### **2. Popup (popup.js + popup.html)**

Displays product data and provides controls:

* Summaries
* Review analysis
* Pros/cons
* Product comparison
* Chat with the AI

Uses fetch() to call your local backend.

---

### **3. Backend (Flask)**

Located in `/ai/app.py`, runs a lightweight REST API:

* Builds model prompts
* Sends requests to Groq using `groq_client.py`
* Returns structured responses to the extension

---

## 🛠 Installation

### Requirements

* Python 3.10+
* Google Chrome
* A Groq API key

---

## 🚀 Backend Setup

1. Navigate to the backend folder:

```
cd ai
```

2. Create a Python virtual environment:

```
python -m venv .venv
```

3. Activate the environment:

**Windows**

```
.venv\Scripts\activate
```

**macOS/Linux**

```
source .venv/bin/activate
```

4. Install backend dependencies:

```
pip install -r requirements.txt
```

5. Add your Groq API key in `groq_client.py`:

```python
API_KEY = "your_api_key_here"
```

6. Start the server:

```
python app.py
```

Your backend will run at:
👉 **[http://127.0.0.1:5000](http://127.0.0.1:5000)**

---

## 🧩 Chrome Extension Setup

1. Open Chrome
2. Go to:

   ```
   chrome://extensions
   ```
3. Enable **Developer Mode**
4. Click **Load unpacked**
5. Select the project directory

Then visit any Amazon product page and open the extension popup.

---

## 🔌 API Endpoints

| Method | Endpoint     | Description                              |
| ------ | ------------ | ---------------------------------------- |
| POST   | `/ask`       | Ask custom product questions             |
| POST   | `/summarize` | Summarize reviews                        |
| POST   | `/analyze`   | Analyze sentiment, strengths, weaknesses |
| POST   | `/proscons`  | Generate bulleted pros/cons              |
| POST   | `/compare`   | Compare two product names                |

---

## 🔧 Configuration

### Manifest permissions

```json
"host_permissions": [
  "https://www.amazon.com/*",
  "https://www.amazon.in/*"
]
```

### Backend endpoint in popup.js

```
http://127.0.0.1:5000/
```

---

## 📦 Dependencies

### Python

```
flask
flask-cors
groq
```

### Chrome Extension

* Vanilla JavaScript
* HTML/CSS
* Chrome Extensions API

---

## 🔐 Security Notes

* Do **not** commit your Groq API key in production
* Use environment variables for secure builds
* Backend is local-only by default—use HTTPS, auth, and strict CORS if deploying

---

## 🐞 Troubleshooting

| Issue                  | Solution                                 |
| ---------------------- | ---------------------------------------- |
| Backend not responding | Ensure Flask is running on port 5000     |
| "Loading..." stuck     | Reload extension + refresh Amazon page   |
| Reviews not showing    | Scroll review section—Amazon lazy loads  |
| CORS errors            | `flask_cors` must be installed & enabled |

---

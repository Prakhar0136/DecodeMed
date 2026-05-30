# 🧬 DecodeMed

> An intelligent, privacy-first full-stack application that transforms complex, unstructured medical lab reports into clear, visualized, and trackable longitudinal health timelines.

![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Vite](https://img.shields.io/badge/Vite-B73BFE?style=for-the-badge&logo=vite&logoColor=FFD62E)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2CA5E0?style=for-the-badge&logo=docker&logoColor=white)

## 📖 Overview

Medical data is notoriously messy, jargon-heavy, and siloed. Patients often receive disconnected physical printouts or PDFs from different laboratories, making it impossible to track chronic health trends over time.

**DecodeMed** solves this by utilizing a hybrid backend architecture (Node.js + Python). It extracts text from raw medical scans via OCR, scrubs it for privacy, normalizes laboratory nomenclature using LLMs (Google Gemini), and graphs the unified data on a secure, multi-tenant React dashboard.

## ✨ Key Features

* **Hybrid Document Extraction:** Intelligently checks for native digital PDF text (PyMuPDF) and falls back to PyTorch-driven Optical Character Recognition (EasyOCR) for physical scans and images.
* **LLM Nomenclature Normalization:** Dynamically maps varying laboratory terminology (e.g., "GLUCOSE, SERUM" vs "Fasting Blood Sugar") into a single, standardized Title Case name so historical graphs never break.
* **Clinical Guardrails:** Strictly prohibits AI hallucinations and medical diagnosing. Instead, it translates data into jargon-free summaries and generates personalized "Questions for Your Doctor."
* **Longitudinal Data Visualization:** Utilizes Recharts to plot historical patient biomarkers, allowing users to track their health trajectories visually.
* **Dynamic Status Alerting:** Automatically color-codes "High/Low" vs "Optimal" metrics, allowing patients to instantly triage what needs attention.
* **Data Portability:** Single-click CSV export grants patients total ownership of their parsed, structured medical data.
* **Secure Multi-Tenant Architecture:** Powered by Clerk Auth and MongoDB, ensuring every medical record is strictly siloed and encrypted to the authenticated user.

## 🏗️ System Architecture

1. **Frontend (Vercel):** React/Vite SPA handles Clerk authentication, file uploads, and renders the Recharts data visualizations.
2. **Backend Engine (Hugging Face Spaces):** A Dockerized Node.js Express server receives the file and triggers a child Python process.
3. **Extraction Layer:** Python runs `EasyOCR` / `PyMuPDF` to extract raw strings. Regex pipelines scrub PII (Phone numbers, emails, etc.).
4. **AI Normalization Layer:** Scrubbed text is sent to the Google Gemini API with strict JSON-schema prompting to extract specific biomarkers, reference ranges, and statuses.
5. **Database Layer:** The structured JSON is saved to MongoDB Atlas, linked strictly to the user's Clerk ID.
6. **Client Return:** The updated timeline array is returned to the frontend for immediate visual rendering.

## 🚀 Getting Started (Local Development)

### Prerequisites

* Node.js (v18 or higher)
* Python (v3.10 or higher)
* MongoDB Atlas Account
* Google Gemini API Key
* Clerk Authentication Account

### 1. Clone the Repository

```bash
git clone https://github.com/yourusername/decodemed.git
cd decodemed
```

### 2. Frontend Setup

```bash
cd frontend
npm install
```

Create a `.env` file in the frontend directory:

```env
VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key
VITE_API_URL=http://localhost:5000
```

Start the frontend development server:

```bash
npm run dev
```

### 3. Backend Setup

```bash
cd backend
npm install
pip install -r requirements.txt
```

Create a `.env` file in the backend directory:

```env
PORT=5000
MONGO_URI=your_mongodb_connection_string
GEMINI_API_KEY=your_gemini_api_key
```

```bash
node server.js
```

## ☁️ Deployment

This application is designed for a distributed cloud deployment to accommodate the heavy memory requirements of PyTorch OCR models.

**Frontend:** Deployed via Vercel for ultra-fast edge delivery.

**Backend:** Dockerized and deployed via Hugging Face Spaces (16GB RAM Free Tier) listening on port 7860.

**Database:** Hosted on MongoDB Atlas (M0 Sandbox).

## ⚠️ Medical Disclaimer

Not Medical Advice. This application is a technological demonstration of AI data parsing and visualization. It is not intended to diagnose, treat, cure, or prevent any disease. The AI-generated summaries and insights are for educational purposes only and should never replace the guidance of a qualified healthcare professional. Always consult your doctor regarding medical lab results.

## 📜 License

Distributed under the MIT License. See LICENSE for more information.

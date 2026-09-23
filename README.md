# TechEval AI: Intelligent Role Assignment System

TechEval AI is a full-stack web application designed to eliminate bias and guesswork in software team formation. By leveraging the Google Gemini API, this application dynamically generates context-aware technical assessments for team members and assigns optimal project roles based on their evaluated proficiency.

**Developer:** Ritik Chanana

## ✨ Key Features

* **Dynamic AI Assessment Generation:** Generates unique, project-specific multiple-choice questions (MCQs) utilizing Gemini's structured JSON output constraints for reliable backend parsing.
* **Intelligent Role Optimization:** Analyzes the aggregate technical accuracy of all candidates to assign distinct, optimal roles (e.g., System Architect, Developer, QA Tester, Database Engineer).
* **High-Availability Fallback Mechanism:** Engineered with a graceful degradation system. If the external LLM API experiences capacity limits (503 UNAVAILABLE) or rate limiting, the backend instantly intercepts the exception and routes to randomized, local data failovers, guaranteeing 100% application uptime.
* **Session State Management:** Securely tracks multiple concurrent candidate profiles, answers, and evaluations using Flask sessions.
* **Premium SaaS Interface:** Features a modern, responsive split-screen dashboard utilizing CSS grid and custom states for a polished user experience.

## 🛠️ Tech Stack

* **Backend:** Python 3.x, Flask
* **AI Integration:** Google Gemini API (`gemini-3.5-flash` / `gemini-1.5-flash`) via `google-generativeai`
* **Frontend:** HTML5, CSS3, Jinja2 Templating
* **Configuration:** `python-dotenv` for environment variable management
* **Data Processing:** `markdown` parser for dynamic HTML table generation

## ⚙️ Installation & Setup

### 1. Clone the Repository
```bash
git clone [https://github.com/Ritik-24/TECHEVAL-AI]
cd techeval-ai
```

### 2. Create a Virtual Environment (Recommended)
```bash
python -m venv venv
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Configure Environment Variables
Create a `.env` file in the root directory of the project and add your Google Gemini API key:
```env
GEMINI_API_KEY="your_actual_api_key_here"
```

## 🚀 Running the Application

Start the Flask server by running the main Python file:

```bash
python role_detector_app.py
```

The application will spin up on a local WSGI server. Open your web browser and navigate to:
`http://127.0.0.1:5000`

## 🏗️ Architecture & Engineering Notes

This project was built with a focus on **backend resilience** and **prompt engineering reliability**. 
* **JSON Constraints:** Instead of relying on brittle string splitting to parse LLM outputs, the MCQ generation pipeline enforces a strict JSON schema on the model. This guarantees that the Flask backend receives a predictable data structure every time.
* **Failover Logic:** Free-tier AI models often experience traffic spikes. To ensure enterprise-grade reliability, the API calls are wrapped in a robust `try/except` block. If a timeout or server error occurs, the system silently fails over to a randomized internal data pool, allowing the user to continue their assessment without encountering a 500/503 crash screen.


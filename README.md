# 🤖 AI Recruitment Agent & Autonomous Interview Platform

An end-to-end talent acquisition platform featuring **Ollama LLM resume crawling (`qwen2.5:3b`)**, **dynamic multi-role ATS matching**, **customizable Job Descriptions & technical skill benchmarks**, **instant fresher vs. experienced role assignment**, and **autonomous 7-minute voice interviews powered by 11 Curated ElevenLabs voices**.

---

## 🌟 Key Platform Features

1. **Animated Voice Assistant Landing Page**:
   - ChatGPT-style pulsing animated blue orb in the center. Clicking the orb smoothly transitions into the workspace.
   - Section 1 hero subtitle: *"Autonomous Interview Agent — Conducts autonomous 7-minute voice interviews strictly aligned with your job role requirements."*

2. **Section 1: Configured Job Roles & Requirements**:
   - Pre-configured with two primary engineering roles under **Engineering**:
     - **Associate Software Engineer**: Entry-level role for freshers and recent graduates (Min Exp: 0 months; Skills: Python, JavaScript, HTML/CSS, SQL, Git, Data Structures).
     - **Software Engineer**: Core engineering role for developers with practical hands-on, internship, or full-time experience (Min Exp: 6 months; Skills: Python, FastAPI, React, Node.js, PostgreSQL, Docker, REST APIs, Git).
   - **Full Role Customization**: Recruiters can add new roles, edit titles, update JDs, configure required skills, and toggle status.

3. **Section 2: Resume Ingestion & Ollama ATS Crawling**:
   - Drag-and-drop ingestion of PDF, DOCX, TXT, and scanned image resumes.
   - Evaluates profiles using **Local Ollama LLM (`qwen2.5:3b`)** and a comprehensive 70+ keyword technical semantic crawler.
   - **Individual & Batch Shortlisting**: Choose **"⚡ Shortlist Resume"** beside any candidate or click **"⚡ Shortlist All Resumes"** at the top right.
   - **Intelligent Role Assignment**:
     - **Freshers (0 exp / recent graduates)** $\rightarrow$ placed under `Associate Software Engineer`.
     - **Experienced developers (6+ mos / internships / full-time)** $\rightarrow$ placed under `Software Engineer`.
     - **Candidates suitable for both roles** $\rightarrow$ placed strictly under the single best, most appropriate requirement.

4. **Section 3: Shortlisted Candidates**:
   - Candidates are segregated cleanly under their matched role card with match scores (70–96%) and detected skills.
   - Click **"📞 Call (7-Min Interview)"** beside any candidate to launch an autonomous AI voice interview directly inside the browser.

5. **Section 4: Not Shortlisted Candidates**:
   - Resumes with non-technical backgrounds or lacking required programming skills are marked as **NOT SHORTLISTED** (ATS score < 50%) with clear explanations.

6. **11 Curated ElevenLabs Voices**:
   - Dedicated voice selector with live audio auditioning:
     - **Abhi** (`EMxdghWQV7gqV33j4J3F`): Authentic Telugu Male — Professional Technical Articulation
     - **Raju** (`pzxut4zZz4GImZNlqQ3H`): Natural Conversationalist — Friendly Interview Tone
     - **Amritanshu** (`1qZOLVpd1TVic43MSkFY`): Seasoned Professor — Architecture & Deep Technical Evaluation
     - **Shrey** (`x3gYeuNB0kLLYxOZsaSh`): Deep and Engaging — Authoritative Engineering Screening
     - **Chinmay** (`xnx6sPTtvU635ocDt2j7`): Raw Call Center Voice — Rapid-Fire Screening
     - **Vikrant** (`y6Ao4Y93UrnTbmzdVlFc`): Confident Motivational Speaker — Leadership & System Design
     - **Amrut Deshmukh** (`vO7hjeAjmsdlGgUdvPpe`): Energetic Influencer — Dynamic Conversational Screening
     - **Sia** (`oO7sLA3dWfQXsKeSAjpA`): Sweet & Smart Sales Professional — Consultative & Polished
     - **Monika Sogam** (`6qL48o1LBmtR94hIYAQh`): Suspense & Expressive Storyteller — Distinct Tonality
     - **Manav** (`2BsEFcU7jUhLaUwV4h7l`): Friendly, Calm & Natural — Stress-Free Technical Interview
     - **Ananya** (`ack0QsRaQyDLnVyMQTSd`): Fast Paced, Polished & Sharp — High-Velocity Evaluation

---

## 🏗️ Architecture

```
                               ┌────────────────────────┐
                               │   Web Browser Client   │
                               │  Glassmorphic UI / JS  │
                               └───────────┬────────────┘
                                           │ HTTP / Audio Playback
                                           ▼
                               ┌────────────────────────┐
                               │    FastAPI Backend     │
                               │ (Port 8000, ATS, Auth) │
                               └─────┬────────────┬─────┘
                                     │            │
               ┌─────────────────────┼────────────┼─────────────────────┐
               │                                  │                     │
               ▼                                  ▼                     ▼
       ┌──────────────┐                   ┌──────────────┐       ┌──────────────┐
       │ SQLite / DB  │                   │ Local Ollama │       │  ElevenLabs  │
       │interview_ai  │                   │ (qwen2.5:3b) │       │  TTS Voices  │
       └──────────────┘                   └──────────────┘       └──────────────┘
```

---

## 🚀 Step-by-Step Commands to Run the Project

### Method 1: Local Development (Recommended)

#### 1. Start Local Ollama LLM
Ensure Ollama is installed and running on your system:
```powershell
# In terminal 1: Start the Ollama background service
ollama serve

# In terminal 2: Verify or pull the qwen2.5:3b model
ollama run qwen2.5:3b
```
*(Type `/bye` to exit the CLI chat once verified; Ollama keeps the model loaded in memory).*

---

#### 2. Install Python Dependencies
```powershell
# From the project root folder:
pip install -r backend/requirements.txt
```

---

#### 3. (Optional) Initialize / Reset Database
To clear previous records and seed clean default roles (`Associate Software Engineer` & `Software Engineer`):
```powershell
python scripts/clean_init_db.py
```

---

#### 4. Start the Application Server
Run the FastAPI application from the project root:
```powershell
uvicorn backend.app.main:app --host 127.0.0.1 --port 8000 --reload
```
*Or from inside the `backend/` directory:*
```powershell
cd backend
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000 --reload
```

---

#### 5. Open the Web Application
Open your browser and navigate to:
- **Recruitment Web Dashboard**: [http://127.0.0.1:8000](http://127.0.0.1:8000)
- **Interactive Swagger API Docs**: [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

### Method 2: Docker Compose (Optional)
To run the containerized backend and PostgreSQL database:

```powershell
docker-compose up --build
```

---

## 📂 Project Directory Structure

```
AI Recruitment Agent/
├── .env                           # Environment configuration and API keys
├── .env.example                   # Clean template environment configuration
├── .gitignore                     # Git ignore rules for DBs, media, environments
├── docker-compose.yml             # Lean container configuration (backend + db)
├── README.md                      # Platform documentation and execution guide
├── interview_ai.db                # SQLite database
│
├── backend/                       # FastAPI Web Backend & Interview Engine
│   ├── requirements.txt           # Clean dependencies
│   ├── Dockerfile                 # Backend container definition
│   ├── alembic/                   # Database migrations
│   ├── alembic.ini                # Alembic configuration
│   └── app/
│       ├── data/
│       │   └── custom_voices.json # Curated ElevenLabs voice registry
│       ├── main.py                # FastAPI entry point & static frontend server
│       ├── config.py              # Configuration & deterministic paths
│       ├── database.py            # SQLAlchemy database engine and session
│       ├── auth.py                # Authentication and security
│       ├── models/
│       │   └── all_models.py      # Candidate, Job, Resume, and CallLog models
│       ├── routers/
│       │   ├── candidates.py      # Resume upload, ATS shortlist, delete
│       │   ├── jobs.py            # Role CRUD, JD config, required skill benchmarks
│       │   ├── calls.py           # 7-minute voice interview & ElevenLabs TTS engine
│       │   └── auth.py            # Recruiter authentication
│       └── services/
│           ├── ats_matcher.py     # Ollama LLM resume crawler & matcher
│           ├── ocr_service.py     # PDF / DOCX / Image resume text extraction
│           ├── email_service.py   # Candidate notifications
│           └── calendar_service.py# IST interview scheduling
│
├── frontend/                      # Glassmorphic Web Client
│   ├── index.html                 # Hero orb landing + 6 recruitment tabs
│   ├── style.css                  # Dark neon-cyan theme with micro-animations
│   └── app.js                     # UI controller, audio player, API client
│
├── recordings/                    # Generated 7-minute interview WAV audio files
├── uploads/                       # Ingested candidate resume documents
└── scripts/                       # Maintenance utilities
    └── clean_init_db.py           # Database reset & default role seeder
```

---

## 🧪 Resume Evaluation Verification

You can verify the resume parsing and role matching logic via CLI at any time:

```powershell
python -c "
import sys; sys.path.append('backend')
from app.services.ats_matcher import ats_matcher
from app.database import SessionLocal
from app.models.all_models import Job

db = SessionLocal()
roles = db.query(Job).filter(Job.status == 'open').all()

# Fresher Test
cand = {'name': 'Aarav Patel', 'intern_months': 0, 'fulltime_years': 0.0, 'skills': ['Python', 'SQL', 'Git'], 'raw_text': 'Recent CS Graduate. Skills: Python, SQL, Git, Algorithms.'}
res = ats_matcher.match_candidate_across_roles(cand, roles)
print('Fresher Result:', res['status'], '| Role:', res['matched_role_title'], '| Score:', res['ats_score'])
db.close()
"
```
**Expected Output:**
```
Fresher Result: shortlisted | Role: Associate Software Engineer | Score: 85.0
```

---

## 🛠️ Environment Variables Configuration (`.env`)

Configure your `.env` file in the root directory:

```ini
APP_NAME="AI Recruitment Agent API"
PORT=8000
DEBUG=True
DATABASE_URL="sqlite:///./interview_ai.db"

# Local Ollama LLM Configuration
LLM_MODEL="qwen2.5:3b"
OLLAMA_API_BASE="http://localhost:11434"
LLM_TIMEOUT_SECONDS=60

# ElevenLabs Conversational Voice Engine
ELEVENLABS_API_KEY="your_elevenlabs_api_key_here"
ELEVENLABS_VOICE_ID="EMxdghWQV7gqV33j4J3F"
```

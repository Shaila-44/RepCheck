# Commands to Run

### Step 1: Set Up Environment Files
```bash
cp api/.env.example api/.env
cp web_app/.env.example web_app/.env
```

---

## Option A: Using Docker (All-in-One)

### Step 2: Build and Run All Services
```bash
docker-compose up --build
```

---

## Option B: Running Locally

### Step 2: Start MongoDB & Redis
```bash
docker-compose up -d mongodb redis
```

### Step 3: Run Backend API (Terminal 1)
```bash
cd api
python3 -m venv env
source env/bin/activate
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

### Step 4: Run Celery Worker (Terminal 2)
```bash
cd api
source env/bin/activate
celery -A app.celery_app:celery_app worker --loglevel=info --queues=document_processing
```

### Step 5: Run Frontend (Terminal 3)
```bash
cd web_app
npm install
npm run dev
```

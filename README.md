# 🚀 Scalable Job Importer with Queue Processing & History Tracking

A production-style, scalable job import system that fetches jobs from multiple external XML feeds, processes them using a Redis queue, stores them in MongoDB, and provides an admin dashboard to monitor import history.

This project demonstrates:

✔ System design thinking  
✔ Queue-based background processing  
✔ Scalable ingestion of large datasets  
✔ Clean architecture & modular code  
✔ Real-world backend engineering practices  

---

# 📌 Tech Stack

## Backend
- Node.js
- Express.js
- MongoDB (Mongoose)
- Bull / BullMQ (Redis Queue)
- Redis
- Cron Scheduler

## Frontend
- Next.js (Admin Dashboard)
- TailwindCSS

## Dev Tools
- Docker
- Nodemon
- Dotenv
- Bull Board (Queue Monitoring UI)

---

# 🧠 Architecture

External Job APIs (XML feeds)
↓
Cron Scheduler (every 1 hour)
↓
Fetcher Service (XML → JSON)
↓
Redis Queue (Bull/BullMQ)
↓
Worker Processes (concurrency enabled)
↓
MongoDB (Jobs + Import Logs)
↓
Next.js Admin Dashboard

markdown
Copy code

---

# ✨ Features

## ✅ Job Feed Import
- Fetches jobs from multiple XML feeds
- Converts XML → JSON
- Supports multiple sources
- Runs automatically via cron

## ✅ Queue Processing
- Redis + BullMQ
- Background workers
- Configurable concurrency
- Retry support
- Failure handling

## ✅ MongoDB Upsert Logic
- Prevents duplicates
- Efficient bulk insert/update
- Handles large datasets (1M+ records)

## ✅ Import History Tracking
Each import logs:

- timestamp
- source URL (fileName)
- totalFetched
- newJobs
- updatedJobs
- failedJobs
- error reasons

## ✅ Admin Dashboard (Next.js)
- View import history
- See stats per feed
- Pagination support
- Real-time queue status

## ✅ Bull Board
- View queue state
- Active jobs
- Failed jobs
- Retry manually

---

# 📁 Project Structure

/client → Next.js frontend (dashboard)
/server → Express backend
/docs → Architecture docs
README.md

yaml
Copy code

---

# ⚙️ Setup Instructions

---

## 1️⃣ Clone repo

git clone <your-repo-url>
cd job-importer

yaml
Copy code

---

## 2️⃣ Install dependencies

### Backend
cd server
npm install

shell
Copy code

### Frontend
cd client
npm install

yaml
Copy code

---

## 3️⃣ Start Redis (Docker)

docker run --name redis -p 6379:6379 -d redis:alpine

yaml
Copy code

---

## 4️⃣ Setup Environment Variables

### server/.env

PORT=5000
MONGO_URI=mongodb://localhost:27017/job_importer

REDIS_HOST=127.0.0.1
REDIS_PORT=6379

CRON_SCHEDULE=*/60 * * * *
CONCURRENCY=5
BATCH_SIZE=100

yaml
Copy code

---

### client/.env.local

NEXT_PUBLIC_API_BASE=http://localhost:5000

yaml
Copy code

---

## 5️⃣ Start Backend

cd server
npm run dev

yaml
Copy code

---

## 6️⃣ Start Worker

npm run worker

yaml
Copy code

---

## 7️⃣ Start Frontend

cd client
npm run dev

yaml
Copy code

---

# 🚀 Usage

---

## Import jobs automatically

Cron runs every 1 hour.

OR manually trigger:

POST /import

yaml
Copy code

---

## View dashboard

http://localhost:3000

yaml
Copy code

---

## View queue monitor (Bull Board)

http://localhost:5000/admin/queues

yaml
Copy code

---

# 🗄 MongoDB Collections

## jobs
Stores normalized job records

## import_logs
Stores history of every import run

Example:

{
timestamp: Date,
fileName: "https://jobicy.com/?feed=job_feed",
totalFetched: 2000,
newJobs: 1500,
updatedJobs: 400,
failedJobs: 100
}

yaml
Copy code

---

# ⚡ Scalability Considerations

This system is designed to scale:

### ✔ Queue-based ingestion
Prevents API blocking

### ✔ Worker concurrency
Parallel processing

### ✔ Batch writes
Bulk Mongo operations

### ✔ Idempotent upserts
Avoid duplication

### ✔ Horizontal scaling ready
Multiple workers can run simultaneously

### ✔ Microservice-ready
Queue/Worker/Server can be separated

---

# 📊 Performance Strategy

- Bulk writes
- Indexing on external job ID
- Streaming XML parsing
- Redis queue for buffering
- Configurable batch size
- Retry with exponential backoff

---

# 🧪 Testing

Manual:

- Trigger import
- Check logs
- Verify Mongo
- Check dashboard

Queue status:

/admin/queues

yaml
Copy code

---

# 🎯 Design Decisions

### Why Redis Queue?
Decouples ingestion from processing → better reliability

### Why Workers?
Prevents blocking API thread

### Why Upsert?
Avoid duplicate jobs

### Why Cron?
Automated ingestion

### Why Separate import_logs?
Auditable history + monitoring

---

# 🔮 Future Improvements

- WebSocket live updates
- Pagination + filters
- Rate limiting
- Kubernetes deployment
- Distributed workers
- Caching layer
- Dead-letter queues
- Metrics with Prometheus

---

# 👨‍💻 Author

Prince Bhatt  
Full Stack Developer  

---

# ✅ Outcome

This project demonstrates the ability to:

- design scalable backend systems
- handle large datasets
- build queue-based architectures
- implement real-world engineering patterns
- deliver end-to-end solutions
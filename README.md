# 💻 Codemate — DSA CheatSheet & Interview Revision Companion

A full-stack **Data Structures & Algorithms (DSA)** revision and interview preparation web application built with **React**, **Redux Toolkit**, **Tailwind CSS**, **Material UI**, **Express**, and **MongoDB**. Organize personal revision problems with multiple solution approaches, browse curated SDE DSA sheets, filter by topic, and test recall in Rapid Fire mode.

---

## ✨ Key Features

- **📚 Curated DSA Sheets (`/sheets`, `/sheets/:sid`)**
  - Browse structured SDE problem sheets stored in MongoDB (`DsaSheet` model) with direct problem links.
- **🧠 Revision Problems & Multi-Approach CheatSheet (`/problems`)**
  - View saved coding problems in a responsive table (desktop) and card layout (mobile), complete with primary/secondary approaches (`approach_1`, `approach_2`), data structure tags, algorithm tags, and practice links.
  - Filter problems dynamically by **Data Structure** and **Algorithm** (`src/utils/problemfilter.js`).
- **➕ Add Revision Problems (`/addproblem`)**
  - Submit new problems with problem statements, multiple approaches, comma-separated data structures, and algorithms via Redux state (`slices/problemSlice.js`) persisted to `localStorage`.
- **⚡ Rapid Fire Practice Mode (`/rapidfire`)**
  - Randomized flashcard-style review cycling through unique problems (`RapidProblemCard`) with Next/Back navigation.

---

## 🛠️ Tech Stack

| Layer | Technologies |
| :--- | :--- |
| **Frontend** | React 19, Vite 7, React Router DOM v7, Redux Toolkit, React Redux, Tailwind CSS v4, Material UI (`@mui/material`, `@mui/icons-material`), Axios, GSAP, `react-icons` |
| **Backend API** | Node.js (ESM), Express 5, Mongoose 8, CORS, dotenv, `serverless-http` |
| **Database** | MongoDB |
| **Deployment** | Vercel-ready configuration (`backend/vercel.json` & `frontend/vercel.json`) |

---

## 📁 Project Structure

```text
codemate/
├── backend/
│   ├── src/
│   │   ├── lib/
│   │   │   └── db.js              # Mongoose DB_URI connection helper
│   │   ├── models/
│   │   │   ├── dsasheet.js        # DsaSheet Mongoose schema
│   │   │   └── problems.js        # Problem Mongoose schema
│   │   ├── seed/
│   │   │   └── data.js            # Seed data for SDE sheets & revision problems
│   │   └── index.js               # Express server & /sheets, /problems endpoints
│   ├── package.json
│   └── vercel.json
└── frontend/
    ├── public/
    ├── src/
    │   ├── api/
    │   │   ├── revproblems.js     # Fetches /problems into Redux
    │   │   └── sheets.js          # Fetches /sheets into Redux
    │   ├── components/            # Navbar, Footer, Filter, Tables, RapidFire, ProblemInput
    │   ├── pages/
    │   │   ├── home/              # LandingPage & Hero
    │   │   ├── rapidfire/         # Randomized RapidFire problem viewer
    │   │   ├── revisionProblems/  # Filterable revision table & mobile cards
    │   │   └── sheets/            # DSA sheet list & individual sheet problems
    │   ├── reducers/              # Input form reducer
    │   ├── slices/                # dsaSheetsSlice & problemSlice
    │   ├── store/                 # Redux store configuration
    │   ├── utils/                 # DS/Algo filter helpers & random unique picker
    │   └── App.jsx                # Application routes
    ├── package.json
    ├── vite.config.js
    └── vercel.json
```

---

## 🚀 Getting Started Locally

### Prerequisites
- Node.js (v18+ recommended)
- MongoDB connection URI (`DB_URI`)

### 1. Clone the repository
```bash
git clone https://github.com/Muqtabis/codemate.git
cd codemate
```

### 2. Backend Setup
Create a `.env` file inside `backend/`:
```env
PORT=5000
DB_URI=your_mongodb_connection_string
FRONTEND_URL=http://localhost:5173
```

Install dependencies and start the server:
```bash
cd backend
npm install
npm run dev
```
*(To seed initial DSA sheets or problems on first run, invoke `seedDb()` / `seedProblems_todb()` in `backend/src/index.js`.)*

### 3. Frontend Setup
Create a `.env` file inside `frontend/`:
```env
VITE_BACKEND_URL=http://localhost:5000
```

Install dependencies and start the Vite dev server:
```bash
cd frontend
npm install
npm run dev
```

---

## 🔌 Backend API Endpoints

| Method | Endpoint | Description |
| :--- | :--- | :--- |
| `GET` | `/` | API health greeting (`welcome codemates api`) |
| `GET` | `/sheets` | Retrieve all DSA sheets and embedded sheet problems |
| `GET` | `/problems` | Retrieve all revision problems with approaches, DS, and algorithm tags |

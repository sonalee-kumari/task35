# Workout Buddy (MERN Stack with Context API & useReducer)

A full-stack MERN application for logging and tracking workouts with a responsive UI and centralized React state management.

---

## 📁 Project Architecture

```
mern/
├── backend/
│   ├── controllers/
│   │   └── workoutController.js      # getWorkouts, createWorkout, deleteWorkout
│   ├── models/
│   │   └── workoutModel.js           # Mongoose Workout schema
│   ├── routes/
│   │   └── workouts.js               # Workout API routes
│   ├── .env                          # Server environment configuration
│   ├── .env.example
│   ├── package.json
│   └── server.js                     # Express server & DB connection
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   │   ├── Navbar.jsx            # Header with "Workout Budyyy"
│   │   │   ├── WorkoutDetails.jsx    # Card with stats, relative date & trash button
│   │   │   └── WorkoutForm.jsx       # Input form with validation & emptyFields highlight
│   │   ├── context/
│   │   │   └── WorkoutContext.jsx    # WorkoutContext & workoutsReducer
│   │   ├── hooks/
│   │   │   └── useWorkoutsContext.js # Custom hook to access context safely
│   │   ├── pages/
│   │   │   └── Home.jsx              # Responsive 2-column home page
│   │   ├── App.jsx
│   │   ├── main.jsx                  # Root entry wrapped with WorkoutContextProvider
│   │   └── index.css                 # Clean, modern design & animations
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── package.json
└── README.md
```

---

## 🚀 Getting Started

### 1. Prerequisites
- Node.js (v18+)
- MongoDB (Local instance or MongoDB Atlas URI)

### 2. Backend Setup
```bash
cd backend
npm install
npm run dev
```
By default, the server runs on `http://localhost:4000`.

### 3. Frontend Setup
```bash
cd frontend
npm install
npm run dev
```
The frontend dev server runs with Vite (default `http://localhost:5173` or `http://localhost:5174`) and automatically proxies `/api` calls to port 4000.

---

## 📡 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/api/workouts` | Fetch all workouts sorted by `createdAt` descending (`-1`) |
| `POST` | `/api/workouts` | Create a new workout (`title`, `load`, `reps`). Validates missing fields and returns 400 with `emptyFields` |
| `DELETE` | `/api/workouts/:id` | Delete workout by MongoDB ObjectId (validates ObjectId format) |

---

## 🧠 State Management (Context API + useReducer)

- **Context (`context/WorkoutContext.jsx`)**: Holds global state `{ workouts: null }`.
- **Reducer Actions**:
  - `SET_WORKOUTS`: Replaces workouts array with fetched data.
  - `CREATE_WORKOUT`: Prepends new workout to top of list `[action.payload, ...state.workouts]`.
  - `DELETE_WORKOUT`: Filters out workout matching `action.payload._id`.
- **Hook (`hooks/useWorkoutsContext.js`)**: Consumes `WorkoutContext` and throws a descriptive error if accessed outside the provider.

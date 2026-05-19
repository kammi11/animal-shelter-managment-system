# animal-shelter-managment-system
Full-stack Animal Shelter Management System with QR tracking, adoption workflows, medical records, analytics dashboard, and AI-powered insights.
# 🐾 PawTrack — Animal Shelter Management System

A complete, professional Animal Shelter Management System built with React + Node.js + SQLite.

---

## 📋 Features

- **Animal Registration** — Add animals with photo, tag number, species, breed, health info
- **Tag-Based Search** — Instant lookup by unique tag number
- **QR Code Generation** — Generate & download QR codes for each animal
- **QR Code Scanner** — Scan QR codes with device camera for instant lookup
- **Health & Medical Tracking** — Diagnoses, treatments, medications, vet visits
- **Vaccination Tracking** — Record vaccines, set due dates, get overdue alerts
- **Shelter Stay Tracking** — Auto-calculated days in shelter since entry date
- **Adoption Management** — Process adoptions, store adopter info, track fees
- **Role-Based Access Control** — Admin, Staff, Veterinarian, Volunteer roles
- **Dashboard** — Live stats, charts, species breakdown, health overview
- **Reports & Analytics** — Monthly intakes, adoptions, longest stays, overdue vaccines
- **Mobile Responsive** — Works on phones, tablets, and desktops
- **Photo Uploads** — Upload animal photos (up to 5MB)
- **Gemini AI Integration** — Optional AI-powered health analysis (via Google Gemini API)

---

## 🗂 Project Structure

```
pawtrack/
├── backend/                  # Node.js + Express API
│   ├── db/
│   │   └── database.js       # SQLite schema + seed data
│   ├── middleware/
│   │   └── auth.js           # JWT authentication middleware
│   ├── routes/
│   │   ├── auth.js           # Login, user management
│   │   ├── animals.js        # Animal CRUD + QR code
│   │   ├── medical.js        # Medical records
│   │   ├── vaccinations.js   # Vaccination records
│   │   ├── adoptions.js      # Adoption management
│   │   └── reports.js        # Analytics + alerts
│   ├── uploads/              # Uploaded animal photos (auto-created)
│   ├── server.js             # Express app entry point
│   ├── .env.example          # Environment variable template
│   └── package.json
│
├── frontend/                 # React + Vite SPA
│   ├── src/
│   │   ├── components/
│   │   │   └── Layout.jsx    # Sidebar + topbar layout
│   │   ├── context/
│   │   │   └── AuthContext.jsx
│   │   ├── pages/
│   │   │   ├── LoginPage.jsx
│   │   │   ├── Dashboard.jsx
│   │   │   ├── AnimalsPage.jsx
│   │   │   ├── AddAnimalPage.jsx
│   │   │   ├── AnimalDetail.jsx
│   │   │   ├── SearchPage.jsx
│   │   │   ├── AdoptionsPage.jsx
│   │   │   ├── ReportsPage.jsx
│   │   │   ├── UsersPage.jsx
│   │   │   └── ProfilePage.jsx
│   │   ├── utils/
│   │   │   ├── api.js        # Axios instance
│   │   │   └── helpers.js    # Utility functions
│   │   ├── App.jsx           # Router + routes
│   │   ├── index.css         # Global styles
│   │   └── main.jsx
│   ├── index.html
│   ├── vite.config.js
│   └── package.json
│
├── package.json              # Root convenience scripts
└── README.md
```

---

## ⚙️ Requirements

- **Node.js** v18 or higher — https://nodejs.org
- **npm** v8 or higher (comes with Node.js)
- A modern web browser (Chrome, Firefox, Edge, Safari)

---

## 🚀 Quick Setup (5 Minutes)

### Step 1 — Install Dependencies

Open a terminal in the project root folder and run:

```bash
npm run install:all
```

This installs all backend and frontend packages automatically.

### Step 2 — Configure Backend Environment

```bash
cd backend
cp .env.example .env
```

Open `backend/.env` and set:

```env
PORT=5000
JWT_SECRET=change_this_to_a_long_random_string_in_production
GEMINI_API_KEY=your_gemini_api_key_here   # Optional — for AI features
NODE_ENV=development
```

> **Getting a free Gemini API key:**
> 1. Go to https://aistudio.google.com/app/apikey
> 2. Sign in with your Google account
> 3. Click "Create API Key"
> 4. Paste it into your `.env` file
>
> The app works fully without the Gemini key — AI features will simply be unavailable.

### Step 3 — Start the Backend

Open **Terminal 1**:

```bash
cd backend
npm run dev
```

You should see:
```
🐾 Shelter Management API running on http://localhost:5000
Default login credentials:
  Admin:   admin / admin123
  Vet:     drsmith / vet123
  Staff:   jdoe / staff123
```

### Step 4 — Start the Frontend

Open **Terminal 2**:

```bash
cd frontend
npm run dev
```

You should see:
```
VITE ready in 300ms
➜  Local: http://localhost:3000/
```

### Step 5 — Open the App

Go to **http://localhost:3000** in your browser.

Login with any of the default credentials shown on the login page.

---

## 👤 Default User Accounts

| Role          | Username  | Password   | Access Level                          |
|---------------|-----------|------------|---------------------------------------|
| Admin         | admin     | admin123   | Full access including user management |
| Veterinarian  | drsmith   | vet123     | Medical records, vaccinations         |
| Staff         | jdoe      | staff123   | Animals, adoptions, basic operations  |

> ⚠️ **Change default passwords immediately** before using in production!

---

## 🏗 Production Deployment

### Build Frontend

```bash
cd frontend
npm run build
```

This creates a `frontend/dist/` folder with optimized static files.

### Serve with Backend

In `backend/.env`, set `NODE_ENV=production`. The Express server will serve the built frontend automatically from `../frontend/dist`.

Start with:

```bash
cd backend
npm start
```

App will be available at `http://your-server:5000`

### Recommended: Use PM2 for process management

```bash
npm install -g pm2
cd backend
pm2 start server.js --name pawtrack
pm2 save
pm2 startup
```

### Recommended: Use Nginx as reverse proxy

```nginx
server {
    listen 80;
    server_name yourdomain.com;

    location / {
        proxy_pass http://localhost:5000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }

    client_max_body_size 10M;
}
```

---

## 🔒 Security Notes for Production

1. **Change JWT_SECRET** to a long random string (32+ characters)
2. **Change all default passwords** immediately after first login
3. **Use HTTPS** — set up SSL with Let's Encrypt (free)
4. **Backup the database** regularly — it's stored at `backend/shelter.db`
5. **Backup uploads folder** — animal photos are stored at `backend/uploads/`

---

## 📱 QR Code Feature

Each animal gets a unique QR code containing their tag number.

- Go to any animal's detail page → click **QR Code** button
- Download the QR code as PNG and print it
- Attach to the animal's cage
- Staff can scan it from the **Tag Search** page using their phone camera

---

## 🤖 Gemini AI Feature (Optional)

With a Gemini API key configured, the system can:
- Analyze medical symptoms
- Suggest health assessments
- Provide care recommendations

Get a free API key at: https://aistudio.google.com/app/apikey

---

## 🗄 Database

The app uses **SQLite** — a single-file database. No database server needed.

- Database file: `backend/shelter.db` (auto-created on first run)
- To reset: delete `backend/shelter.db` and restart the backend

Tables:
- `users` — Staff accounts
- `animals` — Animal records
- `medical_records` — Health & treatment history
- `vaccinations` — Vaccination records
- `adoptions` — Adoption records
- `alerts` — System notifications

---

## 🛠 Tech Stack

| Layer     | Technology                                    |
|-----------|-----------------------------------------------|
| Frontend  | React 18, React Router 6, Recharts, Vite      |
| Backend   | Node.js, Express 4, JWT Authentication        |
| Database  | SQLite (via better-sqlite3)                   |
| Styling   | Custom CSS (no framework dependencies)        |
| QR Codes  | qrcode (generation), jsQR (scanning)          |
| AI        | Google Gemini API (free tier, optional)       |
| Photos    | Multer (local file storage)                   |

---

## ❓ Troubleshooting

**Port already in use:**
```bash
# Change port in backend/.env
PORT=5001
```

**Cannot connect to backend:**
- Make sure backend is running on port 5000
- Check `frontend/vite.config.js` proxy settings

**Photos not showing:**
- Make sure `backend/uploads/` folder exists (auto-created)
- Check that backend is running (photos are served by Express)

**Database errors:**
- Delete `backend/shelter.db` to reset and start fresh

**Camera not working for QR scan:**
- Camera access requires HTTPS or localhost
- Allow camera permission in browser settings

---

## 📞 Support

This is a complete, self-contained project. All source code is included and fully editable.

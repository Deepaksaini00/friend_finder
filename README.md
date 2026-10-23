# Friend Finder

A full-stack social app to discover and chat with new friends, searchable by **username, topic, or pincode**, with users shown on a live street map.

![SvelteKit](https://img.shields.io/badge/SvelteKit-FF3E00?logo=svelte&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind_CSS-06B6D4?logo=tailwindcss&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?logo=sqlite&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?logo=leaflet&logoColor=white)

### 👉 [**Live Demo**](https://friends.new.nkit.dev/login)

## 📸 Screenshots

| Login | Home |
|:---:|:---:|
| ![Login](docs/screenshots/login.png) | ![Home](docs/screenshots/home.png) |

| Profile | Chat |
|:---:|:---:|
| ![Profile](docs/screenshots/profile.png) | ![Chat](docs/screenshots/chat.png) |


## ✨ Features

- **Auth**: registration and login with secure, HTTP-only cookie sessions
- **Chat**: one-to-one messaging between users
- **Search**: find people by username, topic, or pincode
- **Map**: your location and other users' markers on a Leaflet street map, using the browser Geolocation API
- **Deployment**: one-command setup with Docker Compose

## 🧱 Tech Stack

| Layer | Tech | Role |
|---|---|---|
| Frontend | SvelteKit, Tailwind CSS | UI, routing, responsive layout |
| Backend | FastAPI (Python) | REST API, auth, search, chat |
| Database | SQLite | Users, profiles, messages |
| Maps | Leaflet.js | Street map and user markers |
| Deployment | Docker, Docker Compose | Containerized frontend and backend |

## 🏗️ How It Works

```
SvelteKit (UI)  ──HTTP──▶  FastAPI (API)  ──▶  SQLite
      ▲                          │
      └── session cookie ◀───────┘
```

- On login, the backend sets a session token in an HTTP-only cookie. Every later request is authorized with it.
- Search queries hit FastAPI endpoints that filter users by username, topic, or pincode.
- The frontend reads the browser's coordinates and renders users as markers with Leaflet.

## 🚀 Getting Started

**Prerequisites:** Docker, or Python 3.10+ and Node.js 18+.

```bash
git clone https://github.com/your-username/friend-finder.git
cd friend-finder
```

### Option 1: Docker (recommended)

```bash
docker-compose up --build
```

### Option 2: Run manually

**Backend**

```bash
cd backend
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn main:app --reload
```

**Frontend**

```bash
cd frontend
npm install
npm run dev
```

## 📁 Project Structure

```
friend-finder/
├── backend/
│   ├── main.py
│   ├── models/
│   └── routes/
├── frontend/
│   └── src/
│       └── routes/
├── docs/screenshots/
├── docker-compose.yml
└── README.md
```

## 🛣️ Roadmap

- [ ] Notifications
- [ ] Friend request system
- [ ] File and image sharing in chat
- [ ] UI enhancements
- [ ] PostgreSQL support

## 👤 Author

**Deepak Kumar Saini**
[GitHub](https://github.com/Deepaksaini00) · [LinkedIn](www.linkedin.com/in/deepak-saini-07d02) ·deepaksaini062005@example.com

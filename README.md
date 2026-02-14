# 🚀 NoteX
````markdown

A secure full-stack note app built with **MERN** (MongoDB, Express, React, Node.js).  

🌐 Live Demo: https://notex-1o7i.onrender.com/

---

## Features
- JWT Auth (Register/Login)  
- CRUD Notes 
- Responsive UI
- MongoDB Atlas Storage  

---

## Setup

```bash
git clone https://github.com/Mohak-787/NoteX.git
cd NoteX
````

Create `server/.env`:

```env
PORT=5000
MONGO_URI=your_mongodb_uri
JWT_SECRET=your_secret_key
```

Install & Run:

```bash
# Backend
cd server && npm install && npm start

# Frontend
cd ../client && npm install && npm start
```

---

## API

```
POST   /api/auth/register
POST   /api/auth/login
GET    /api/notes
POST   /api/notes
PUT    /api/notes/:id
DELETE /api/notes/:id
```

Protected routes need: `Authorization: Bearer <token>`

---

## Author

Mohak Devkota

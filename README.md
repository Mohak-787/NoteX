# NoteX

NoteX is a full-stack note-taking application built with the MERN ecosystem. It provides a focused CRUD workflow for creating, reading, updating, and deleting notes through a React frontend and an Express + MongoDB backend.

## Tech Stack

- **Frontend:** React, Vite, React Router, Axios, Tailwind CSS, DaisyUI
- **Backend:** Node.js, Express, Mongoose
- **Database:** MongoDB (Atlas/local)
- **Platform Services:** Upstash Redis + `@upstash/ratelimit` for API rate limiting

## Project Structure

```text
NoteX/
├── backend/          # Express API, MongoDB models, controllers, middleware
├── frontend/         # React client app (Vite)
└── README.md
```

## Features

- Create, view, edit, and delete notes
- RESTful backend API with dedicated controllers and routes
- MongoDB persistence with Mongoose models
- Global API rate limiting middleware via Upstash
- Production static serving of frontend assets from the backend

## Prerequisites

- Node.js 18+ (recommended)
- npm 9+ (or compatible npm version bundled with Node.js)
- MongoDB connection string
- Upstash Redis credentials (for rate limiting)

## Environment Variables

Create a `.env` file in `backend/`:

```env
PORT=5001
MONGO_URI=your_mongodb_connection_string
UPSTASH_REDIS_REST_URL=your_upstash_redis_rest_url
UPSTASH_REDIS_REST_TOKEN=your_upstash_redis_rest_token
NODE_ENV=development
```

> `PORT` is read from env, but the current server boot code listens on `5001` explicitly. Keep `PORT=5001` unless that code is adjusted.

## Local Development

Install dependencies:

```bash
# from repository root
npm install --prefix backend
npm install --prefix frontend
```

Run backend (Terminal 1):

```bash
npm run dev --prefix backend
```

Run frontend (Terminal 2):

```bash
npm run dev --prefix frontend
```

Frontend runs on Vite's default dev server and targets `http://localhost:5001/api` in development mode.

## Production Build and Start

From the repository root:

```bash
npm run build
npm start
```

What this does:

- Installs backend and frontend dependencies
- Builds the frontend into `frontend/dist`
- Starts the backend server
- Serves built frontend assets when `NODE_ENV=production`

## API Reference

Base URL (development): `http://localhost:5001/api`

| Method | Endpoint          | Description         |
| ------ | ----------------- | ------------------- |
| GET    | `/notes`          | Fetch all notes     |
| GET    | `/notes/:id`      | Fetch note by ID    |
| POST   | `/notes`          | Create a new note   |
| PUT    | `/notes/:id`      | Update an existing note |
| DELETE | `/notes/:id`      | Delete a note       |

### Example Request (Create Note)

```http
POST /api/notes
Content-Type: application/json

{
  "title": "Weekly goals",
  "content": "Ship NoteX README improvements."
}
```

## Rate Limiting

All API requests pass through a global rate limiter (`100` requests per `40` seconds) backed by Upstash Redis. If exceeded, the API returns HTTP `429`.

## Deployment Notes

- Set backend environment variables in your hosting provider
- Ensure `NODE_ENV=production` for static frontend serving
- Configure MongoDB and Upstash credentials securely (do not commit `.env`)

## Scripts

### Root

- `npm run build` - install dependencies and build frontend
- `npm start` - start backend service

### Backend (`backend/package.json`)

- `npm run dev` - run with nodemon
- `npm start` - run with node

### Frontend (`frontend/package.json`)

- `npm run dev` - start Vite dev server
- `npm run build` - create production build
- `npm run preview` - preview production build
- `npm run lint` - run ESLint

## Future Improvements

- Add authentication and per-user note ownership
- Add request validation (e.g., Zod/Joi) for stronger API contracts
- Add tests (unit/integration/e2e) and CI pipeline
- Add Docker support for reproducible local/prod environments


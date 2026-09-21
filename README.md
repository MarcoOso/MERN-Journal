# Journal (MERN Stack)

A full-stack journaling app built on the MERN stack (MongoDB, Express, React,
Node). Users register, log in, and write dated journal entries with optional
photos, tags, and mood/energy/sleep/productivity/stress ratings, then browse
past entries in a list or calendar view.

**Status:** not hosted live — runs locally with the setup below.

## Features

- User registration and login
- Create entries with text, up to 3 photos (stored in MongoDB via GridFS),
  tags, and mood/energy/productivity/sleep/stress ratings
- View entries in a searchable list or a calendar
- Edit and delete entries

## Tech stack

- **Frontend:** React 19 + TypeScript + Vite, React Router, FullCalendar
- **Backend:** Node/Express, MongoDB (Atlas), Multer + GridFS for image storage

## My contribution

I built the entry-retrieval endpoint (`/api/getEntries` in
[`server.js`](server.js)) and the update-entry endpoint (`/api/updateEntry`).
I also did the security hardening pass described below when preparing this
repo as a portfolio piece.

## Security hardening (post-course cleanup)

- **Live database credentials had been committed in plaintext** directly in
  `server.js` (a real MongoDB Atlas connection string). Moved to an
  environment variable (`MONGO_URI`, see `.env.example`), and the exposed
  credentials were scrubbed from git history.
- **No server-side password hashing** — passwords were stored and compared
  as plaintext. Added `bcrypt` hashing to `/api/register` and `/api/login`.

## Setup

Requires Node.js and a MongoDB connection (Atlas or local).

**Backend:**
```bash
npm install
cp .env.example .env   # then fill in MONGO_URI
npm start               # runs on http://localhost:5000
```

**Frontend:**
```bash
cd frontend
npm install
npm run dev             # proxies /api/* to localhost:5000
```

## Repo contents

- `server.js` — Express API (auth, entries, image storage via GridFS)
- `frontend/` — React + TypeScript + Vite client
- `.env.example` — required environment variables

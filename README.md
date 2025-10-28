# Axepress

Axepress is the digital noticeboard built for the Acadia University community. It replaces scattered posters and social feeds with one elegant hub where campus events, club notices, and urgent announcements are published in real time. Students discover what is happening, while administrators curate the experience through a secure, session-based workspace.

## Highlights
- Unified event and notice feed with category filters, responsive cards, and immersive hero banners
- Session-backed admin dashboard with invitation-code onboarding, bulk management, and live previews
- Calendar-ready `.ics` downloads, Google Calendar shortcuts, and smart date handling for every event
- Contact form that pipes directly to campus inboxes via Gmail App Passwords and Nodemailer
- Deployment-ready configuration for Vercel + Render + Neon, including CORS whitelisting and SSL-backed pooling

## Student & Admin Journeys
- **Students** browse featured notices, filter content by categories, deep-link to event detail pages, and add events to personal calendars with a single click.
- **Admins** authenticate with secure sessions, create and update events/notices, manage categories, and monitor usage statistics inside a purpose-built dashboard.

## Tech Stack
- **Frontend:** React 19, Vite 6, React Router 7, Axios, custom CSS modules, modern hooks-first architecture
- **Backend:** Node.js 20+, Express 4, PostgreSQL via `pg`, session management with `express-session`, validation with `express-validator`, password hashing with `bcryptjs`
- **Integrations:** Nodemailer for contact emails, ICS generator for calendar exports
- **Infrastructure:** Vercel (static hosting + SPA rewrites), Render (Express API), Neon (serverless PostgreSQL with SSL pooling)

## Getting Started Locally
### 1. Prerequisites
- Node.js 18 or newer (includes npm)
- Access to a PostgreSQL instance (Neon recommended)

### 2. Clone and Install
```bash
git clone https://github.com/sarbzcode/Axepress.git
cd Axepress

# Backend dependencies
cd backend
npm install

# Frontend dependencies
cd ../frontend
npm install
```

### 3. Environment Variables
Copy the provided examples and tailor them to your environment:
```bash
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env
```
- `backend/.env` expects your Neon `PG_URI`, a strong `SESSION_SECRET`, the admin `VALID_INVITATION_CODE`, and Gmail credentials for the contact form.
- `frontend/.env` sets `VITE_API_URL` and must point to your running Express server (`http://localhost:5000` during development).

### 4. Run the App
Open two terminals:
```bash
# Terminal 1 - backend
cd Axepress/backend
npm start  # serves on http://localhost:5000

# Terminal 2 - frontend
cd Axepress/frontend
npm run dev  # serves on http://localhost:5173
```
The Vite dev server proxies API requests to the backend using `VITE_API_URL`, enabling a full local stack that mirrors the Render deployment.

## Deployment Notes
- **Frontend on Vercel:** Commit-ready with `vercel.json` SPA rewrites. Configure `VITE_API_URL` in the Vercel dashboard to point at the Render API domain.
- **Backend on Render:** Use the Render dashboard to inject env vars from `backend/.env`. Enable persistent connections and add the Vercel domain to the CORS allow list (`server.js`).
- **Database on Neon:** Create a dedicated database branch, enable pooled connection strings, and paste the URL into `PG_URI`. SSL is enforced automatically in `db.js`.

## Key API Modules
- `GET /api/notices` - notice feed with category filtering and CRUD endpoints for admins
- `GET /api/events` - event listings, detail pages, and ICS payload creation
- `POST /api/auth/signup|login|logout` - invitation-based admin authentication
- `GET /api/categories` - taxonomy powering the homepage filter bar
- `POST /api/contact` - inbox automation for student enquiries

## Contributors
- Melita Leonie Pereira
- Sarbjot Singh
- Vishu Vishu

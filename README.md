# AUCA Dorm Management Frontend (dorm-web)

React 19 + Vite + Tailwind CSS 4 UI for the AUCA Dorm Management API. Data is pulled from the backend via `VITE_API_URL`.

## Prerequisites
- Node.js 18+
- npm
- Backend API running locally (default `http://localhost:4000`) with the database seeded

## Quick start
1. `cd Final_Project/Frontend/dorm-web`
2. `npm install`
3. Create `.env` with `VITE_API_URL=http://localhost:4000`
4. `npm run dev`
5. Open the URL shown in the terminal (typically `http://localhost:5173`)

## Scripts
- `npm run dev` — start Vite dev server with hot reload
- `npm run build` — production build to `dist/`
- `npm run preview` — preview the production build locally
- `npm run lint` — run ESLint checks

## Environment
- `VITE_API_URL` — Base URL for the backend API (include protocol). Example: `http://localhost:4000`.

## UI overview
- **Dashboard**: totals for students/rooms + occupancy %, pending payments, recent maintenance requests.
- **Search & theme**: global search bar on list tabs; light/dark toggle.
- **Students**: searchable table, add-student modal (name/email required), soft-delete.
- **Rooms**: cards with building/number/type/occupancy/facilities; add-room modal (building_id, room_type_id, room_no, status), soft-delete.
- **Payments**: table with period/amount/method/status; record-payment modal; soft-delete.
- **Maintenance**: list with category/priority/status; new-request modal; soft-delete.
- **Recovery**: restore soft-deleted students, rooms, payments, and maintenance requests (30-day window enforced by the API).

Forms expect valid IDs from the backend (e.g., `student_id`, `building_id`, `room_type_id`), so keep the database data in sync with the API.

## API dependency
All requests go to `VITE_API_URL` using the backend REST endpoints:
- `GET /api/health`, `GET /api/stats`
- Students: `GET /api/students?q=&deleted=`, `POST /api/students`, `DELETE /api/students/:id`, `POST /api/students/:id/restore`
- Rooms: `GET /api/rooms?q=&available=&deleted=`, `POST /api/rooms`, `DELETE /api/rooms/:id`, `POST /api/rooms/:id/restore`
- Payments: `GET /api/payments?q=&deleted=`, `POST /api/payments`, `DELETE /api/payments/:id`, `POST /api/payments/:id/restore`
- Maintenance: `GET /api/maintenance?q=&deleted=`, `POST /api/maintenance`, `DELETE /api/maintenance/:id`, `POST /api/maintenance/:id/restore`

Ensure the backend is running before starting the UI.

## Project layout
- `src/app.jsx` — single-page app with tabbed navigation, forms, and theme toggle
- `src/index.css` — Tailwind entrypoint and base styles
- `src/app.css` — font smoothing and reset helpers
- `index.html` — Vite entry file
- `tailwind.config.js`, `vite.config.js`, `postcss.config.js` — build/styling config
- `public/` — static assets

## Troubleshooting
- **No data or failed fetches**: confirm the backend is running and `VITE_API_URL` matches it.
- **CORS or 404/500 errors**: check backend logs and ensure the database is seeded.
- **Styles missing**: reinstall dependencies and restart `npm run dev` so Tailwind rebuilds.

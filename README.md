## Real Estate Property Management (Zikrabyte Task)

Full-stack MERN application that lets internal residential and commercial teams upload listings, share public property pages with clients, and give admins a consolidated dashboard to manage users and inventory.

### ✨ Highlights

- **Role-aware flows** for admins, residential, and commercial employees (JWT + middleware).
- **Property studio** with multi-image uploads (Cloudinary or local fallback), Google Maps preview, and auto-generated share URL `https://app.com/p/:id`.
- **Admin cockpit** with live stats, filters (area/type/search), employee CRUD, and property moderation.
- **Public property microsite** (Next.js route) with responsive gallery, pricing badges, features, and embedded map.
- **Mobile-first UI** built in Next.js 16 (App Router) + Tailwind, with protected layouts, reusable cards/forms, toast feedback, and skeleton-like loaders.

---

### 🧱 Tech Stack

| Layer      | Tech                                                                 |
| ---------- | -------------------------------------------------------------------- |
| Frontend   | Next.js 16 (App Router), TypeScript, Tailwind CSS, React Hot Toast   |
| Backend    | Node.js, Express 5, MongoDB + Mongoose, Cloudinary/Multer, JWT       |
| Auth       | bcrypt password hashing, JWT access tokens, role middleware          |
| Hosting    | Ready for Vercel (frontend) + Render/Railway (backend) deployments   |

---

### 📁 Repository Layout

```
Real_state_propertymanagment/
├── backend/           # Express API (models, controllers, routes, middleware)
├── frontend/          # Next.js app router project
└── README.md          # You are here
```

---

### ⚙️ Environment Variables

#### Backend (`backend/env.example`)

```
PORT=5000
MONGO_URI=mongodb://localhost:27017/zikrabyte_realestate
JWT_SECRET=supersecret
FRONTEND_URL=http://localhost:3000
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret
ADMIN_NAME=Zikrabyte Admin
ADMIN_EMAIL=admin@zikrabyte.com
ADMIN_PASSWORD=Admin@123
```

> If Cloudinary keys are omitted, the API falls back to storing images locally under `/uploads` and serves them via `/uploads/*`.

#### Frontend (`frontend/env.example`)

```
NEXT_PUBLIC_API_URL=http://localhost:5000
```

---

### 🚀 Getting Started (Local)

1. **Clone & install**

   ```bash
   git clone <repo-url>
   cd Real_state_propertymanagment
   ```

2. **Backend**

   ```bash
   cd backend
   cp env.example .env
   npm install
   npm run dev
   ```

   - First boot seeds an admin using `ADMIN_*` env values if no admin exists.
   - Alternatively, POST to `/api/auth/register-admin` once to bootstrap.

3. **Frontend**

   ```bash
   cd ../frontend
   cp env.example .env.local
   npm install
   npm run dev
   ```

4. Visit **http://localhost:3000** (frontend) and ensure **http://localhost:5000/api/health** returns `{"status":"ok"}`.

---

### 🔐 Sample Credentials

| Role  | Email                | Password   |
| ----- | -------------------- | ---------- |
| Admin | admin@zikrabyte.com  | Admin@123  |

Use the Admin panel to create residential/commercial employees with their own passwords.

---

### 📡 API Overview

| Method | Endpoint                       | Description                                | Auth      |
| ------ | ------------------------------ | ------------------------------------------ | --------- |
| POST   | `/api/auth/login`              | Login and receive JWT                      | Public    |
| POST   | `/api/auth/register-admin`     | Bootstrap first admin (one-time)           | Public    |
| GET    | `/api/users`                   | List employees                             | Admin     |
| POST   | `/api/users`                   | Create employee (res/com)                  | Admin     |
| PATCH  | `/api/users/:id`               | Update employee                            | Admin     |
| DELETE | `/api/users/:id`               | Delete employee                            | Admin     |
| GET    | `/api/properties`              | List properties (auto scoped for employees)| Auth      |
| GET    | `/api/properties/summary`      | Dashboard summary cards                    | Admin     |
| POST   | `/api/properties`              | Create property (type auto-set by role)    | Auth      |
| PUT    | `/api/properties/:id`          | Update property                            | Owner/Admin |
| DELETE | `/api/properties/:id`          | Delete property                            | Owner/Admin |
| GET    | `/api/properties/:id`          | Public property detail (no auth)           | Public    |
| GET    | `/api/properties/public/:id`   | Alias of above                             | Public    |

Filtering: `/api/properties?type=residential&area=Whitefield&search=2BHK`.

---

### 🖥️ Frontend Features

- Protected layouts powered by a global `AuthProvider` + `ProtectedRoute`.
- Dashboard cards (`Total`, `Today`, `Residential`, `Commercial`) + filters + table actions.
- Property form with image previews, feature tags, Google Maps embeds, and auto type selection.
- Employee management screen (create/remove) for admins.
- Public `/p/:id` microsite with gallery, rent/deposit badges, owner info, features, and embedded map.
- Toast feedback, responsive cards, and accessible buttons throughout.

---

### 📦 Deployment Notes

- **Backend:** Deploy to Render/Railway. Set env vars from `backend/env.example`. Ensure `/uploads` persists (use persistent disk or Cloudinary).
- **Frontend:** Deploy to Vercel. Set `NEXT_PUBLIC_API_URL` to deployed API URL. Next image config already whitelists Cloudinary and your backend.
- Update README with live URLs + add a short Loom/YouTube walkthrough covering:
  1. Admin login & dashboard
  2. Employee login
  3. Property creation with images/maps
  4. Visiting public share link
  5. Filters/search & employee admin actions

---

### ✅ Next Steps / Nice-to-haves

- Add pagination & date range filters on the admin table.
- Hook up charts (e.g., Residential vs Commercial pie) and skeleton loaders.
- Integrate QR-code generation for public property links.
- Expand unit/integration coverage (Jest/React Testing Library + supertest).

---

Happy shipping! 🚀


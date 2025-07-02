# 🚧 Road Safety Navigation System (RSNS) - Backend Documentation (Public)

This public repository documents the private **RSNS backend system**, a scalable geolocation-based alerting backend designed to improve road safety through user-driven hazard reporting. Built using **Node.js, TypeScript, Express, MongoDB, and Redis**, this system is under active development and is available for access upon request.

> ⚠️ Note: The actual implementation is in a private repository due to reasons including sensitive architecture details, API security concerns, and deployment configurations. This public repo only contains documentation and project structure details. To request access, please get in touch with kumarhritiksinha@gmail.com.

---

## 📚 Table of Contents

* [Overview](#Overview)
* [Tech Stack](#TechStack)
* [Architecture](#architecture)
* [Folder Structure](#folder-structure)
* [Environment Variables](#environment-variables)
* [Installation](#installation)
* [API Endpoints](#api-endpoints)
* [Testing](#testing)
* [Rate Limiting](#rate-limiting)
* [Project Flow](#project-flow)
* [Contribute](#contribute)
* [License](#license)

---

## 🧩 Overview

The RSNS backend system:

* Handles user registration, authentication, and account management.
* Supports secure hazard reporting with admin moderation.
* Utilizes geospatial queries to fetch nearby hazards.
* Returns estimated hazard arrival times without leaking exact driver coordinates.
* Implements token-based authentication, logging, and performance monitoring.

---

## 🚀 Tech Stack

* **Runtime & Language:** Node.js, TypeScript
* **Web Framework:** Express.js
* **Database:** MongoDB (Geospatial queries)
* **Cache/Queue:** Redis
* **Auth & Security:** JWT, Cookies, Bcrypt
* **Cloud Storage:** Cloudinary, Amazon S3
* **Utilities:** Multer, Winston, rate-limiter-flexible
* **Testing:** Jest, Supertest, K6, Postman
* **Containerization:** Docker

---

## 🏗️ Architecture

* Modular structure using versioned APIs (`v1/`, `v2/`...)
* Multi-layered separation: Routes → Middleware → Controller → Service → Model
* Strong emphasis on validation, logging, and request tracking
* All user-facing APIs protected via layered auth & rate limiters
* Includes performance testing and job queues (BullMQ planned)

---

## 📁 Folder Structure

```
src/
├── environmentVariables
├── statusCodes
├── v1
│   ├── __tests__
│   │   ├── unit
│   │   ├── integration
│   │   └── performance (K6)
│   ├── logs
│   │   ├── allLogs
│   │   └── productionLogs
│   ├── user
│   │   ├── constants
│   │   ├── controllers
│   │   ├── db
│   │   ├── middlewares
│   │   ├── models
│   │   ├── routes
│   │   ├── services
│   │   │   ├── cloudinary
│   │   │   └── redis
│   │   ├── utils
│   │   │   ├── api
│   │   │   ├── cookies
│   │   │   ├── handleFile
│   │   │   ├── secure
│   │   │   └── winston/logs
│   │   └── validationSchema
│   └── index.ts
├── public/profileImages
└── index.ts
```

---

## ⚙️ Environment Variables

A full list is in `.env.sample`. Includes:

* MongoDB, Redis, Cloudinary credentials
* JWT secrets, cookie configs
* Rate limiting constants

---

## 🛠️ Installation

```bash
git clone https://github.com/pythonpioneer/rsns-doc.git
cd rsns-doc
npm install
npm run dev
```

* Default health check: `http://localhost:5100/health`
* API health check: `http://localhost:5100/api/v1/health`

---

## 📬 API Endpoints

The API includes:

* `POST /api/v1/user/register` — User signup
* `POST /api/v1/user/login` — Login
* `POST /api/v1/user/logout` — Logout
* `DELETE /api/v1/user/` — Delete account
* `PUT /api/v1/user/` — Update user info
* `PATCH /api/v1/user/password` — Update password
* `PUT /api/v1/user/profile-picture` — Upload/update picture
* `DELETE /api/v1/user/profile-picture` — Delete picture
* `POST /api/v1/user/token-login` — Token-based re-login
* `POST /api/v1/hazard/report` — Report a new hazard (with location & description)
* `GET /api/v1/hazard/nearby` — Fetch nearby hazards based on the driver's coordinates
* `GET /api/v1/hazard/:id` — Get detailed info of a specific hazard
* `PATCH /api/v1/hazard/:id` — Update hazard status (admin/mod only)
* `DELETE /api/v1/hazard/:id` — Remove a hazard entry (admin/mod only

> Work is in progress...

---

## 🧪 Testing

| Type               | Tool             | Description                 |
| ------------------ | ---------------- | --------------------------- |
| Unit Tests         | Jest             | Module-level checks         |
| Integration Tests  | Supertest + Jest | Full route & DB integration |
| Performance Tests  | K6               | Load testing                |
| Manual API Testing | Postman          | Manual endpoint validation  |

To run tests:

```bash
npm run test:v1:unit
npm run test:v1:integration
```

---

## 🚦 Rate Limiting

* Configurable via `rateLimiter.constants.ts`
* Defines `points`, `duration`, `requests/day`
* Middleware located at: `middlewares/rateLimiter.ts`

---

## 🔁 Project Flow

1. Server starts → `index.ts`
2. Routes routed by version → `src/v1/index.ts`
3. Middleware chain executes (auth, validation, rate limiting)
4. The controller executes business logic
5. Response sent with logs + request ID

> Supports modular expansion with clean separation of concerns.

---

## 🤝 Contribute

This is a **documentation-only public repo**. The actual backend code is private.
Feel free to open an issue or request access if you'd like to:

* Review architecture/code
* Collaborate on backend or infra
* Suggest improvements to API design

---

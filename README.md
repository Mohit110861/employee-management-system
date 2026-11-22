# Employee Management System

A task-management dashboard for small teams, built with **React, Vite and Tailwind CSS**.
An admin creates and assigns tasks; each employee sees their own tasks grouped as **New, Active, Completed and Failed**.

> Front-end-only project: users and tasks are stored in the browser's **localStorage**, so no server or database is needed.

---

## Features

- **Role-based login**: one admin account and several employee accounts (demo data)
- **Admin dashboard**: create a task (title, description, date, category) and assign it to an employee; see every employee's task counts at a glance
- **Employee dashboard**: task counters (new, active, completed, failed) and a scrollable list of task cards, styled by status
- **Persistent session**: the logged-in user is remembered across page reloads
- Responsive layout with Tailwind CSS

## Tech stack

React 18 · Vite · Tailwind CSS · Context API · localStorage · ESLint

## Project structure

```
ems-main/
├── src/
│   ├── components/
│   │   ├── Auth/Login.jsx                 # Login form
│   │   ├── Dashboard/AdminDashboard.jsx   # Admin view
│   │   ├── Dashboard/EmployeeDashboard.jsx
│   │   ├── TaskList/                      # New / Accept / Complete / Failed task cards
│   │   └── other/                         # Header, CreateTask, AllTask, TaskListNumbers
│   ├── context/AuthProvider.jsx           # Shares employee data through Context
│   ├── utils/localStorage.jsx             # Seed data + read/write helpers
│   ├── App.jsx                            # Login handling and role routing
│   └── main.jsx
├── tailwind.config.js
└── vite.config.js
```

## Getting started

```bash
cd ems-main
npm install
npm run dev        # http://localhost:5173
npm run build      # production build in dist/
```

### Demo logins

| Role | Email | Password |
|---|---|---|
| Admin | `admin@me.com` | `123` |
| Employee | `e@e.com` | `123` |

These are hard-coded demo accounts. Authentication happens **in the browser**, so this project isn't meant for real user data.

## How it works

1. On first load, `utils/localStorage.jsx` writes sample employees (each with tasks and task counts) to localStorage.
2. `AuthProvider` reads them and shares them through React Context.
3. `App.jsx` checks the entered email and password against the admin account or the employee list, stores the session in `localStorage.loggedInUser`, and shows the matching dashboard.
4. Creating a task adds it to the chosen employee's list in React Context.

## Known limitations

- New tasks live in React state only; they aren't written back to localStorage, so they disappear on reload.
- The "Accept Task", "Mark as Completed" and "Mark as Failed" buttons are not wired up yet.

## Possible improvements

- Wire up the task buttons and persist changes to localStorage

- Move authentication and data to a back-end (Node.js/Express + MongoDB, JWT)
- Hash passwords; remove hard-coded credentials
- Replace `alert()` with inline error messages; use strict equality (`===`)
- Move the app from `ems-main/` to the repository root

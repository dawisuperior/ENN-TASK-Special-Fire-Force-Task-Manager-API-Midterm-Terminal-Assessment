# 🔥 ENN TASK: Special Fire Force Task Manager API

**Assessment:** Week 10 - Terminal Assessment 2  
**Project Choice:** Task Manager API  

## 📖 Overview
This is a secure, RESTful API built with **Node.js**, **Express**, and **SQLite**. It features full CRUD operations for task management and incorporates a custom modern frontend interface, themed after the Special Fire Force anime.

## 🛡️ Security & Authentication Method
This API utilizes **Token-Based Authentication via JSON Web Tokens (JWT)**. 

* **Secure Storage:** Passwords are encrypted and hashed using `bcrypt` before being stored in the database.
* **Session Management:** Upon successful login at `/api/auth/login`, the server issues a JWT valid for 24 hours.
* **Protected Routes:** Protected routes require this token to be sent in the header: `Authorization: Bearer <your_token>`.
* **Data Protection:** Sensitive data is protected; the user retrieval endpoint explicitly excludes passwords from the JSON response.

---

## 🚀 API Endpoints List

### 1. Authentication (Public)
* `POST /api/auth/register` - Enlists a new user.
* `POST /api/auth/login` - Authenticates a user and generates a JWT.

### 2. Users (Public)
* `GET /api/users` - Retrieves a list of all users (Safe Data: ID and Username only).

### 3. Task Management (Protected - Requires Bearer Token)
* `GET /api/tasks` - Retrieves all tasks assigned to the authenticated user.
* `POST /api/tasks` - Deploys a new task.
* `PUT /api/tasks/:id` - Updates a task's title, description, deadline, priority, or completion status.
* `DELETE /api/tasks/:id` - Purges a task from the database.

---

## 📡 Sample Requests & Responses (All Scenarios)

### Scenario 1: Registering a User (`POST /api/auth/register`)
**Request Body (JSON):**
\`\`\`json
{
  "username": "shinra",
  "password": "password123"
}
\`\`\`
**Response (201 Created):**
\`\`\`json
{
  "message": "User registered."
}
\`\`\`

### Scenario 2: Logging In (`POST /api/auth/login`)
**Request Body (JSON):**
\`\`\`json
{
  "username": "shinra",
  "password": "password123"
}
\`\`\`
**Response (200 OK):**
\`\`\`json
{
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
\`\`\`

### Scenario 3: Viewing All Users (`GET /api/users`)
**Response (200 OK):**
\`\`\`json
[
  {
    "id": 1,
    "username": "shinra"
  },
  {
    "id": 2,
    "username": "arthur"
  }
]
\`\`\`

### Scenario 4: Creating a Task (`POST /api/tasks`)
**Headers:** * `Authorization: Bearer <token>`
* `Content-Type: application/json`

**Request Body (JSON):**
\`\`\`json
{
  "title": "Purge Sector 4 Infernal",
  "description": "Target spotted near the old factory.",
  "dueDate": "2026-05-15",
  "priority": "Infernal"
}
\`\`\`
**Response (201 Created):**
\`\`\`json
{
  "id": 1
}
\`\`\`

### Scenario 5: Viewing All Tasks (`GET /api/tasks`)
**Headers:** * `Authorization: Bearer <token>`

**Response (200 OK):**
\`\`\`json
[
  {
    "id": 1,
    "user_id": 1,
    "title": "Purge Sector 4 Infernal",
    "description": "Target spotted near the old factory.",
    "due_date": "2026-05-15",
    "priority": "Infernal",
    "status": "pending"
  }
]
\`\`\`

### Scenario 6: Updating a Task (`PUT /api/tasks/:id`)
**Headers:** * `Authorization: Bearer <token>`
* `Content-Type: application/json`

**Request Body (JSON):** *(Example: Changing status to completed and priority to Minor)*
\`\`\`json
{
  "status": "completed",
  "priority": "Minor"
}
\`\`\`
**Response (200 OK):**
\`\`\`json
{
  "message": "Task updated."
}
\`\`\`

### Scenario 7: Deleting a Task (`DELETE /api/tasks/:id`)
**Headers:** * `Authorization: Bearer <token>`

**Response (200 OK):**
\`\`\`json
{
  "message": "Task purged."
}
\`\`\`

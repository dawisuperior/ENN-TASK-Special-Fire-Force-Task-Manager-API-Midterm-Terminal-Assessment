# 🔥 ENN TASK: Special Fire Force Task Manager API

**Assessment:** Week 10 - Terminal Assessment 2
**Project Choice:** Task Manager API

## 📖 Overview
This is a secure, RESTful API built with **Node.js**, **Express**, and **SQLite**. It features full CRUD operations for task management and incorporates a custom modern frontend interface, themed after the Special Fire Force.

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

## 📡 Sample Requests & Responses

### Scenario A: Registering a User (`POST /api/auth/register`)

**Request Body (JSON):**
```json
{
  "username": "shinra",
  "password": "password123"
}

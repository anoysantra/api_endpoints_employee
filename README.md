
# 🚀 FastAPI Employee Management System

A production-style backend application built using **FastAPI**, **MySQL**, and **JWT Authentication** with **Role-Based Access Control (RBAC)** for managing employees.

---

## 🏷️ Tech Stack

- ⚡ FastAPI
- 🐍 Python 3.9+
- 🗄️ MySQL
- 🔗 SQLAlchemy (ORM)
- 🔐 JWT Authentication (python-jose)
- 🚀 Uvicorn Server

---

## 📁 Project Structure
emp_fast_api_project/
│
├── main.py
├── models.py
├── schemas.py
├── database.py
├── auth.py
└── db_test.py


---

## ⚙️ Database Setup

```sql
CREATE DATABASE employee_db;

USE employee_db;

CREATE TABLE users (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(100) UNIQUE,
    password VARCHAR(255),
    user_type VARCHAR(20)
);

CREATE TABLE employees_fastapi (
    employee_id VARCHAR(10) PRIMARY KEY,
    name VARCHAR(100),
    department VARCHAR(100),
    salary FLOAT,
    email VARCHAR(100),
    address VARCHAR(200)
);

DATABASE_URL = "mysql+pymysql://root:username@localhost:3306/employee_db"

▶️ Run the Project : uvicorn main:app --reload

API Base URL: http://127.0.0.1:8000

🔐 Authentication Flow
Login API
POST /login
{
  "username": "admin",
  "password": "admin1"
}

Response
{
  "success": true,
  "status_code": 200,
  "message": "Login successful",
  "access_token": "eyJhbGciOiJIUzI1NiIs...",
  "token_type": "bearer"
}

🔑 JWT Token Usage

Use token in all protected APIs:

Authorization: Bearer <access_token>
👥 User Roles
Role	Access
admin	Full CRUD access
employee	Read-only access
🧑‍💼 Employee APIs
➕ Create Employee (ADMIN ONLY)
POST /employees
Payload
{
  "employee_id": "E101",
  "name": "Rahul Sharma",
  "department": "IT",
  "salary": 75000,
  "email": "rahul@example.com",
  "address": "Bangalore"
}
Response
{
  "success": true,
  "message": "Employee created successfully"
}
📄 Get All Employees
GET /employees
Response
[
  {
    "employee_id": "E101",
    "name": "Rahul Sharma",
    "department": "IT",
    "salary": 75000,
    "email": "rahul@example.com",
    "address": "Bangalore"
  }
]
🔍 Get Employee by ID
GET /employees/E101
✏️ Update Employee (ADMIN ONLY)
PUT /employees/E101
Payload
{
  "name": "Rahul Updated",
  "department": "Engineering",
  "salary": 90000,
  "email": "rahul_new@example.com",
  "address": "Hyderabad"
}
❌ Delete Employee (ADMIN ONLY)
DELETE /employees/E101
🔐 Role-Based Access Logic
if current_user["role"] != "admin":
    raise HTTPException(status_code=403, detail="Admin access required")
🧠 JWT Payload Example
{
  "sub": "admin1",
  "role": "admin",
  "exp": 1779536525
}
🧪 Testing Flow (Postman)
Call /login
Copy JWT token
Add header:
Authorization: Bearer <token>
Call employee APIs

# 🛠️ Backend Feature Requirements – ALX Airbnb Project

This document outlines the technical and functional specifications for three key backend features: User Authentication, Property Management, and Booking System.

---

## 1. 🧑‍💻 User Authentication

### 📌 Functional Requirements
- Users should be able to register using their name, email, and password.
- Users should be able to log in using their email and password.
- Passwords should be hashed for secure storage.
- The system should return a JWT (JSON Web Token) for authenticated sessions.

### 🌐 API Endpoints
| Method | Endpoint        | Description          |
|--------|------------------|----------------------|
| POST   | `/api/register`  | Register a new user  |
| POST   | `/api/login`     | Authenticate a user  |
| GET    | `/api/profile`   | Get user profile     |

### 🧾 Input/Output Specification

#### ✅ Register
**Input:**
```json
{
  "first_name": "Jane",
  "last_name": "Doe",
  "email": "jane@example.com",
  "password": "SecurePass123"
}


## 🏠 Property Management

### ✅ Functional Requirements

- Hosts can **create**, **update**, and **delete** their property listings.
- Each listing includes:
  - `name`
  - `description`
  - `location`
  - `price_per_night`
  - `created_at`, `updated_at` timestamps
- Only the **host who created the listing** can edit or delete it.
- All users can **view property listings**.

---

### 🌐 API Endpoints

| Method | Endpoint              | Description                   |
|--------|-----------------------|-------------------------------|
| POST   | `/api/properties`     | Create a new property (host)  |
| GET    | `/api/properties`     | Retrieve all properties       |
| GET    | `/api/properties/:id` | Retrieve a single property    |
| PUT    | `/api/properties/:id` | Update property (host only)   |
| DELETE | `/api/properties/:id` | Delete property (host only)   |


## 📅 Booking System

### ✅ Functional Requirements

- Users can **book a property** by selecting a start and end date.
- The system calculates the **total price** based on the duration of the stay and the property's nightly rate.
- Bookings are associated with both a **user** and a **property**.
- Each booking has a **status** field, which can be:
  - `pending`
  - `confirmed`
  - `cancelled`
- The system must check **property availability** to prevent overlapping bookings.

---

### 🌐 API Endpoints

| Method | Endpoint             | Description                   |
|--------|----------------------|-------------------------------|
| POST   | `/api/bookings`      | Create a new booking          |
| GET    | `/api/bookings`      | View all bookings (user)      |
| GET    | `/api/bookings/:id`  | Retrieve a single booking     |
| PUT    | `/api/bookings/:id`  | Update or cancel a booking    |

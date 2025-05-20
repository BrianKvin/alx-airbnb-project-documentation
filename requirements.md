Great! Here's the enhanced `README.md` with added sections for **Database Schema (simplified)**, **Authentication Middleware**, and **Deployment Steps** — all structured and formatted cleanly in Markdown.

---

````markdown
# 🛠️ Backend Feature Requirements – ALX Airbnb Project

This document outlines the technical and functional specifications for three key backend features: **User Authentication**, **Property Management**, and **Booking System**.

---

## 1. 🧑‍💻 User Authentication

### ✅ Functional Requirements

- Users can register using their name, email, and password.
- Users can log in using their email and password.
- Passwords must be hashed for secure storage.
- The system should return a JWT (JSON Web Token) for authenticated sessions.

### 🌐 API Endpoints

| Method | Endpoint        | Description         |
| ------ | --------------- | ------------------- |
| POST   | `/api/register` | Register a new user |
| POST   | `/api/login`    | Authenticate a user |
| GET    | `/api/profile`  | Get user profile    |

### 🧾 Input/Output Example

#### 📥 Register – Input

```json
{
  "first_name": "Jane",
  "last_name": "Doe",
  "email": "jane@example.com",
  "password": "SecurePass123"
}
```
````

---

## 2. 🏠 Property Management

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

### 🌐 API Endpoints

| Method | Endpoint              | Description                  |
| ------ | --------------------- | ---------------------------- |
| POST   | `/api/properties`     | Create a new property (host) |
| GET    | `/api/properties`     | Retrieve all properties      |
| GET    | `/api/properties/:id` | Retrieve a single property   |
| PUT    | `/api/properties/:id` | Update property (host only)  |
| DELETE | `/api/properties/:id` | Delete property (host only)  |

---

## 3. 📅 Booking System

### ✅ Functional Requirements

- Users can **book a property** by selecting a start and end date.
- The system calculates the **total price** based on the duration of the stay and the property's nightly rate.
- Bookings are associated with both a **user** and a **property**.
- Each booking has a **status** field:

  - `pending`
  - `confirmed`
  - `cancelled`

- The system must check **property availability** to prevent overlapping bookings.

### 🌐 API Endpoints

| Method | Endpoint            | Description                |
| ------ | ------------------- | -------------------------- |
| POST   | `/api/bookings`     | Create a new booking       |
| GET    | `/api/bookings`     | View all bookings (user)   |
| GET    | `/api/bookings/:id` | Retrieve a single booking  |
| PUT    | `/api/bookings/:id` | Update or cancel a booking |

---

## 🧩 Database Schema (Simplified)

### `users` Table

| Field      | Type       | Description |
| ---------- | ---------- | ----------- |
| id         | UUID / INT | Primary key |
| first_name | STRING     |             |
| last_name  | STRING     |             |
| email      | STRING     | Unique      |
| password   | STRING     | Hashed      |
| created_at | TIMESTAMP  |             |

### `properties` Table

| Field           | Type       | Description            |
| --------------- | ---------- | ---------------------- |
| id              | UUID / INT | Primary key            |
| name            | STRING     |                        |
| description     | TEXT       |                        |
| location        | STRING     |                        |
| price_per_night | DECIMAL    |                        |
| host_id         | UUID / INT | Foreign key to `users` |
| created_at      | TIMESTAMP  |                        |
| updated_at      | TIMESTAMP  |                        |

### `bookings` Table

| Field       | Type       | Description              |
| ----------- | ---------- | ------------------------ |
| id          | UUID / INT | Primary key              |
| property_id | UUID / INT | Foreign key to property  |
| user_id     | UUID / INT | Foreign key to user      |
| start_date  | DATE       |                          |
| end_date    | DATE       |                          |
| total_price | DECIMAL    |                          |
| status      | STRING     | pending, confirmed, etc. |
| created_at  | TIMESTAMP  |                          |

---

## 🛡️ Authentication Middleware

Create a middleware to verify JWTs for protected routes (e.g., profile, property creation):

```js
const jwt = require("jsonwebtoken");

function authenticateToken(req, res, next) {
  const token = req.headers["authorization"]?.split(" ")[1];
  if (!token) return res.sendStatus(401);

  jwt.verify(token, process.env.JWT_SECRET, (err, user) => {
    if (err) return res.sendStatus(403);
    req.user = user;
    next();
  });
}

module.exports = authenticateToken;
```

Use in routes:

```js
app.get("/api/profile", authenticateToken, (req, res) => {
  // Return user data
});
```

---

## 🚀 Deployment Steps

1. **Clone the repository**

   ```bash
   git clone https://github.com/your-username/airbnb-backend.git
   cd airbnb-backend
   ```

2. **Install dependencies**

   ```bash
   npm install
   ```

3. **Set environment variables**
   Create a `.env` file:

   ```
   DATABASE_URL=your_database_url
   JWT_SECRET=your_jwt_secret
   ```

4. **Run database migrations** (if using an ORM like Sequelize or Prisma)

5. **Start the server**

   ```bash
   npm start
   ```

6. **Test API with Postman or curl**

---

## ✅ Future Enhancements

- Admin panel for managing users and bookings
- Payment integration (e.g., Stripe)
- Review and rating system

---

## 🧑‍💻 Contributors

- KelvinBrian – Backend Engineer

---

```

---

```

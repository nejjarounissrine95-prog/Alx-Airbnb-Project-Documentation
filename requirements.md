# Airbnb Clone — Backend Requirement Specifications

## 1. User Authentication

###  Description
This feature allows users to **register, log in, log out, and manage their profiles** securely.  
It supports multiple roles — **Guest**, **Host**, and **Admin** — and uses **JWT (JSON Web Tokens)** for authentication.

---

###  API Endpoints

| Method | Endpoint | Description |
|--------|-----------|-------------|
| `POST` | `/api/v1/auth/register` | Register a new user |
| `POST` | `/api/v1/auth/login` | Authenticate user and return JWT token |
| `POST` | `/api/v1/auth/logout` | Invalidate user session/token |
| `GET`  | `/api/v1/auth/me` | Fetch current logged-in user profile |
| `PATCH` | `/api/v1/auth/update-profile` | Update user information |
| `DELETE` | `/api/v1/auth/delete-account` | Delete user account permanently |

---

### Request Examples

1. **Registration Request**
```json
{
  "first_name": "Nissrine",
  "last_name": "Nejjarou",
  "email": "nissrine@example.com",
  "password": "StrongPass123!",
  "role": "host"
}
``````
2. **Login Request**
```json
{
  "email": "nissrine@example.com",
  "password": "StrongPass123!"
}
``````
#### Response Examples
1. **Registration Success**
```json
{
  "user": {
    "id": "8f2a0c5b-b8b0-4b72-b6d0-7a9e77a31f0f",
    "first_name": "Nissrine",
    "last_name": "Nejjarou",
    "email": "nissrine@example.com",
    "role": "host"
  },
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
``````
2. **Login Success**
```json
{
  "message": "Login successful",
  "token": "jwt_token_here",
  "user": {
    "id": "uuid",
    "email": "nissrine@example.com",
    "role": "host"
  }
}
``````
# Authentication Service Requirements

##  Validation Rules

- **Email**
  - Must be unique
  - Must follow a valid format (user@example.com)
- **Password**
  - Minimum 8 characters
  - Must include at least 1 uppercase letter, 1 lowercase letter, and 1 number
- **First Name / Last Name**
  - Alphabetic characters only
  - Maximum 50 characters
- **Role**
  - Must be one of: `guest`, `host`, or `admin`
- **Required Fields**
  - `email`, `password`, and `role`

---

##  Performance and Security Requirements

### Password Security
- Hash all passwords using **bcrypt** before saving

### JWT Tokens
- Tokens must **expire within 1 hour**
- Use **refresh tokens** for extended sessions without re-login

### API Security
- Use **HTTPS** for all communications
- Implement **rate limiting** to prevent brute-force login attacks

### Performance
- Authentication database queries must execute in **<300ms** under normal load

---

##  Notes

- The authentication service will be the **entry point for all protected endpoints**
- Future integration with **OAuth providers** ( Google, Facebook) is planned
- Users must **verify their email** before full access is granted

---
## 2. Property Management

###  Description
This feature allows **hosts** to **create, update, delete, and manage property listings** on the platform.  
Properties include details such as **title, description, location, price, amenities, availability, and images**.  

---

###  API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST`   | `/api/v1/properties`            | Create a new property listing |
| `GET`    | `/api/v1/properties`            | Retrieve all properties (with filters) |
| `GET`    | `/api/v1/properties/:id`        | Retrieve a single property by ID |
| `PATCH`  | `/api/v1/properties/:id`        | Update property details (only owner can update) |
| `DELETE` | `/api/v1/properties/:id`        | Delete a property listing (only owner can delete) |

---

### 📥 Request Examples

1. **Create Property**
```json
{
  "title": "Cozy Apartment in Downtown",
  "description": "A comfortable 2-bedroom apartment near city center.",
  "location": "New York, NY",
  "price": 120,
  "availability": ["2025-11-01", "2025-11-02", "2025-11-03"],
  "images": ["image1.jpg", "image2.jpg"]
}
``````
2. **Update Property**
```json
{
  "price": 130,
  "availability": ["2025-11-01", "2025-11-02", "2025-11-05"]
}
``````
#### Response Examples
1. **Create Success**
```json
{
  "message": "Property created successfully",
  "property": {
    "id": "abc123-uuid",
    "title": "Cozy Apartment in Downtown",
    "host_id": "host-uuid",
    "price": 120,
    "location": "New York, NY"
  }
}
``````
2. **Update Success**
```json
{
  "message": "Property updated successfully",
  "property": {
    "id": "abc123-uuid",
    "price": 130,
    "availability": ["2025-11-01", "2025-11-02", "2025-11-05"]
  }
}
``````
# Property Service Requirements

##  Validation Rules

- **Required Fields**
  - `title`, `description`, `location`, `price` are required
- **Price**
  - Must be a positive number
- **Availability Dates**
  - Must be in valid **ISO 8601 format**
- **Images**
  - Should be valid URLs or file references
- **Ownership**
  - Only the **host who owns the property** can update or delete it

---

##  Performance and Security Requirements

- API requests must **authenticate the host via JWT**
- Database queries should execute in **<300ms** under normal load
- Only **authorized users** (property owner) can modify their listings
- Support **pagination and filtering** for large property datasets

---

##  Notes

- Future enhancement: integrate **image upload** to cloud storage (AWS S3 or Cloudinary)
- **Property search and filtering** are handled in a separate endpoint for performance optimization

## 3. Booking System

###  Description
This feature allows **guests** to **create, manage, and cancel bookings** for properties, while **hosts** can view and manage bookings for their listings.  
It ensures **availability validation, booking status tracking, and integration with payment processing**.

---

###  API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST`   | `/api/v1/bookings`             | Create a new booking |
| `GET`    | `/api/v1/bookings`             | Retrieve all bookings for a user (guest or host) |
| `GET`    | `/api/v1/bookings/:id`         | Retrieve a single booking by ID |
| `PATCH`  | `/api/v1/bookings/:id`         | Update booking details (e.g., status) |
| `DELETE` | `/api/v1/bookings/:id`         | Cancel a booking |

---

###  Request Examples

1. **Create Booking**
```json
{
  "property_id": "abc123-uuid",
  "guest_id": "guest-uuid",
  "start_date": "2025-11-01",
  "end_date": "2025-11-05",
  "number_of_guests": 2
}
```

2. **Update Booking (Cancel or Change Status)**
```json
{
  "status": "canceled"
}
```
#### Response Examples
1. **Booking Creation Success**
```json
{
  "message": "Booking created successfully",
  "booking": {
    "id": "booking-uuid",
    "property_id": "abc123-uuid",
    "guest_id": "guest-uuid",
    "start_date": "2025-11-01",
    "end_date": "2025-11-05",
    "status": "pending"
  }
}
```
2. **Booking Cancellation Success**
```json
{
  "message": "Booking canceled successfully",
  "booking": {
    "id": "booking-uuid",
    "status": "canceled"
  }
}
```

# Booking Service Requirements

##  Validation Rules

- **Required Fields**
  - `property_id`, `guest_id`, `start_date`, `end_date`, and `number_of_guests` are required
- **Date Validation**
  - `start_date` must be before `end_date`
- **Double Booking**
  - Guests cannot double-book the same property for overlapping dates
- **Ownership and Permissions**
  - Only the guest who created the booking or the host can cancel or update the booking

---

##  Performance and Security Requirements

- API requests must **authenticate the user via JWT**
- Database queries for availability and booking creation must execute in **<300ms** under normal load
- Support **pagination and filtering** for booking lists
- Ensure bookings are **transactional** to prevent race conditions and double-booking

---

##  Notes

- **Booking status workflow:** `pending` → `confirmed` → `canceled` / `completed`
- **Payment Integration** is required to confirm bookings
- **Notifications** should be sent to both guest and host when a booking is created, updated, or canceled




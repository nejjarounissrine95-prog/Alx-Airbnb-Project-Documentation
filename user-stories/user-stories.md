# User Stories — Airbnb Clone Backend

This document translates use cases from the use case diagram into user stories. Each story follows the format:  
**As a [role], I want [action] so that [goal].**

---

## Core User Stories

### 1. User registration & authentication
**As a** visitor, **I want** to register and log in using email/password (and optionally OAuth) **so that** I can create and manage my account and access protected features.

**Acceptance criteria**
- New users can sign up as Guest or Host.
- Users receive a JWT on successful login.
- Passwords are stored hashed.

---

### 2. Create and manage property listings
**As a** Host, **I want** to create, update, and delete property listings (title, description, location, price, photos, availability) **so that** I can offer my place for bookings.

**Acceptance criteria**
- Hosts can upload property images.
- Hosts can edit property details and set availability.
- Only the property owner (host) can modify or remove its listing.

---

### 3. Search and view properties
**As a** Guest, **I want** to search and filter properties by location, date, price and amenities **so that** I can find suitable places to stay.

**Acceptance criteria**
- Search supports location, date range, price range and amenities filters.
- Results are paginated for large datasets.

---

### 4. Book a property
**As a** Guest, **I want** to create a booking for selected dates **so that** I can reserve the property and receive confirmation.

**Acceptance criteria**
- System validates availability and prevents double-booking.
- Booking status is tracked (pending → confirmed → canceled/completed).

---

### 5. Payment for booking
**As a** Guest, **I want** to pay for a confirmed booking via a secure gateway (e.g., Stripe) **so that** my reservation is guaranteed and payment records are saved.

**Acceptance criteria**
- Payment is recorded in Payments table and linked to the booking.
- Booking status updates after successful payment.
- Refunds handled according to cancellation policy.

---

### 6. Reviews and ratings
**As a** Guest, **I want** to leave a review and rating after a completed stay **so that** other users can learn about the property and host.

**Acceptance criteria**
- Reviews are allowed only for completed bookings.
- Hosts can reply to reviews.

---

### 7. Host booking management
**As a** Host, **I want** to view and manage bookings for my properties **so that** I can accept, reject, or coordinate reservations.

**Acceptance criteria**
- Hosts can view booking details and change status where appropriate.
- Hosts receive notifications for new bookings/cancellations.

---

### 8. Admin moderation and monitoring
**As an** Admin, **I want** to manage users, properties, bookings, payments, and reports **so that** I can enforce platform rules and resolve disputes.

**Acceptance criteria**
- Admin can deactivate users and remove listings.
- Admin has access to logs and activity for moderation.

---

## Additional (optional) user stories

- **Wishlists:** As a Guest, I want to save favorite properties so I can book them later.  
- **Messaging:** As a Guest or Host, I want to message each other about a booking so that we can coordinate details.  
- **Notifications:** As any user, I want to receive email/in-app notifications for booking and payment events.

---

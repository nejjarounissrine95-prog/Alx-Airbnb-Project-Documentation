# Use Case Diagram Airbnb Clone Backend

## Overview
This use case diagram visualizes the interactions between actors and the backend system for the Airbnb Clone project.  
It highlights how **Guests**, **Hosts**, and **Admins** interact with key functionalities including user management, property listings, bookings, payments, and reviews.

---

## Actors
- **Guest**: Searches properties, books, pays, and leaves reviews.  
- **Host**: Manages property listings, views bookings, and receives payments.  
- **Admin**: Oversees users, properties, bookings, payments, and reviews.  
- **System** : Handles notifications and automatic updates.

---

## Use Cases
**Guest Use Cases**:  
- Register / Login / Logout  
- Search Properties  
- Book Property  
- Make Payment  
- Leave Review  
- Receive Notifications (optional)

**Host Use Cases**:  
- Register / Login / Logout  
- Create / Update / Delete Property  
- View Bookings  
- Receive Payment  
- Receive Notifications

**Admin Use Cases**:  
- Manage Users  
- Manage Properties  
- Manage Bookings  
- Manage Payments  
- Monitor Reviews

**System Use Cases (Optional)**:  
- Send Notifications (Email / In-App)  
- Automatic Booking / Payment Updates

---

## Relationships
- **Guest → Register/Login/Logout**  
- **Guest → Search Properties**  
- **Guest → Book Property**  
- **Guest → Make Payment**  
- **Guest → Leave Review**  
- **Guest → Notifications (optional)**  

- **Host → Register/Login/Logout**  
- **Host → Create/Update/Delete Property**  
- **Host → View Bookings**  
- **Host → Receive Payment**  
- **Host → Notifications (optional)**  

- **Admin → Manage Users, Properties, Bookings, Payments, Reviews**  
- **System → Send Notifications / Automatic Updates (optional)**  

- Optional dependencies:  
  - Book Property → Make Payment  
  - Book Property → Leave Review  

---

## Diagram
The use case diagram illustrating these interactions is included in this directory:  
**use-case-diagram.png**

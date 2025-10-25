# Data Flow Diagram — Airbnb Clone Backend

## Overview
This Data Flow Diagram (DFD) maps how data moves through the backend of the Airbnb Clone application.  
It shows the key external entities (users), core processes, and data stores used by the system.

## External Entities (Actors)
- **Guest** — browses properties, makes bookings, pays, and leaves reviews.  
- **Host** — creates and manages property listings and views bookings.  
- **Admin** — manages users, properties, bookings, payments, and reviews.

## Core Processes
- **User Authentication** — handles registration, login, and session validation.  
- **Property Management** — create, update, and delete property listings.  
- **Booking Management** — create, update, cancel bookings and check availability.  
- **Payment Processing** — handle payments, refunds, and payouts.  
- **Review Management** — record and retrieve property reviews.  
- **Notifications (optional)** — send email/in-app notifications triggered by events.

## Data Stores
- **Users Table** — stores user records (guests, hosts, admins).  
- **Properties Table** — stores property listings and details.  
- **Bookings Table** — stores booking records and statuses.  
- **Payments Table** — stores payment transactions and receipts.  
- **Reviews Table** — stores reviews and ratings linked to bookings.

## Key Data Flows (summary)
- Actors → Processes: Guests/Hosts/Admin send requests (e.g., login, create booking).  
- Processes → Data Stores: Processes read/write to the database (e.g., create booking → Bookings Table).  
- Processes → Actors: The system returns responses and triggers notifications (booking confirmations, payment receipts).

## Diagram
The exported diagram is included in this directory:  
**data-flow.png**

This DFD illustrates the input, processing, storage, and output for core backend operations.

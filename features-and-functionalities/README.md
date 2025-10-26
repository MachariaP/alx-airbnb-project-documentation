
# Features and Functionalities

## Overview

This document outlines the key features and functionalities of the Airbnb Clone backend, as part of the **Backend Blueprint: Feature Foundations** project. The backend provides a RESTful API (with optional GraphQL support) to manage user accounts, property listings, bookings, payments, reviews, notifications, and admin functionalities. The data model supporting these features is visualized in an Entity-Relationship (ER) diagram (`features-and-functionalities.png`), detailing entities, attributes, and relationships.

## Data Model (ER Diagram)

The ER diagram represents the database schema underpinning the backend’s features, based on the project requirements.

### Entities and Attributes
1. **Users**:
   - `user_id`: UUID (Primary Key)
   - `first_name`, `last_name`, `email` (UNIQUE), `password`: VARCHAR
   - `role`: ENUM(guest,host,admin)
   - `phone_number`: VARCHAR
   - Supports: User registration, login, profile management.
2. **Properties**:
   - `property_id`: UUID (PK)
   - `host_id`: UUID (Foreign Key to Users)
   - `title`, `location`: VARCHAR
   - `description`: TEXT
   - `price_per_night`: DECIMAL
   - `amenities`, `availability`: JSON
   - Supports: Property listings management, search and filtering.
3. **Bookings**:
   - `booking_id`: UUID (PK)
   - `property_id`, `guest_id`: UUID (FKs to Properties, Users)
   - `start_date`, `end_date`: DATE
   - `status`: ENUM(pending,confirmed,canceled,completed)
   - `total_price`: DECIMAL
   - Supports: Booking creation, cancellation, status management.
4. **Payments**:
   - `payment_id`: UUID (PK)
   - `booking_id`: UUID (FK to Bookings)
   - `amount`: DECIMAL
   - `status`: ENUM(pending,completed,refunded)
   - `method`: ENUM(credit_card,paypal)
   - `timestamp`: DATETIME
   - Supports: Payment processing, payouts, refunds.
5. **Reviews**:
   - `review_id`: UUID (PK)
   - `booking_id`, `property_id`, `guest_id`: UUID (FKs)
   - `rating`: INTEGER (1-5)
   - `comment`, `host_response`: TEXT
   - Supports: Review submission, host responses.
6. **Notifications**:
   - `notification_id`: UUID (PK)
   - `user_id`: UUID (FK to Users)
   - `type`: ENUM(booking_confirmation,cancellation,payment_update)
   - `content`: TEXT
   - `timestamp`: DATETIME
   - Supports: Notification system.

### Relationships
- **Users → Properties**: One-to-Many (host_id links a user to multiple properties).
- **Users → Bookings**: One-to-Many (guest_id links a user to multiple bookings).
- **Properties → Bookings**: One-to-Many (property_id links a property to multiple bookings).
- **Bookings → Payments**: One-to-Many (booking_id links a booking to multiple payments).
- **Bookings → Reviews**: One-to-Many (booking_id links a booking to a review).
- **Users → Reviews**: One-to-Many (guest_id links a user to multiple reviews).
- **Properties → Reviews**: One-to-Many (property_id links a property to multiple reviews).
- **Users → Notifications**: One-to-Many (user_id links a user to multiple notifications).

## Visualization

- **Diagram**: `features-and-functionalities.png`
- **Tool**: Draw.io (Diagrams.net)
- **Description**: An ER diagram showing entities (Users, Properties, Bookings, Payments, Reviews, Notifications), their attributes, and relationships (one-to-many via foreign keys). Each entity supports specific backend features (e.g., Users for authentication, Bookings for booking management).


```

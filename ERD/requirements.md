# Airbnb Database Design – Entity Relationship Diagram (ERD)

## 🎯 Objective
This document outlines the database structure for the **Airbnb Clone Project**, designed to model users, properties, bookings, and related entities. It defines entities, attributes, and relationships that will guide database implementation.

---

## 🧩 Entities & Attributes

### 1. User
| Field | Type | Description |
|-------|------|--------------|
| user_id | INT (PK) | Unique user identifier |
| first_name | VARCHAR | User’s first name |
| last_name | VARCHAR | User’s last name |
| email | VARCHAR | Unique email address |
| password | VARCHAR | Encrypted password |
| phone_number | VARCHAR | Contact number |
| role | ENUM('guest', 'host') | User’s role in the system |
| created_at | DATETIME | Account creation date |

---

### 2. Property
| Field | Type | Description |
|-------|------|--------------|
| property_id | INT (PK) | Unique property identifier |
| host_id | INT (FK) | Links to User (Host) |
| title | VARCHAR | Property name or headline |
| description | TEXT | Property details |
| price_per_night | DECIMAL | Nightly cost |
| property_type | VARCHAR | e.g. Apartment, House |
| max_guests | INT | Maximum guest capacity |
| location_id | INT (FK) | Links to Location |
| created_at | DATETIME | Date listed |

---

### 3. Location
| Field | Type | Description |
|-------|------|--------------|
| location_id | INT (PK) | Unique location identifier |
| country | VARCHAR | Country name |
| city | VARCHAR | City name |
| address | VARCHAR | Street address |
| latitude | FLOAT | Geo coordinate |
| longitude | FLOAT | Geo coordinate |

---

### 4. Booking
| Field | Type | Description |
|-------|------|--------------|
| booking_id | INT (PK) | Unique booking identifier |
| guest_id | INT (FK) | Links to User (Guest) |
| property_id | INT (FK) | Links to Property |
| start_date | DATE | Booking start date |
| end_date | DATE | Booking end date |
| total_price | DECIMAL | Total cost |
| booking_status | ENUM('pending', 'confirmed', 'cancelled') | Status of booking |
| created_at | DATETIME | Date created |

---

### 5. Payment
| Field | Type | Description |
|-------|------|--------------|
| payment_id | INT (PK) | Unique payment identifier |
| booking_id | INT (FK) | Links to Booking |
| payment_date | DATETIME | Date of payment |
| amount | DECIMAL | Payment amount |
| payment_method | VARCHAR | e.g. Card, PayPal |
| payment_status | ENUM('paid', 'failed', 'pending') | Payment outcome |

---

### 6. Review
| Field | Type | Description |
|-------|------|--------------|
| review_id | INT (PK) | Unique review identifier |
| booking_id | INT (FK) | Links to Booking |
| reviewer_id | INT (FK) | Links to User (Reviewer) |
| rating | INT | Rating (1–5) |
| comment | TEXT | Review content |
| created_at | DATETIME | Date created |

---

### 7. Amenity
| Field | Type | Description |
|-------|------|--------------|
| amenity_id | INT (PK) | Unique amenity identifier |
| name | VARCHAR | Amenity name |
| description | TEXT | Description |

---

### 8. Property_Amenity
| Field | Type | Description |
|-------|------|--------------|
| property_id | INT (FK) | Links to Property |
| amenity_id | INT (FK) | Links to Amenity |

---

## 🔗 Relationships
- **User → Property:** One-to-Many (a host can list multiple properties)
- **User → Booking:** One-to-Many (a guest can make multiple bookings)
- **Property → Booking:** One-to-Many (a property can have multiple bookings)
- **Booking → Payment:** One-to-One (each booking has one payment)
- **Booking → Review:** One-to-One (each booking can have one review)
- **Property → Location:** Many-to-One (many properties share one location)
- **Property ↔ Amenity:** Many-to-Many (handled via Property_Amenity)

---

## 🗂 Directory Structure

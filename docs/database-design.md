# Database Design Documentation

## 1. Overview

This document describes the database design for **Rent Adda**, a smart parking system developed as a national-level exhibition project. The database is designed using a **relational SQL model** and serves as the backbone for user management, parking space listing, booking workflows, and administrative control.

The primary objectives of the database design are:

* Data consistency and integrity
* Clear separation of roles and responsibilities
* Simplicity suitable for a prototype while remaining extensible for future production use

The database is implemented using **MySQL**, hosted locally via **XAMPP**, and accessed through PHP scripts.

---

## 2. Design Principles

The database design follows standard industry and academic principles:

* **Normalization**: Core entities are separated to reduce redundancy
* **Role-based modeling**: Different user roles are stored and managed explicitly
* **Relational integrity**: Logical relationships exist between users, parking spaces, and administrative actions
* **Scalability readiness**: Schema can be extended to support payments, sensors, and real-time occupancy in the future

---

## 3. Entity Overview

The database consists of the following core entities:

1. Admin
2. Owner
3. Parker
4. Parking Space / Cost Information (`cost_info`)

Each entity corresponds to a table in the database and represents a real-world actor or resource in the system.

---

## 4. Table Definitions

### 4.1 Admin Table

**Purpose:**
Stores administrator account details. Admins are responsible for verifying owners, supervising listings, and maintaining system integrity.

**Key Responsibilities:**

* Approve or reject owner registrations
* Monitor registered parking spaces
* Perform system-level oversight

**Logical Fields:**

* Admin ID (Primary Key)
* Name
* Email
* Phone Number
* Password (hashed)
* Account Status
* Created Timestamp

---

### 4.2 Owner Table

**Purpose:**
Stores information about users who register parking spaces or land for rent.

**Key Responsibilities:**

* Register parking spaces
* Define pricing and availability
* Manage their listed properties

**Logical Fields:**

* Owner ID (Primary Key)
* Name
* Email
* Phone Number
* Password (hashed)
* Verification Status (Approved / Rejected / Pending)
* Address / Location Details
* Registered Timestamp

**Notes:**
Owner accounts become active only after admin verification.

---

### 4.3 Parker Table

**Purpose:**
Stores information about end-users who search for and use parking spaces.

**Key Responsibilities:**

* Discover nearby parking spaces
* Select and use available spaces
* View parking history

**Logical Fields:**

* Parker ID (Primary Key)
* Name
* Email
* Phone Number
* Password (hashed)
* Account Status
* Created Timestamp

---

### 4.4 Cost_Info Table (Parking Space Table)

**Purpose:**
Stores details about parking spaces registered by owners, including pricing and availability.

**Key Responsibilities:**

* Represent each parking slot or location
* Track availability and cost
* Support booking and selection workflows

**Logical Fields:**

* Space ID (Primary Key)
* Owner ID (Foreign Key – references Owner)
* Location (Address / Latitude / Longitude)
* Price Per Hour
* Availability Status (Available / Occupied)
* Active Days / Timings
* Created Timestamp

---

## 5. Relationships Between Tables

* **Admin → Owner**

  * Admins verify and approve owner registrations

* **Owner → Cost_Info**

  * One owner can register multiple parking spaces

* **Parker → Cost_Info**

  * Parkers interact with parking spaces for selection and usage (logical relationship)

These relationships are enforced logically through application-level constraints and foreign keys where applicable.

---

## 6. ER-Level Relationship Summary (Textual)

* Admin (1) → (Many) Owner
* Owner (1) → (Many) Parking Spaces
* Parker (Many) → (Many) Parking Spaces (conceptual, via booking/usage)

This design ensures a clear hierarchy and separation of control.

---

## 7. Authentication & Security Considerations

* Passwords are stored in hashed form within their respective tables
* OTP verification is handled via external services and is not persisted permanently in the database
* Session-based authentication is managed at the application layer (PHP)

---

## 8. Limitations of Current Database Design

* No dedicated booking or transaction table
* No payment-related entities
* No real-time sensor or occupancy data
* No audit or logging tables

These limitations align with the project’s scope as a prototype and exhibition-level implementation.

---

## 9. Future Enhancements

The database schema can be extended to include:

* Booking and reservation tables
* Payment and transaction records
* QR-code based slot locking
* Sensor-based real-time occupancy tables
* Analytics and reporting entities

---

## 10. Conclusion

The database design of Rent Adda provides a structured, role-based, and extensible foundation for a smart parking system. While intentionally simple to suit the project’s scope, it follows standard relational design principles and can be evolved into a production-ready schema with minimal restructuring.


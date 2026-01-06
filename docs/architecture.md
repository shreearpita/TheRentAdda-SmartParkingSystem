## Overview
The Rent Adda is a web-based Smart Parking System designed to address parking unavailability and traffic
congestion issues commonly observed in Tier-1 and Tier-2 cities in India. The system enables vehicle users
to discover nearby available parking spaces while allowing landowners to rent out unused land or spaces
for parking purposes. The project was developed and demonstrated as a fully functional prototype at a
national-level CBSE exhibition.

The architecture focuses on clarity of roles, simplicity of deployment, and feasibility of implementation
within academic and infrastructural constraints. While not production-deployed, the system demonstrates a
complete end-to-end workflow covering user authentication, space listing, discovery, selection, and
administrative supervision

## High-Level Architectural Diagram
### Diagram Overview
The following diagram represents the high-level architecture of the Rent Adda Smart Parking System. It
illustrates the interaction between users, the web application, backend services, database, and external
integrations.

![High-Level Architectural Diagram](https://github.com/shreearpita/TheRentAdda-SmartParkingSystem/blob/main/docs/HL%20Arch.png)
### Architectural Explanation
**End Users** interact with the system through a standard web browser. All three roles (Admin, Owner,
Parker) use the same application with role-based dashboards.

**Frontend Layer** provides the user interface and basic client-side validation. It communicates with
the backend using HTTP form submissions and JavaScript-triggered requests.

**Backend Layer (PHP)** acts as the core of the system:

-Handles authentication and OTP verification

-Enforces role-based access control

-Processes parking space listings, selection, and administrative approvals

-Manages interaction with both the database and external services

**MySQL Database** stores persistent system data, including users, owners, parking space information,
and authentication credentials.

**Google Maps API** is integrated to support:

-Location detection

-Visualization of nearby parking spaces

-Distance-based discovery

**OTP Service** is used for secure authentication via email and phone-based verification.

This architecture ensures clear separation of responsibilities while remaining simple enough for a prototype
and academic demonstration environment.

### Architectural Style
The Rent Adda is implemented as a server-rendered, database-driven web application. The system follows a
classic three-layer logical separation:

- **Presentation Layer:** HTML, CSS, and JavaScript rendered in the browser
  
- **Application Layer:** PHP scripts handling business logic and workflows
  
- **Data Layer:** MySQL relational database for persistent storage
  
The architecture prioritizes simplicity, role separation, and feasibility for a prototype-scale deployment while
maintaining clear control flows and data consistency.

## Technology Stack

**Frontend:** HTML, CSS, JavaScript

**Backend:** PHP

**Database:** MySQL (SQL)

**Server Environment:** XAMPP (Apache + MySQL, localhost)

**External Services:**

- Google Maps API (location & visualization)

- Third-party OTP service (email and phone verification)

## Component Breakdown

### Frontend Layer

**Multi-page web interface**

- Separate dashboards and UI flows for Admin, Owner, and Parker

- Pages are role-specific and rendered using HTML and CSS

**Client-side logic (JavaScript)**

- Form validation (login, registration, updates)

- Basic UI interactivity (select parking space, submit actions)

- Error handling before form submission

**User Interaction**

- Users interact with the system through a browser using HTTP requests

- Each major action (login, register, book, update) maps to a backend PHP script

**Maps Visualization**

- Google Maps is used on the Parker dashboard to display nearby parking locations using markers

### Backend Layer

**PHP Application Layer**

- Each functional page is backed by a corresponding PHP script
(e.g., login.html → login.php, owner_dashboard.html → owner_dashboard.php)

**Authentication & Authorization**

- Handles user login and registration

- OTP verification via third-party services (email and phone)

- Role-based access control ensures Admin, Owner, and Parker can only access permitted actions

**Business Logic**

- Owner space registration and updates

- Admin approval or rejection of owner registrations

- Parking space listing, availability updates, and selection logic

**Session Management**

- PHP sessions are used to maintain authenticated user state across requests

**External Service Integration**

- Google Maps API for location visualization

- OTP service API for secure user verification

### Database Layer
**Relational SQL Database (MySQL via XAMPP)**

- Used for persistent storage of users, parking spaces, and system data

- All database interactions are handled through PHP scripts

**Core Tables**

- admin
Stores administrator account details and credentials used for system supervision and approvals

- owner
Stores verified owner information, including login details and registered parking spaces

- parker
Stores parker (end-user) account details and parking activity history

- cost_info
Stores parking space metadata such as location, pricing, availability status, and timing

**Data Handling**

- Authentication credentials are stored directly within respective user tables (admin, owner, parker)

- PHP scripts perform CRUD operations for:

    - User registration and login

    - Owner verification and approvals

    - Parking space creation, updates, and selection

    - Availability and pricing management
      
## Data Flow Archotecture
The data flow architecture describes how information moves through the system across different user roles
and system components. Rent Adda follows a request–process–persist–respond pattern, where user
actions trigger backend processing, database updates, and UI responses.

![Data Flow Architecture](https://github.com/shreearpita/TheRentAdda-SmartParkingSystem/blob/main/docs/Data%20Architecture.png)
### Role Based Flow
**Owner Registration & Verification** 
1. Owner submits registration data
2. Data stored as unverified
3. Admin reviews and approves
4. Owner gains listing privileges

**Parking Space Listing** 
1. Verified owner submits space details
2. Data stored in cost_info table
3. Space becomes visible to parkers
   
**Parker Discovery & Selection** 
1. Parker logs in
2. Location retrieved via Google Maps API
3. Nearby spaces queried from database
4. Parker selects a space using Select/Book option
   
**Authentication Flow** 
1. User submits credentials
2. OTP generated and delivered
3. OTP validated
4. Session created

### Conceptual Extensions
- QR-code-based slot locking

- Entry/exit-based availability updates

### Database Design
**Core Tables**
- admin: Stores administrator details
- owner: Stores verified owner information
- cost_info: Stores parking space data (location, price, availability)
- parker: Stores parker's account detail and activity

**Relationships**
- Admin verifies Owners
- Owners manage multiple parking spaces
- Parkers interact with parking spaces through selection and booking
  
A detailed database schema, table relationships, and field-level design are documented separately in the [Database Design](database-design.md) document.

## API & External Services Integration 

## Authentication & Authorization Flow

## Deployment Architecture

## Design Decisions & Trade-offs

## Scalability Considerations

## Limitations & Known Constraints

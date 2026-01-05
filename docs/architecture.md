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

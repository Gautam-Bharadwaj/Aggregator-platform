# Aggregator Platform: Local Rental Marketplace

## Project Overview
A multi-role marketplace application designed to aggregate local car, bike, and scooty rental vendors into a single unified platform. The goal is to provide users with real-time access to the nearest verified rental options, ensuring price transparency and easy booking.

## Core Roles
* **User:** Searches for nearby vehicles, compares prices, and books instantly.
* **Vendor:** Manages their fleet, updates availability, and tracks earnings.
* **Admin:** Oversees platform security, vendor onboarding, and dispute resolution.

---

## Key Features

### 1. Smart Discovery
* **Hyper-Local Search:** Displays vehicles based on the user's current GPS location.
* **Real-Time Inventory:** Live status updates ensure that users only see vehicles that are currently available.

### 2. Trust & Security
* **Verified Vendors:** Every rental shop undergoes a verification process before listing.
* **In-App KYC:** Seamless digital verification of user driving licenses and ID proofs.

### 3. Booking Management
* **OTP-Based Handover:** Secure vehicle pickup and return process using unique codes.
* **Dynamic Pricing:** Automated price calculation based on rental duration (hourly/daily).

---

## Technical Architecture



* **Frontend:** Cross-platform mobile application (Flutter or React Native).
* **Backend:** Scalable API services (Node.js or Python).
* **Database:** Relational database (PostgreSQL) for transactions and Redis for real-time tracking.
* **Maps:** Integration with Google Maps API for geofencing and routing.

---

## Workflow Logic

```mermaid
flowchart TD
    Start((Start)) --> Search[User searches nearby]
    Search --> Filter[System filters verified vendors]
    Filter --> Select[User selects vehicle]
    Select --> KYC{KYC Verified?}
    KYC -- No --> Verify[Upload Documents]
    Verify --> Pay
    KYC -- Yes --> Pay[Process Payment]
    Pay --> OTP[Generate Pickup OTP]
    OTP --> Handover[Vendor verifies OTP & Handover]
    Handover --> End((End))

# Sequence Diagram: Vehicle Booking Flow

## Actors
* **User:** Booking karne wala person.
* **App/System:** Frontend interface aur backend logic.
* **Payment Gateway:** Transaction handle karne wala service.
* **Vendor:** Gaadi ka owner.

## Workflow Steps

1. **Search:** User location aur vehicle type enter karta hai.
2. **Fetch:** System database se nearest available vehicles filter karke dikhata hai.
3. **Select:** User apni pasand ki gaadi select karta hai.
4. **Validation:** System user ke documents (KYC) check karta hai.
5. **Payment:** User payment process shuru karta hai.
6. **Confirmation:** Payment successful hone par Vendor ko notification milta hai.
7. **OTP Generation:** System hand-over ke liye ek unique OTP generate karta hai.

---

## Mermaid Visual Logic

```mermaid
sequenceDiagram
    participant User
    participant System
    participant PaymentGateway
    participant Vendor

    User->>System: Search Vehicle (Type, Location)
    System->>System: Filter nearest available fleet
    System-->>User: Show Results
    
    User->>System: Select Vehicle & Book
    System->>System: Verify User KYC
    
    User->>PaymentGateway: Process Payment
    PaymentGateway-->>System: Payment Success
    
    System->>Vendor: Notify Booking Details
    Vendor-->>System: Accept Booking
    
    System->>User: Send Booking Confirmation & OTP
    System->>Vendor: Share User Details & OTP Trigger

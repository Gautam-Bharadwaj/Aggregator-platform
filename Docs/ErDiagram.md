# ER Diagram: Aggregator-Platform

## Entities and Attributes

### 1. User
* **user_id** (Primary Key)
* name
* email
* phone_number
* driving_license_no
* aadhar_no
* is_verified (Boolean)

### 2. Vendor
* **vendor_id** (Primary Key)
* shop_name
* owner_name
* location_coordinates (Lat/Lng)
* address
* contact_number
* verification_status

### 3. Vehicle
* **vehicle_id** (Primary Key)
* **vendor_id** (Foreign Key)
* vehicle_type (Car/Bike/Scooty)
* model_name
* registration_number
* hourly_rate
* daily_rate
* is_available (Boolean)

### 4. Booking
* **booking_id** (Primary Key)
* **user_id** (Foreign Key)
* **vehicle_id** (Foreign Key)
* start_time
* end_time
* total_amount
* status (Pending/Active/Completed/Cancelled)
* otp_code (For hand-over)

### 5. Review
* **review_id** (Primary Key)
* **booking_id** (Foreign Key)
* rating (1-5)
* comment
* target_type (User_to_Vendor / Vendor_to_User)

---

## Relationships

* **Vendor to Vehicle:** One-to-Many (Ek vendor ke paas bahut saari gaadiyan ho sakti hain).
* **User to Booking:** One-to-Many (Ek user multiple bookings kar sakta hai).
* **Vehicle to Booking:** One-to-Many (Ek gaadi ki history mein bahut saari bookings ho sakti hain).
* **Booking to Review:** One-to-One (Har booking ke liye ek review cycle hota hai).

---

## Mermaid Flow (Visual Logic)

```mermaid
erDiagram
    USER ||--o{ BOOKING : places
    VENDOR ||--o{ VEHICLE : owns
    VEHICLE ||--o{ BOOKING : reserved_in
    BOOKING ||--|| REVIEW : generates

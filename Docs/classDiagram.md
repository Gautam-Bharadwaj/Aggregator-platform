# Class Diagram: Vehicle Rental Aggregator

## Classes and Methods

### 1. User
* **Attributes:**
    - int userId
    - String name
    - String email
    - String phoneNumber
    - String licenseDetails
    - Boolean isVerified
* **Methods:**
    - searchVehicle(location, type)
    - bookVehicle(vehicleId, duration)
    - uploadDocuments(type, file)
    - makePayment(amount)

### 2. Vendor
* **Attributes:**
    - int vendorId
    - String shopName
    - String address
    - Coordinates location
    - List fleetList
* **Methods:**
    - addVehicle(vehicleDetails)
    - updateAvailability(vehicleId, status)
    - confirmBooking(bookingId)
    - viewEarnings()

### 3. Vehicle (Abstract Class)
* **Attributes:**
    - int vehicleId
    - String model
    - String plateNumber
    - double basePrice
    - Boolean isAvailable
* **Methods:**
    - getDetails()
    - calculateRent(hours)

### 4. Bike / Car / Scooty (Sub-classes of Vehicle)
* **Specific Attributes:**
    - FuelType (Petrol/Electric)
    - cc (for bikes)
    - seatingCapacity (for cars)

### 5. Booking
* **Attributes:**
    - int bookingId
    - User user
    - Vehicle vehicle
    - DateTime startTime
    - DateTime endTime
    - String status
* **Methods:**
    - generateOTP()
    - calculateTotalFare()
    - updateStatus(newStatus)

### 6. Payment
* **Attributes:**
    - int paymentId
    - int bookingId
    - double amount
    - String paymentMethod
    - String transactionStatus
* **Methods:**
    - processTransaction()
    - refund()

---

## Relationships

* **Inheritance:** Car, Bike, aur Scooty `Vehicle` class se inherit hote hain.
* **Association:** `User` aur `Booking` ke beech 1:M relationship hai.
* **Composition:** `Vendor` ke paas multiple `Vehicle` objects hote hain.
* **Dependency:** `Booking` class `Payment` class par depend karti hai transaction completion ke liye.

---

## Mermaid Visual Logic

```mermaid
classDiagram
    class User {
        +int userId
        +searchVehicle()
        +bookVehicle()
    }
    class Vendor {
        +int vendorId
        +addVehicle()
        +updateAvailability()
    }
    class Vehicle {
        +int vehicleId
        +String model
        +Boolean isAvailable
    }
    class Booking {
        +int bookingId
        +generateOTP()
        +updateStatus()
    }
    class Payment {
        +int paymentId
        +processTransaction()
    }

    User "1" --> "*" Booking : places
    Vendor "1" --o "*" Vehicle : manages
    Vehicle <|-- Car
    Vehicle <|-- Bike
    Booking "1" -- "1" Payment : settles
    Booking "*" o-- "1" Vehicle : reserves

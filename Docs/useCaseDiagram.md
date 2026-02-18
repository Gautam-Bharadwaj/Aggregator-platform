# Use Case Diagram: Vehicle Rental Aggregator

## Actors
1. **User (Customer):** Jo rentals dhoond raha hai.
2. **Vendor (Shop Owner):** Jo gaadiyan provide kar raha hai.
3. **Admin:** Jo platform ko monitor aur verify kar raha hai.
4. **Payment Gateway (External):** Jo transactions handle kar raha hai.

## Use Cases

### 1. User Use Cases
* **Register/Login:** Account banana aur KYC documents upload karna.
* **Browse Vehicles:** Filter aur proximity ke hisaab se gaadiyan dekhna.
* **Book Vehicle:** Rental request place karna.
* **Make Payment:** Secure transaction complete karna.
* **Rate Service:** Vendor aur gaadi ka review dena.

### 2. Vendor Use Cases
* **Manage Fleet:** Gaadiyan add, remove ya update karna.
* **Manage Availability:** Live status toggle karna.
* **Verify Booking:** User ka OTP check karke gaadi hand-over karna.
* **View Earnings:** Weekly/Monthly payouts track karna.

### 3. Admin Use Cases
* **Verify Vendor:** Business legit hai ya nahi check karna.
* **Resolve Disputes:** User ya Vendor ki complaints handle karna.
* **Manage Commissions:** Platform fees track karna.

---

## Mermaid Visual Logic
```mermaid
flowchart TD
    Start((Start)) --> Search[User searches for vehicle]
    Search --> Find[System finds nearest vendors]
    
    Find --> Avail{Vehicles Available?}
    Avail -- No --> NoFound[Show No Vehicles Found]
    NoFound --> End((Stop))
    
    Avail -- Yes --> List[Display list of vehicles]
    List --> Select[User selects a vehicle]
    
    Select --> KYC{User KYC Verified?}
    KYC -- No --> Upload[Redirect to KYC Upload]
    Upload --> Verify[Admin verifies documents]
    Verify --> Summary
    KYC -- Yes --> Summary[Show Booking Summary]
    
    Summary --> Pay[Process Payment]
    
    Pay --> PayCheck{Payment Success?}
    PayCheck -- No --> Error[Show Payment Error]
    Error --> Summary
    
    PayCheck -- Yes --> Confirm[Confirm Booking & OTP]
    Confirm --> Notify[Notify Vendor]
    Notify --> Reach[User reaches Vendor Location]
    Reach --> OTP[Vendor verifies OTP]
    OTP --> StartRent[Start Rental Period]
    StartRent --> Return[User returns vehicle]
    Return --> Final[Vendor confirms return]
    Final --> Invoice[Generate Invoice & Rating]
    Invoice --> End

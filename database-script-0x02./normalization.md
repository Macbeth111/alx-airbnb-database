AirBnb Database
Apply Normalisation principle (1NF, 2NF, 3NF)
Apply 1NF - First normal forms

Entity Separation

user entity
property entity
booking entity
review entity
payment entity
message entity

Remark: each entity contains unique data, no column should contain a list or array values

Apply 2NF - Second normal forms

Enity separation with no dependancy:

    user entity: Must contain only user data, id: [primary key]

    property entity: Must contain only property data, id: [primary key], host_id [foreign key].

    booking entity: Must contain only booking data, id: [primary key], user_id [foreign key]

    review entity: Must contain only review data, id: [primary key], user_id [foreign key] property_id [foreign key]

    payment entity: Must contain only payment data, id: [primary key], booking_id [foreign key]

    message entity: Must contain only message data, id: [primary key], sender_id [foreign key] recipient_id [foreign key]

Remark: relationships must be enforced using foreign keys, no duplicate data (1NF) applied

Apply 3NF - Third normal forms

No Transitive Dependencies
*Remove total_price from Booking table
*Add locked_pricepernight for scalability and audit tracking

Remark: 
- Upholds 3NF by eliminating derived data.
- Scales better for real-world financial systems.
- Simplifies audits with immutable price snapshots


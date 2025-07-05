High-Usage Columns Identified:
Users Table:

    user_id (PRIMARY KEY) - Used in JOINs, WHERE clauses
    email (UNIQUE) - Authentication, user lookup
    role (ENUM) - Access control, filtering
    created_at (TIMESTAMP) - Date range queries, analytics

Bookings Table:

    id (PRIMARY KEY) - Booking lookup, JOINs
    user_id (FOREIGN KEY) - User booking history, JOINs
    property_id (FOREIGN KEY) - Property booking history, JOINs
    start_date (DATE) - Date range queries, availability checks
    end_date (DATE) - Date range queries, availability checks
    status (ENUM) - Booking status filtering
    created_at (TIMESTAMP) - Date range queries, analytics

Properties Table:

    id (PRIMARY KEY) - Property lookup, JOINs
    host_id (FOREIGN KEY) - Host property listings, JOINs
    location (VARCHAR) - Location-based searches
    price_per_night (DECIMAL) - Price filtering, sorting
    created_at (TIMESTAMP) - Date range queries, analytics

Indexes Created:
Single Column Indexes:

    Users: role, created_at
    Bookings: user_id, property_id, start_date, end_date, status, created_at
    Properties: host_id, location, price_per_night, created_at

Composite Indexes:

    idx_bookings_dates_range - For availability checks
    idx_bookings_user_status - For user booking status queries
    idx_properties_host_location - For host property searches
    idx_properties_price_location - For location-based price searches

Performance Measurement Queries:

The script now includes 11 realistic performance measurement queries that cover:

    User authentication (high frequency)
    User booking history (dashboard queries)
    Property availability checks (critical booking system)
    Host property listings (host dashboard)
    Location-based searches (common functionality)
    Booking status analysis (admin/reporting)
    User activity analysis (analytics)
    Index usage monitoring
    Query performance tracking
    Index effectiveness analysis

This comprehensive approach ensures optimal performance for the most common query patterns in an Airbnb-like booking system!

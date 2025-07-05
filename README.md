# **AirBnB Clone Database Join Queries**

---

## **Retrieve Bookings with Users that Booked Them**

**INNER JOIN Bookings with Users**

```sql
SELECT 
    bookings.booking_id,
    bookings.booking_date,
    users.user_id,
    users.first_name,
    users.last_name
FROM 
    bookings
INNER JOIN 
    users ON bookings.user_id = users.user_id
ORDER BY 
    bookings.booking_date DESC;
```

---

## **Retrieve Properties and Property Reviews**

```sql
SELECT 
    properties.id AS property_id,
    properties.name AS property_name,
    reviews.rating,
    reviews.comment,
    reviews.created_at AS review_date
FROM        
    properties
LEFT JOIN 
    reviews ON properties.id = reviews.property_id
ORDER BY 
    properties.name ASC,
    reviews.created_at DESC;
```

---

## **Retrieve All Users**

```sql
SELECT 
    users.user_id,
    users.first_name,
    users.last_name,
    bookings.booking_id,
    bookings.booking_date
FROM 
    users
FULL OUTER JOIN 
    bookings ON users.user_id = bookings.user_id
ORDER BY 
    users.user_id ASC,
    bookings.booking_date DESC;
```

---

## **Retrieve Properties that Have Average Rating Above 4.0**

```sql
SELECT 
    properties.id AS property_id,
    properties.name AS property_name,
    AVG(reviews.rating) AS is_high_rating
FROM 
    properties
INNER JOIN 
    reviews ON properties.id = reviews.property_id
GROUP BY 
    properties.id, properties.name
HAVING 
    AVG(reviews.rating) > 4.0;
```

---

## **Retrieve Users with More Than 3 Bookings**

```sql
SELECT * FROM users
WHERE 
    (SELECT COUNT(*) FROM bookings WHERE bookings.user_id = users.user_id) > 3;
```

---


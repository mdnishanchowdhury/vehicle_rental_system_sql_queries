# Vehicle Rental System Database Project

## Project Overview
This project is a simplified **Vehicle Rental System** database designed to manage **users**, **vehicles**, and **bookings** efficiently.  
It demonstrates the use of **SQL queries**, relational database concepts, and **ERD design** to represent relationships between tables.

### Project Objectives
- Design and implement a relational database for a vehicle rental system.  
- Create SQL queries to manage and retrieve data efficiently.  
- Represent database structure using an **ERD**.  
- Prepare professional documentation for submission.

---

## Database Tables

1. **Users** – Stores customer and admin information:
   - `user_id` (Primary Key)  
   - `name`, `email`, `phone`, `role`, `password`  

2. **Vehicles** – Stores details of vehicles available for rent:
   - `vehicle_id` (Primary Key)  
   - `name`, `type`, `registration_number`, `rental_price`, `status`  

3. **Bookings** – Stores booking information linking users and vehicles:
   - `booking_id` (Primary Key)  
   - `user_id` (Foreign Key → Users)  
   - `vehicle_id` (Foreign Key → Vehicles)  
   - `start_date`, `end_date`, `total_cost`, `status`  

---

## SQL Queries & Solutions

### Query 1: Retrieve booking information with customer and vehicle details
```sql
SELECT
  b.booking_id,
  u.name AS customer_name,
  v.name AS vehicle_name,
  b.start_date,
  b.end_date,
  b.total_cost,
  b.status
FROM
  bookings AS b
  INNER JOIN users AS u ON b.user_id = u.user_id
  INNER JOIN vehicles AS v ON b.vehicle_id = v.vehicle_id;


Concepts Used: INNER JOIN
Explanation:
This query joins the bookings, users, and vehicles tables to display booking details along with the customer name and vehicle name.


Query 2: Find all vehicles that have never been booked
SELECT
  *
FROM
  vehicles AS v
WHERE
  NOT EXISTS (
    SELECT 1
    FROM bookings AS b
    WHERE b.vehicle_id = v.vehicle_id
  );


Concepts Used: NOT EXISTS
Explanation:
This query finds all vehicles that do not have any bookings using a NOT EXISTS subquery.

Query 3: Retrieve all available vehicles of a specific type
SELECT
  *
FROM
  vehicles
WHERE
  type = 'bike'
  AND status = 'available';


Concepts Used: SELECT, WHERE
Explanation:
This query filters the vehicles table to display only vehicles of type "bike" that are currently available for rent.

Query 4: Find vehicles with more than 2 bookings
SELECT
  v.vehicle_id,
  v.name AS vehicle_name,
  COUNT(b.booking_id) AS total_bookings
FROM
  vehicles AS v
  INNER JOIN bookings AS b ON v.vehicle_id = b.vehicle_id
GROUP BY
  v.vehicle_id,
  v.name
HAVING
  COUNT(b.booking_id) > 2;


Concepts Used: GROUP BY, HAVING, COUNT
Explanation:
This query counts the total bookings for each vehicle and displays only vehicles that have been booked more than twice.

ERD (Entity-Relationship Diagram)

One-to-Many: Users → Bookings

Many-to-One: Bookings → Vehicles

One-to-One (logical): Each booking connects exactly one user and one vehicle

ERD Link: [Your Lucidchart or ERD Tool Public Link]

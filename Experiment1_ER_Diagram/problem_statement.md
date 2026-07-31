# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
<img width="1035" height="671" alt="image" src="https://github.com/user-attachments/assets/e1b1b045-0d8f-4a37-b38a-13032a814e92" />


## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---------|----------------------|-------|
| Member | MemberID (PK), Name, PhoneNo | Stores member details. |
| Trainer | TrainerID (PK), TrainerName, PhoneNo | Stores trainer details. |
| Session | Time, Plan | Stores session information. |
| Payment | PaymentID (PK), Amount, DateOfPay | Stores payment details. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Member — Workout — Trainer | M:N | Partial | A member can work out with multiple trainers, and a trainer can train multiple members. |
| Workout — Program — Session | 1:M | Total (Session) | A workout is associated with one or more sessions. |
| Member — Payment | 1:M | Total (Payment) | A member can make multiple payments, and each payment belongs to one member. |

---

## Assumptions

- Each member has a unique MemberID.
- Each trainer has a unique TrainerID.
- Members can train with multiple trainers.
- Trainers can train multiple members.
- Payments are made only by registered members.
- Session information consists of a plan and scheduled time.

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
<img width="1031" height="685" alt="image" src="https://github.com/user-attachments/assets/c270dc70-865d-451a-8c43-c10e8343ccc9" />


## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---------|----------------------|-------|
| Member | MemberID (PK), Name, Phone | Stores library member details. |
| Book | BookID (PK), Title, Author, Category, LoanDate, ReturnDate, FineAmount | Stores book details and borrowing information. |
| Event | EventID (PK), EventName, EventDate, SpeakerName | Stores cultural event details and speaker information. |
| Room | RoomID (PK), RoomName, Capacity | Stores rooms used for events and study sessions. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Member — Borrows — Book | M:N | Partial | A member can borrow multiple books, and a book can be borrowed by different members over time. |
| Member — Registers — Event | M:N | Partial | Members can register for multiple events, and each event can have many members. |
| Room — Hosts — Event | 1:M | Total (Event) | Each event is conducted in one room, while a room can host multiple events. |

---

## Assumptions

- Each member has a unique MemberID.
- Each book has a unique BookID.
- LoanDate and ReturnDate are stored with the Book entity for simplicity.
- FineAmount is recorded only when a book is returned after the due date.
- Speaker information is stored as the SpeakerName attribute of the Event entity.
- A room can be used for both cultural events and study sessions.

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
<img width="1062" height="681" alt="image" src="https://github.com/user-attachments/assets/ac748e5b-e7de-4e0e-be65-014d5c4661f7" />


## Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|---------|----------------------|-------|
| Customer | CustomerID (PK), Name, Phone | Stores customer details. |
| Reservation | ReservationID (PK), ReservationDate, ReservationTime, NoOfGuests, TableNo | Stores reservation information for customers. |
| Order | OrderID (PK), DishName, Category, Quantity | Stores food orders placed for a reservation. |
| Bill | BillID (PK), FoodCharge, ServiceCharge, TotalAmount | Stores billing information for each reservation. |

---

## Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|-------------|---------------|-------|
| Customer — Makes — Reservation | 1:M | Partial | A customer can make multiple reservations or walk in. |
| Reservation — Places — Order | 1:M | Total (Order) | Each reservation can have multiple food orders. |
| Reservation — Generates — Bill | 1:1 | Total (Bill) | Every reservation generates exactly one bill. |

---

## Assumptions

- Each customer has a unique CustomerID.
- Walk-in customers are also recorded as customers.
- Dish category (Starter, Main Course, Dessert) is stored as an attribute of the Order entity.
- Each reservation is assigned a table number.
- Each bill includes both food charges and service charges.
```

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**

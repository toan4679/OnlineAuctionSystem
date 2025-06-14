# 🗃️ Table Design – Online Auction System

This section describes the structure of the main tables in the system.

---

## 1. Users

| Field Name   | Data Type       | Description                       |
|--------------|------------------|-----------------------------------|
| UserId       | INT (PK)         | Unique identifier for each user   |
| Username     | NVARCHAR(100)    | Unique username                   |
| Password     | NVARCHAR(255)    | Hashed password                   |
| Email        | NVARCHAR(150)    | Email address                     |
| Role         | NVARCHAR(20)     | 'admin', 'seller', 'buyer'        |
| Status       | NVARCHAR(10)     | 'active', 'blocked'               |
| CreatedAt    | DATETIME         | Date of account creation          |

---

## 2. Categories

| Field Name     | Data Type      | Description                          |
|----------------|----------------|--------------------------------------|
| CategoryId     | INT (PK)       | Unique identifier                    |
| CategoryName   | NVARCHAR(100)  | Name of the product category         |

---

## 3. Items

| Field Name     | Data Type        | Description                          |
|----------------|------------------|--------------------------------------|
| ItemId         | INT (PK)         | Unique item ID                       |
| Title          | NVARCHAR(100)    | Item title                           |
| Description    | NVARCHAR(4000)   | Detailed description                 |
| MinBid         | DECIMAL(10,2)    | Minimum bid price                    |
| BidIncrement   | DECIMAL(10,2)    | Minimum increase in bids             |
| StartDate      | DATETIME         | Auction start date                   |
| EndDate        | DATETIME         | Auction end date                     |
| BidStatus      | CHAR(1)          | 'A' for active, 'I' for inactive     |
| CategoryId     | INT (FK)         | Link to category                     |
| SellerId       | INT (FK)         | Link to user who posted the item     |
| CreatedAt      | DATETIME         | Listing creation time                |

---

## 4. Bids

| Field Name   | Data Type        | Description                         |
|--------------|------------------|-------------------------------------|
| BidId        | INT (PK)         | Unique bid ID                       |
| ItemId       | INT (FK)         | Related item ID                     |
| BidderId     | INT (FK)         | User who placed the bid             |
| BidAmount    | DECIMAL(10,2)    | Amount of the bid                   |
| BidTime      | DATETIME         | When the bid was placed             |

---

## 5. Documents

| Field Name   | Data Type        | Description                          |
|--------------|------------------|--------------------------------------|
| DocumentId   | INT (PK)         | Unique ID                            |
| ItemId       | INT (FK)         | Related item                         |
| FilePath     | NVARCHAR(255)    | Path to uploaded document            |
| UploadedAt   | DATETIME         | Timestamp of upload                  |

---

## 6. Notifications

| Field Name     | Data Type       | Description                          |
|----------------|------------------|--------------------------------------|
| NotificationId | INT (PK)         | Unique ID                            |
| UserId         | INT (FK)         | Recipient of the notification        |
| Message        | NVARCHAR(MAX)    | Notification content                 |
| Seen           | BIT              | Whether notification was read        |
| CreatedAt      | DATETIME         | Notification timestamp               |

---

## 7. Ratings

| Field Name   | Data Type        | Description                          |
|--------------|------------------|--------------------------------------|
| RatingId     | INT (PK)         | Unique rating ID                     |
| ItemId       | INT (FK)         | Related item                         |
| RatedBy      | INT (FK)         | User who rated                       |
| RatedTo      | INT (FK)         | User who was rated                   |
| Score        | INT              | From -5 to +5                        |
| Comment      | NVARCHAR(MAX)    | Optional feedback                    |

---

# 📊 Database Diagram (ER-style)

```
[Users] 1---* [Items] 1---* [Bids]
   |               |
   |               *---* [Documents]
   |
   *---* [Ratings]

[Users] 1---* [Bids]

[Items] *---1 [Categories]

[Items] 1---* [Notifications]
```

This diagram shows the relationships between core tables in the database.


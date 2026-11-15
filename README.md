# Task 3 — SQL Joins (INNER, LEFT, RIGHT, FULL)

A hands-on SQL project demonstrating how to **combine data from multiple related tables** using different types of SQL `JOIN` operations.

---

## 🎯 Objective

Learn to combine data from multiple tables using SQL Joins. Understand how different join types affect the output when there are matching and non-matching records between two tables.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **DB Browser for SQLite** | Run queries locally |
| **MySQL Workbench** | Alternative environment (simulates FULL JOIN via `UNION`) |
| **GitHub** | Version control & submission |

---

## 🗄️ Database Schema

**Database name:** `task3`

### 1. `customers`
| Column | Type | Description |
|--------|------|-------------|
| `customer_id` | INTEGER (PK) | Unique customer ID |
| `customer_name` | VARCHAR(50) | Customer name |
| `city` | VARCHAR(30) | City of residence |
| `email` | VARCHAR(60) | Customer email |
| `join_date` | DATE | Date of registration |

### 2. `orders`
| Column | Type | Description |
|--------|------|-------------|
| `order_id` | INTEGER (PK) | Unique order ID |
| `customer_id` | INTEGER (FK) | References `customers.customer_id` (Nullable) |
| `product` | VARCHAR(40) | Product purchased |
| `quantity` | INTEGER | Units purchased |
| `unit_price` | DECIMAL(10,2) | Price per unit |
| `order_date` | DATE | Date of order |

---

## 📊 Joins Covered

### 🔹 INNER JOIN
| # | Query | Concept |
|---|-------|---------|
| 1 | Customers with their orders | `INNER JOIN` matches only |
| 2 | Total order amount per customer | `INNER JOIN` + `SUM` |

### 🔹 LEFT JOIN
| # | Query | Concept |
|---|-------|---------|
| 3 | All customers with their orders (if any) | `LEFT JOIN` (keeps all left) |
| 4 | Find customers with NO orders | `LEFT JOIN` + `WHERE ... IS NULL` |

### 🔹 RIGHT JOIN
| # | Query | Concept |
|---|-------|---------|
| 5 | All orders with their customers (if any) | `RIGHT JOIN` |
| 6 | Simulated RIGHT JOIN (SQLite workaround) | Swapped `LEFT JOIN` |
| 7 | Find orders with NO customer | `LEFT JOIN` + `IS NULL` |

### 🔹 FULL OUTER JOIN
| # | Query | Concept |
|---|-------|---------|
| 8 | All customers and all orders | Native `FULL OUTER JOIN` (SQLite 3.39+) |
| 9 | Simulated FULL JOIN using UNION | `LEFT JOIN UNION RIGHT JOIN` |

---

## 💻 Sample Queries (Highlights)

### INNER JOIN — Matches Only
```sql
SELECT c.customer_name, o.order_id, o.product, o.quantity, o.unit_price
FROM customers c
INNER JOIN orders o ON c.customer_id = o.customer_id
ORDER BY c.customer_name;
```

### LEFT JOIN — Find Unmatched Records
```sql
SELECT c.customer_name, c.city
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.order_id IS NULL;
```

### FULL OUTER JOIN 
```sql
SELECT c.customer_name, o.order_id, o.product
FROM customers c
FULL OUTER JOIN orders o ON c.customer_id = o.customer_id
ORDER BY c.customer_name, o.order_id;
```


### Simulated FULL JOIN using UNION
```sql
-- Another Way of doing Full Outer Join
-- Note: FULL OUTER JOIN is not supported in all SQL databases, so we use "UNION" as an alternative.

SELECT c.customer_name, o.order_id, o.product
FROM customers c
LEFT JOIN orders o ON c.customer_id = o.customer_id

UNION

SELECT c.customer_name, o.order_id, o.product
FROM orders o
LEFT JOIN customers c ON c.customer_id = o.customer_id
ORDER BY customer_name;
```

---

## 🎓 Learning Outcomes

By completing this task, I gained hands-on experience with:

- **INNER JOIN** — retrieving only matching rows from both tables.
- **LEFT JOIN** — keeping all rows from the left table, even unmatched ones.
- **RIGHT JOIN** — keeping all rows from the right table.
- **FULL OUTER JOIN** — combining all rows from both tables.
- **Simulating FULL JOIN** — using `UNION` of LEFT + RIGHT joins.


---

## ✅ Conclusion

This task gave me a **strong foundation in combining data from multiple related tables** using SQL joins. I learned that:

- **INNER JOIN** is the most common — it returns only matches.
- **LEFT JOIN** is essential when you must **keep all records from one table**, even without matches.
- **RIGHT JOIN** is the mirror of LEFT JOIN — useful when you want all rows from the "right" side.
- **FULL OUTER JOIN** is the most inclusive — nothing is left out.

---

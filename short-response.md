# Short Response: Schema Design and Normalization

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1

The table below stores data for a library's checkout system. Identify every normalization rule it violates and describe how you would fix the schema. You do not need to write SQL — describe the tables you would create and why.

| checkout_id | patron_id | patron_name | patron_email     | book_id | book_title                | author_name       | genres                   |
| ----------- | --------- | ----------- | ---------------- | ------- | ------------------------- | ----------------- | ------------------------ |
| 1           | 10        | Maya Patel  | maya@email.com   | 201     | The Left Hand of Darkness | Ursula K. Le Guin | Science Fiction, Fantasy |
| 2           | 11        | Jordan Kim  | jordan@email.com | 202     | Beloved                   | Toni Morrison     | Fiction, Historical      |
| 3           | 10        | Maya Patel  | maya@email.com   | 202     | Beloved                   | Toni Morrison     | Fiction, Historical      |
| 4           | 12        | Sam Torres  | sam@email.com    | 201     | The Left Hand of Darkness | Ursula K. Le Guin | Science Fiction, Fantasy |

**Your answer:**

**Normalization Rule #2**: The genres columns do not store **atomic** values, making it harder to manage the database and to find the exact value through **query** search.

**Normalization Rule #3**: The table will cause a lot of **repetitive and redundant** data when updating data on a column, since some data repeat we would need to **update** each row of the data we want to update.

**Solution**: The best way to fix the **schema** design is to make **multiple** tables that each serve a purpose. A **patron**'s table tells us details about each customer, and a **book**'s table tells us details about each book while changing the `checkout_id` values from `integer` to `status`.

---

## Question 2

Explain the difference between one-to-many relationships and many-to-many relationships by providing a real world example of each. Then describe how each is represented in a relational database. Use the term "association/bridge" table in your response.

**Your answer:**

A **One-to-many** relationship is where one row in table A can be referenced by many rows in table B: Like the `shows` on a `TV channel`. A **Many-to-many** relationship is where rows in each table can reference many rows in the other: you can think of it like `authors` in `books`. While a TV channel can have multiple shows in its table, an author can have many books, and a book can have multiple authors. This **association** create an connetion that **bridges** the many tables together.  


---

## Question 3

What is referential integrity? How does PostgreSQL enforce it, and why does this enforcement determine the order in which you must create — and drop — tables?

**Your answer:**

**Referential integrity** is when the database itself adds a **clause** to make sure that the value being added is real data. PostgreSQL **enforces** this by rejecting anything inserted that doesn't **exist** in the table.

---

## Question 4

Why does an association table need a `UNIQUE (col1, col2)` constraint on its two foreign key columns? What specific problem does this prevent, and why wouldn't making each column individually `UNIQUE` solve it?

**Your answer:**

When an association table has **two or more** foreign key columns, it might make a row with the same data as a **previous** row. Adding a `UNIQUE` constraint, it prevents two rows from sharing the same `col1` and `col2` pair. Making the constraint a pair prevents the same `col1` from being in the same `col2` twice

---

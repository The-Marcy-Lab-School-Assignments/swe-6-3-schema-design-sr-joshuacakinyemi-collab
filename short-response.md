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

**1NF**: The genres columns do not store **atomic** values, making it harder to manage the database and to find the exact value through **query** search or filtering.

**2NF and 3NF**: The table will cause a lot of **repetitive and redundant** data when updating data on a column, since some data repeat we would need to **update** each row of the data we want to update.

**Solution**: The best way to fix the **schema** design is to **split** the table into separate tables, each responsible for one thing. A **patron**'s table(`patron_name`, `email`),a **authors** table(`author_name`), a **books** table(`title`, `author_id`), a **book_genres**(`book_id`, `genres_id`) bridge table to handle the many-to-many relationship between books and genres, and lastly a **checkouts** table(`checkout_id`,`patron_id`,`book_id`, and a data to note when it was taken out).

---

## Question 2

Explain the difference between one-to-many relationships and many-to-many relationships by providing a real world example of each. Then describe how each is represented in a relational database. Use the term "association/bridge" table in your response.

**Your answer:**

A **One-to-many** relationship is where one row in table A can be referenced by many rows in table B: Like the `shows` on a `TV channel`. A **Many-to-many** relationship is where rows in each table can reference many rows in the other: you can think of it like `authors` in `books`. While a TV channel can have multiple shows in its table, an author can have many books, and a book can have multiple authors. This **association** create an connetion that **bridges** the many tables together.  


---

## Question 3

What is referential integrity? How does PostgreSQL enforce it, and why does this enforcement determine the order in which you must create — and drop — tables?

**Your answer:**

**Referential integrity** is to check if the **foreign key** column points to a existing row in the table it references. **PostgreSQL** checks every insert or update against the referenced table and **rejects** the operation if no matching row exists there. so when making the tables, PostgreSQL check for the **parent** before the **child** since the child need a **vaild** reference in order to be made, and vice versa in order to drop, PostgreSQL need to drop child before the parent.

---

## Question 4

Why does an association table need a `UNIQUE (col1, col2)` constraint on its two foreign key columns? What specific problem does this prevent, and why wouldn't making each column individually `UNIQUE` solve it?

**Your answer:**

When an association table has **two or more** foreign key columns, it might make a row with the same data as a **previous** row. Adding a `UNIQUE` constraint, it prevents two rows from sharing the same `col1` and `col2` pair. Making the constraint a pair prevents duplicate row from appearing twice. Making each column individually `UNIQUE` would not work, because in a normal **many-to-many** relationship each foreign key value is supposed to repeat across multiple rows.

---

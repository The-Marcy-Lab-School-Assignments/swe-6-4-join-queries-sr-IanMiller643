# Short Response: JOIN Queries and Connecting to Postgres

Answer each question below. Write in complete sentences (3–5 per answer).

---

## Question 1

What is the difference between `INNER JOIN` and `LEFT JOIN`? Give a concrete example of when you would use each.

**Your answer:**

While both `INNER JOIN` and `LEFT JOIN` combine the rows of two tables together, `INNER JOIN` will only return the rows that have a match in both tables. `LEFT JOIN` however returns all of the rows on the left table, and will fill in a `NULL` value for columns where the right table values don't have a match. 

An example of this would be if we had a restaurant database with a customers table and an orders table. If we only want the customers that have already made an order, we would use `INNER JOIN`. If we wanted all of the customers, regardless of whether or not they made an order, we would use `LEFT JOIN`. 

---

## Question 2

Look at this query. What will it return, and why do users with zero bookmarks still appear in the results?

```sql
SELECT users.username, COUNT(bookmarks.bookmark_id) AS total_bookmarks
FROM users
LEFT JOIN bookmarks ON users.user_id = bookmarks.user_id
GROUP BY users.user_id;
```

**Your answer:**

This query will return the username of all users and the number of bookmarks each of them have created. The users with zero bookmarks still appear in the results because a `LEFT JOIN` is used instead of an `INNeR JOIN`.

---

## Question 3

What is the `pg` library and why can't you write SQL directly in a `.js` file without it? And what is a connection pool?

**Your answer:**

Since JavaScript and SQL are completely different languages, you can't natively write SQL into `.js`. This is where the `pg` library comes in and connects the JavaScript file with a postgreSQL database, allowing you to write SQL inside of a `.query()` function. In order for an application to better handle these queries, we use a connection pool to open up multiple re-usable connections to queries.

---

## Question 4

What is a parameterized query and what problem does it solve? Rewrite the unsafe query below as a safe parameterized query using `pg`:

```js
// Unsafe — never do this!
pool.query(`SELECT * FROM users WHERE username = '${username}'`);
```

**Your answer:**

A parameterized query allows us to separate the SQL command from the data and send them to the database separately. This prevents malicious users from inputting SQL injections to mess with our database.

Parameterized query:
```js
pool.query(`SELECT * FROM users WHERE username = $1`, [username]);
```

---

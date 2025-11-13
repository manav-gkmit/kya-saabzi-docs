# Database Indices

Defines the structure and relationships of the database entities that power Kya Saabzi’s core features.

---

## Single index on `users(username)` {data-toc-label="On username"}

```sql
CREATE UNIQUE INDEX idx_username 
ON users(username);
```

Example:

```sql
SELECT id, email 
FROM users
WHERE username = 'manav1';
```

## Single index on `dishes(name)` {data-toc-label="On dish name"}

```sql
CREATE INDEX idx_dishname
ON dishes(name);
```

Example:

```sql
SELECT id 
FROM dishes
WHERE name = 'Palak Paneer';
```

## Composite index on `cooklogs(user_id, dish_id, created_at)` {data-toc-label="On user id, dish id, created_at"}

```sql
CREATE INDEX idx_cooklogs_user_dish_date
ON cooklogs(user_id, dish_id, created_at);
```

Example

```sql
SELECT MAX(created_at)
FROM cooklogs
WHERE user_id = 3 AND dish_id = 1;
```
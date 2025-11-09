
# Database Indices

## Single index on `users(username)`

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

## Single index on `dishes(name)`

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

## Composite index on `cooklogs(user_id, dish_id, date_cooked)`

```sql
CREATE INDEX idx_cooklogs_user_dish_date
ON cooklogs(user_id, dish_id, date_cooked);
```

Example

```sql
SELECT MAX(date_cooked)
FROM cooklogs
WHERE user_id = 3 AND dish_id = 1;
```
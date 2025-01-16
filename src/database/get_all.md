# Get all

### SQL for getting all the rows from a table

```sql
SELECT * from "user"
```

A better, and more structured approach, is to specify all fields you need from a table.

```sql
SELECT user_id, first_name, last_name, telephone, password FROM "user"
```

# Type conversion from Postgres to Rust via SQLX

In order to
you need to add FromRow to the derive of the type you will be receiving.

```rust
#[derive(Clone, Debug, FromRow)]
struct User {
    user_id: Option<uuid::Uuid>,
    first_name: String,
    last_name: String,
    telephone: String,
    password: String,
}
```

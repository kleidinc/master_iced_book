# Get all

### SQL for getting all the rows from a table

```sql
SELECT * from "user"
```

A better, and more structured approach, is to specify all fields you need from a table.

```sql
SELECT user_id, first_name, last_name, telephone, password FROM "user"
```

### Type conversion from Postgres to Rust via SQLX

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

### Example of a query

The `Query` type returned form `sqlx::query` will return a `Row<'conn>` from
the database.

As the `Row` retains an immutable borrow on a connection, only one `Row`
may exist at a time.

The `fetch` query finalizer returns a stream-like type that iterates through
the rows in the results set.

```rust
use futures::TryStreamExt;
// provides try_get
use sqlx::Row;

let mut rows = sqlx::query("SELECT * FROM users WHERE email = $1")
    .bind(email)
    .fetch(&pgpool);

while let Some(row) = rows.try_next().await? {
    // map the row into a user-defined domain type
    let email: &str = row.try_get("email")?;
}
```

To assist with mapping the row into a domain type, one of two idioms may be used.

```rust
let mut stream = sqlx::query("SELECT * FROM users")
    .map(|row| PgRow {
        // map the row into a user-defined type
    })
    .fetch(&pgpool);
```

```rust
#[derive(sqlx::FromRow)]
struct User { name: String, id: i64 }

let mut stream = sqlx::query_as::<_, User>("SELECT * FROM users WHERE email = $1 or name = $2")
    .bind(user_email)
    .bind(user_name)
    .fetch(&pgpool);
```

# Get more than one row

When you want to receive more than one row, you need to handle it
like a stream. It may help to review the
[Rust part on streams](rust/try_next.md), and futures.

### Working Example with `try_get` in `sqlx_example`

```rust
async fn get_all(pgpool: Arc<PgPool>) -> Result<Vec<User>, Error> {
    // this gives you the try_next used to poll the next row
    // gives None when no more rows available
    use futures::TryStreamExt;

    // The vec that will hold all users
    let mut users: Vec<User> = Vec::new();

    let incoming = query_as::<_,User>(r#"
SELECT user_id, first_name, last_name, telephone_number, email_address from "user"
        "#).fetch(&*pgpool);
    //
    while let Ok(user) = incoming.try_next().await? {
        let _ = &users.push(user.clone());
    }
//
    Ok(users)
}

```

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

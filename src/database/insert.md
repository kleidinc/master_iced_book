# Insert Example

For the insert example you can use the `query!` macro. You need to derive the
`sqlx::FromRow` trait to the structs you are using, the `User` struct in this
case derive that trait.

You can find a working example [here](https://github.com/kleidinc/sqlx_try_next_example/blob/master/src/main.rs).

```rust
async fn insert_user(pgpool: &PgPool, user: User) -> Result<uuid::Uuid, anyhow::Error> {
    let rec = sqlx::query!(
        r#"
INSERT INTO "user" (first_name,last_name,telephone_number,email_address)
VALUES ($1,$2,$3,$4)
RETURNING user_id;
    "#,
        user.first_name,
        user.last_name,
        user.telephone_number,
        user.email_address,
    )
    .fetch_one(pgpool)
    .await?;
    Ok(rec.user_id)
}
```

### The `query!` macro

Statically check SQL query with `println!()` style syntax.

This expands to an instance of query::Map that outputs an ad-hoc anonymous struct type, if the query
has at least one output column that is not `Void` or `()` (unit) otherwise:

```rust
//let mut conn = <impl sqlx::Executor>;
let account = sqlx::query!("select (1) as id, 'Kutuzov' as name")
    .fetch_one(&mut conn)
    .await?;
// anonymous struct has `#[derive(Debug)]` for convenience
println!("{account:?}");
println!("{}:{}", account.id, account.name);
```

_The output columns will be mapped to their corresponding Rust types._ Check the `sqlx::postgres::types` for
more information.

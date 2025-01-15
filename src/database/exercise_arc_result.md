# Exercise Result

## Result

```rust
fm main() {
    // Set up the PgPool
}

async fn check_connection_to_db(pgpool: Arc<PgPool>) -> Result<(),Error> {
    //
}
```

The full example can be found on [iced_form_experiment]().

## Explanation

1. In the first iteration of our application we will have at least 3 async functions which connect to the database through a shared pool:

   - Registration of a new user (INSERT)
   - Authentication (SELECT-operation) to check if the telephone and password correspond
   - Updating a user's data

2. Iced State derives the Clone trait and that means that most state is, or at least can be, cloned as well. Since sqlx::postgres::PgPool doesn't
   have the Copy trait, you also need to clone it.

3. The PgPool will not mutate itself.

Because we don't need to mutate the pgpool, we just need a smartpointer that allows multiple access and is threadsafe.

# Arc<T>

# Handling Errors in Iced and SQLX

When building production-ready applications you should think carefully about
your strategy in handling errors. While learning you may have discarded errors
by using `unwrap()` everywhere.

When your application will be used by other people, you should focus on handling
errors, in a way that users will not face `panic()` or unexpected crashes.

## Patterns to Handle Errors

### .map_err(/\* .. closure \_/)

With `map_err()` you can get the error, if there is an error, and handle the error
in a closure. If there is no error, the `Ok(value)` is returned.

An example of this pattern can be found in the SQLX Iced Example in the
[`async fn get_all_users`](https://github.com/kleidinc/sqlx_example/blob/master/src/main.rs) function.

```rust
// ...
while let Ok(user_incoming) = incoming
    .try_next()
    .await
    .map_err(|_e| Err::<User, LocalError>(LocalError::CannotGetAllUsers))
{
    // handle the user_incoming
}
// ...
```

### Handle it with a match

The shorter way to handle `Result<T,E>` types is with a `match`.

```rust
// ...
loop {
    match incoming.try_next().await {
        Ok(user) => /* ... */,
        Ok(None) => break,
        Err(e) => { handle_error(e): break; },
    }
// ..
```

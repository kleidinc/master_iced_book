# Exercise: Show the contents of a Vec

You will often want to show the contents of Vec<T> in your Iced application.

How would you go about showing a Vec<User> in Iced?

```rust
#[debug(Debug, Clone)]
struct User {
    first_name: String,
    last_name: String,
}

#[derive(Debug, Clone)]
struct AppName {
    list_users: Option<Vec<User>>,
}
```

You probably would want to iterate over the `&self.list_users`? Try to show the
contents of a list_users with a few names inside an Iced application.

This is more complicated than you might think.

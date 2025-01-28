# anyhow::Error

Handling errors idiomatically, is essential when building Iced or any other Rust application.

Although using `anyhow::Result` is a great way to start, you will fairly quickly hit a bottleneck.
You will notice that `anyhow::Result` doesn't implement the `Clone` and `Copy` traits,
needed by the Iced `Message` Enum.

### Thoughts: Create an enum Error

You know that by using an `Enum` you can combine different types into one Enum. So you can
combine many different Error types.

```rust
#[derive(Debug)]
enum Error {
    IcedError(iced::Error),
    DbError(sqlx::Error),
    OtherError(std::io::Error),
}
```

The only way you can activate the needed traits for the errors, is by boxing them in an
`Arc<dyn Error + Send + Sync>` or `Rc<dyn Error>`. If you want to use `anyhow` features,
you can use `Arc<anyhow::Error>`.

## Handling Errors : Pattern #1

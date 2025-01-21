# Acr Smartpointer

## Usecase in Iced

When you want to share a `sqlx::postgres::PgPool` in your iced application, you will
need to use an Arc smartpointer.

## What is the definition of an Arc smartpointer?

## What is the Usage Pattern of an Arc Smartpointer?

1. Create the Arc with `Arc::new<T>`
2. Clone the Arc with `Arc::clone(Arc<T>)`

## What is the Usage Pattern of an `Option<Arc<T>>` ?

1. Before you can clone the Arc, you need to convert the Option<T> to an Option<&T>.
   You first use the `as_ref()` which converts the Option<T> to Option<&T> and then you
   use `unwrap()` to get the `&T`.

```rust
//
```

2. Then you can create a clone with Arc::clone

```rust
//
```

3. To get the value behind the `Arc<T>` use `*` for dereferencing.

```rust
//

```

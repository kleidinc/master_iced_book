# Solution

### What do we need to achieve?

We want to compose a column, with rows for each separate item in the Vec<T>.
Each row is composed of text widgets for each item element.

### Thought Process Pseudo-code

1. Create a mutable column.
2. Iterate over the Vec<T>.
3. For each item compose the row using the row and text widgets.
4. Push each row to the column.

### Which widgets do you need?

- column
- row
- text

The column widget has a `.push` method, that pushes elements to the column.
This method can be used in our solution.

### Solution #1

```rust
let mut list = column![];
let construct_row = |item| {
    row![text(item.first_name), text(item.last_name)]
}
for item in &self.user_list.iter() {
    let new_row = costruct_row(item);
    list.push(new_row);
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

[Arc](https://doc.rust-lang.org/std/sync/struct.Arc.html#) is a thread-safe referenced-counting pointer.

- Arc allows you to create thread-safe referenced-counted clones inside an async runtime.
- Which can be dereferenced with \*.

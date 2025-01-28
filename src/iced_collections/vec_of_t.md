# Showing a Vec

### 1. First check is there is actually a Some(T) or a None

If None you can just show nothing or a place-holder.

### 2. Now iterate over Vec<T> and ...

What you need to do for each item in the Vec<T>, is to create an Element,
which you can collate, in the end, into a column of elements, where each
element represents each item.

You can't change the data in the Vec<T> in place, because that could change
the types, so you have to either create a new vector of elements, or push it
out immediately?

### Pattern to Convert a Vec<T> to Vec<Element>

```rust
    let mut all_users_element = Vec::new();

    all_users.iter().for_each(|user| {
        // construct a row from the elements
        let user_row: Element<Message> = row![]
            .push(text(user.user_id.to_string()))
            .push(text(user.first_name.clone()))
            .push(text(user.email_address.clone()))
            .push(text(user.telephone_number.clone()))
            .into();
        all_users_element.push(user_row);
        // push the row into a new vector of elements
    });
```

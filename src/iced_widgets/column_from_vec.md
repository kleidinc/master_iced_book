# Column::from_vec

One of the most useful methods when you want to show the contents
of vectors in Iced is `Column::from_vec`.

It takes a `Vec<Element>`, which can be any Iced widget, and the
contents are shown inside the Iced app.

### Pattern to display the Vec<Element> with Column::from_vec

Let's construct a vector of mock elements, which are then fed into
the Column::from_vec method.

```rust
use anyhow::Result;
use iced::widget::{row, text};
fn mock_vec_of_elements() -> Result<Vec<Element<Message>>> {
    let vec_of_elements = vec![
        row![text("first row #1"),text("first row #2"), text("first row #3")].into(),
        row![text("second row #2"), text("second row #2"), text("second row #3")].into(),
    ];
    Ok(vec_of_elements)
}
```

You will notice I am always finishing each row with the `.into()` method. That is essential
because although a widget is a special type of Element, we always have to convert it to an
Element with into.

Then we can display the rows in the `fn view` method.

```rust
use iced::widget::Column;
// ..
    fn view(&self) -> Element<Message> {
        let users_column = Column::from(mock_vec_of_elements());
        users_column.into()
}
```

### Pattern to construct a Vec<Element> from a Vec<T>

Now let's see how to convert a `Vec<T>` into a `Vec<Element>` so we can use the
Column::from_vec.

In our example project we have a `User` type, and we have a `all_users` in the state
which is a `Vec<User>`. What we want to do is to display all users in a column.

```rust
#[derive(Debug,Clone)]
struct User {
    user_id: uuid::Uuid,
    first_name: String,
    last_name: String,
    telephone_number: String,
    email_address: String,
}

#[derive(Debug, Clone)]
struct ExampleApp {
    // ..
    all_users: Option<Vec<User>>,
    // ..
}
```

Let's write a helper function that can convert a Vec<User> into a Vec<Element> so we can
feed it in the Column::from_vec, and display the users.

```rust
fn convert_to_vec_element<'a>(incoming: &'a Vec<User>) -> Result<Vec<Element<&'a,Message>>> {
    //

}
```

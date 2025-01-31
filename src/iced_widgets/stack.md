# stack!

Once you need to show windows, forms or modals on top of your parent
screen, you will need to use the [`stack!` macro](https://docs.iced.rs/iced/widget/macro.stack.html).

As, the name implies, stack, stacks children over an underlying parent.

**Note: Throughout the book I use screen, modal as synonyms. Iced lingo
uses modal.**

### Pattern to show a Child Screen over a Parent Screen

1. Define the parent screen `Element<Message>` in `fn view`
2. Define one or more child screens `Element<Message>` in `fn view`
3. Create a function that takes the parent and a child screen `fn show_child`
   and return use a `stack` component to return a new `Element<Message>`
4. Add a field `show_child_screen`, a `bool`, in the application state.
5. Based on some logic trigger the `fn show_child` in the `fn view`.
6. Create some messages to handle closing the child, and handling its
   input.

### Example `fn show_child`

```rust

```

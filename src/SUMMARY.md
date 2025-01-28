- [Why This Book?](intro/README.md)
  - [How to learn the right way?](intro/how_to_learn.md)
  - [Why Rust](intro/why_rust.md)
  - [Why Iced](intro/why_iced.md)
  - [Why SQLX with Postgres](intro/why_sqlx_postgres.md)
  - [Setting up Development Environment](intro/ide_setup_nvim.md)
  - [Trademarks & Licenses](intro/trademarks.md)

# An Introduction to Iced

- [Anatomy of an Iced App](iced/README.md)
  - [Pattern to build an Iced App](iced/pattern_to_build_an_iced_app.md)
  - [The State](iced/the_state.md)
  - [The Message](iced/the_message.md)
  - [The Logic or Message Handling](iced/the_logic.md)
  - [The View](iced/the_view.md)
  - [The Theme](iced/the_theme.md)
  - [The Subscription](iced/the_subscription.md)
  - [The Iced App](iced/the_iced_app.md)

# Essential Iced UI-Components

- [Essential Iced Building Blocks](iced_widgets/README.md)
  - [text](iced_widgets/text.md)
  - [text_input](iced_widgets/text_input.md)
  - [button](iced_widgets/button.md)
  - [container](iced_widgets/container.md)
  - [center](iced_widgets/center.md)
  - [stack](iced_widgets/stack.md)
  - [horizontal_space](iced_widgets/horizontal_space.md)
  - [Column::from_vec](iced_widgets/column_from_vec.md)

# Intro to SQL

- [SQL](sql/README.md)
  - [CREATE TABLE](sql/create_table.md)
  - [INSERT INTO](sql/insert_into.md)
  - [SELECT FROM](sql/select_from.md)
  - [UPDATE](sql/update.md)
  - [DELETE](sql/delete.md)

# Connecting to a Database through SQLX

- [Adding a Database to your App](database/README.md)
  - [Exercise: Share a PgPool connection pool in Iced](database/exercise_arc.md)
  - [Solution](database/exercise_arc_solution.md)
  - [Postgres Pattern](database/postgres.md)
  - [SQLX Pattern](database/sqlx.md)
  - [Setting up a connection in the Iced App](database/setting_up_dbconnection.md)
  - [Linking Postgres Types with Rust Types](database/types.md)
  - [Insert Example](database/insert.md)
  - [Update Example](database/update.md)
  - [Get one Item](database/get_one.md)
  - [Get many](database/get_all.md)

# Iced Advanced : Working with Collections

- [Pattern to work with Collections](iced_collections/README.md)
- [Exercise: Show the contents of a Vec<T>](iced_collections/exercise_vec_of_t.md)
- [Solution:Showing a Vec<T>](iced_collections/vec_of_t.md)

# Iced Advanced: Subscriptions

- [What are Subscriptions](subscriptions/README.md)
  - [Tab and Shift Tab to Navigate text_input's](subscriptions/tab.md)
  - [Control + s to Save](subscriptions/control_s.md)
  - [Escape to close screen](subscriptions/escape_key.md)

# Rust Refresh

- [Rust](rust/README.md)
  - [anyhow::Error](rust/anyhow.md)
  - [Iterators](rust/iterators.md)
  - [Iterator Adapters](rust/iterator_adapters.md)
  - [How to run Rust with Back-trace](rust/run_rust.md)
  - [Lifetimes in Iced](rust/lifetimes_in_iced.md)
  - [Result](rust/result.md)
  - [Option](rust/option.md)
  - [Handling Errors in Iced](rust/handling_errors_in_iced.md)
  - [Clone Trait](rust/clone_trait.md)
  - [Into Trait](rust/into_trait.md)
  - [Arc Smart pointer](rust/arc_smartpointer.md)
  - [Trait Stream try_next](rust/try_next.md)

# Contribute

- [How to contribute to this book?](thanks/README.md)

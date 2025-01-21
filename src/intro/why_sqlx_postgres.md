# Why SQLX with Postgres

When working with databases in Rust, you always need to handle the differences in data types,
between the database and Rust.

Postgres has different internal types, than Rust. So you always need to convert types,
from Postgres to Rust, and from Rust to Postgres.

SQLX has a conversion process with the `FromRow` trait, and also has `sqlx::postgres::types`,
which make the conversion easy and straightforward.

I would advise you to also read the official docs, review the examples.

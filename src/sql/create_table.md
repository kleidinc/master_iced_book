# CREATE TABLE

## Example of a CREATE TABLE

```sql
CREATE TABLE IF NOT EXISTS "user" (
    user_id PRIMARY KEY DEFAULT gen_random_uuid(),
    first_name varchar(25) NOT NULL,
    middle_name varchar(25),
    last_name varchar(25),
    telephone varchar(15) NOT NULL UNIQUE
);
```

## Postgres Types

When you use Postgres with Rust, you always need to consider how the Postgres types will
be converted to Rust types, and back. One of the reasons why I choose SQLX is because it
has a sqlx::<traits> that automatically converts types back and forth.

The most common types:

- varchar(<number of max characters>)
- uuid
- text
- numeric (for anything where it is important to be precise, for prices or money)

But there are many others. I would suggest to just read the official Postgres documentation.
It is by far the most complete and most importantly the most accurate and up to date.

## Automatic Generation of uuid's

In the example above you will have noticed `gen_random_uuid()`. When inserting a row, if you don't
provide a uuid, it will be automatically generated.

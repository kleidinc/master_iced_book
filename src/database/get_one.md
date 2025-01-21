# Get one Item by Id Example

When using sqlx refrain from using anonymous sqlx queries, as they won't convert, and check
the incoming types of your data.

By using the query_as, you can automatically convert the received data from the database,
from Postgres to Rust types. To allow this conversion back and forth, you need to
add `#[derive(FromRow)]` to your Rust data structure, and use the correct
corresponding `sqlx::postgres::types`.

### Example using `query_as`

```rust
pub async fn get_macro_food_by_id(macro_id: uuid::Uuid) -> Result<MacroFood, anyhow::Error> {
    let pool = helper::connect_to_db().await;
    let result: MacroFood = sqlx::query_as(
        r#"
SELECT macro_id, name, carbohydrates, protein, fat, kcalories, weight from "macro_foor"
WHERE macro_id = $1;
        "#
     )
     .bind(macro_id)
     .fetch_one(&pool)
     .await?;
     Ok(result)
 }
```

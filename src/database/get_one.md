# Get one Item by Id Example

### Example using `query_as`

```rust
pub async fn get_macro_food_by_id(macro_id: uuid::Uuid) -> Result<MacroFood, anyhow::Error> {
    let pool = helper::connect_to_db().await;
    let result: MacroFood = sqlx::query_as(
        r#"
SELECT macro_id, name, carbohydrates, protein, fat, kcalories, weight from "macro_foor" WHERE macro_id = $1;
        "#
     )
     .bind(macro_id)
     .fetch_one(&pool)
     .await?;
     Ok(result)
 }
```

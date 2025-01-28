# INSERT INTO

### Insert a record

```sql
INSERT INTO
```

### INSERT ON CONFLICT UPDATE

In many cases, the telephone number, is set to UNIQUE in the CREATE TABLE.
If you then want to insert a new record for a user with the same telephone
number, you need to handle the conflict.

The update on conflict should not be the default, or you may end up updating
user data, for a different user. But if the user is authenticated, then you
can use the update on conflict.

```sql
INSERT INTO
ON CONFLICT UPDATE
```

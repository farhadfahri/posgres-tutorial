## Constraints


### CREATE CHECK

```sql 
    CREATE TABLE staff (
        staff_id SERIAL PRIMARY KEY, 
        first_name VARCHAR(50), 
        last_name VARCHAR(50), 
        birth_date DATE CHECK (birth_date>'1990-01-01'), 
        joined_date DATE CHECK (joined_data>birth_date), 
        salary NUMERIC CHECK (salary > 0)
    ); 


```

### ADD, MODIFY, DROP CHECK

```sql 
    CREATE TABLE staff (
        price_id SERIAL PRIMARY KEY, 
        product_id INT NOT NULL, 
        price NUMERIC NOT NULL, 
        discount NUMERIC NOT NULL, 
        valid_from DATE NOT NULL
    ); 

    ALTER TABLE staff 
    ADD CONSTRAINT price_check
    CHECK (
        price > 0
        AND discount >= 0
        AND price > discount
    )
```
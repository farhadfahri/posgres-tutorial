## User Defined Datatypes 


### CREATE A DOMAIN

```sql
CREATE DOMAIN address_uk_standard VARCHAR(100) NOT NULL;

CREATE TABLE locations (
    address address_uk_standard
);

INSERT INTO locations (address) VALUES ('Baker street 12');

```


### CREATE A DOMAIN POSITIVE NUMERIC
```sql 
    CREATE DOMAIN positive_numeric INT NOT NULL CHECK (VALUE>0); 

    ALTER TABLE locations
    ADD COLUMN id SERIAL PRIMARY_KEY, 
    ADD COLUMN apartment positive_numeric
```


### CREATE A DOMAIN POSTAL CODE
```sql
CREATE domain us_postal_code as TEXT
CHECK (
	VALUE ~'^\d{5}$'
	OR VALUE ~'^\D{5}$-^\d{4}$'
);

ALTER TABLE locations
ADD column postal_code us_postal_code;
```


### CREATE A DOMAIN ENUM

```sql
    CREATE DOMAIN valid_colors VARCHAR(10)
    CHECK (VALUE IN ('RED', 'GREEN', 'BLUE'))
```

### DROP DOMAIN NAME

- will through error if any object depends on it.

```sql 
    DROP DOMAIN positive_numeric
```


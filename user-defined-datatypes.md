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

- will delete the column it depends on, extra careful

```sql
    DROP DOMAIN positive_numeric CASCADE
```

- save way to delete domain name

```sql 
    ALTER TABLE locations
    ALTER COLUMN apartment TYPE INT

    DROP DOMAIN positive_numeric;
``` 

### CREATE A TYPE

```sql
    CREATE TYPE address_format AS (
        city VARCHAR(50), 
        country VARCHAR(20)
    );

    CREATE TABLE companies (
        comp_id SERIAL PRImARY KEY, 
        address address_format
    );

    INSERT INTO companies VALUES
    (ROW('LONDON', 'UK')),
    (ROW('NEw YORK', 'US'));

    SELECT (address).country FROM companies;
```

```sql
    CREATE TYPE currency AS ENUM('USD', 'EUR', 'GBP')

    ALTER TYPE currency ADD VALUE 'CHF' AFTER 'EUR';

    CREATE TABLE stocks (
        stock_id SEERIAL PRIMARY KEY, 
        stock_currency currency
    )

    INSERT INTO stocks (stock_currency) VALUES ('USD');

    -- to drop type
    DROP TYPE currency;
```

### ALtER A TYPE

```sql 
    CREATE TYPE myaddress AS (
        city VARCHAR(50), 
        country VARCHAR(20)
    );

    ALTER TYPE myaddress RENAME TO corporate_address;

    -- change owner

    ALTER TYPE corporate_address OWNER TO adam;

    -- change schema

    ALTER TYPE corporate_address SET SCHEMA pl;

    -- add new attribute

    ALTER TYPE pl.corporate_address ADD ATTRIBUTE street_address VARCHAR(150);
```

### ALTER ENUM TYPES

```sql
    CREATE TYPE colors AS ENUM ('GREEN', 'RED', 'BLUE');

    ALTER TYPE colors RENAME 'RED' TO 'ORANGE';

    -- select all enum values 

    SELECT enum_range(NULL::colors);

    ALTER TYPE colors ADD VALUE 'PURPLE' AFTER 'RED';
```
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



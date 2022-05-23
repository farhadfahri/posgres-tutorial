## Sequence


### CREATE A SEQUENCE

```sql
    CREATE SEQUENCE IF NOT EXISTS test_seq;

-- what sequence hold, it will increment 1 by default 

    SELECT nextval('test-seq'); 

-- select current value of sequence

    SELECT currval('test-seq');

-- set sequence, it will start incrementing with 100, ex. 101

    SELECT setval('test-seq', 100);

-- set a sequence and do not skip

    SELECT setval('test-seq', 200, false);

-- constrole the sequence START value

    CREATE SEQUENCE IF NOT EXISTS test_sequence START WITH 100;

```

### RENAME, ALTER SEQUENCE

```sql
    SELECT nextval('test-seq')
    -- => 206

    -- restart the sequence

    ALTER SEQUENCE test_seq RESTART WITH 100; 
    SELECT nextval('test_seq');

    -- => 100

    ALTER SEQUENCE test_seq RENAME TO my_sequence;
```

### START WITH, MAX, MIN VALUES, DROP SEQUENCES
```sql
    CREATE SEQUENCE IF NOT EXISTS increment_value
    INCREMENT 50
    MINVALUE 400
    MAXVALUE 6000
    START WITH 500

    SELECT nextval('increment_value');

    -- => 500, 550, 600

    -- specify data types of sequence

    CREATE SEQUENCE IF NOT EXISTS test_seq_smallint AS SMALLINT;

    -- create a descending sequence and cycle, by default it will create in ascending order

    CREATE SEQUENCE seq_des
    INCREMENT -1
    MINVALUE 1
    MAXVALUE 3
    START 3
    CYCLE;

    -- drop sequence

    DROP SEQUENCE seq_des;
```

### ATTACH SEQUENCE

```sql
    -- serial datatype create default sequence

    CREATE TABLE users (
        user_id SERIAL PRIMARY KEY, 
        user_name VARCHAR(50)
    )
    -- default dequence table_columnname_seq
    ALTER SEQUENCE users_user_id_seq RESTART WITH 100; 


    -- create table and attach sequence

    CREATE TABLE melons (
        user_number INT PRIMARY KEY, 
        user_location VARCHAR(50)
    )

    CREATE SEQUENCE IF NOT EXIST personal_number
    START WITH 100 OWNED BY melons.user_number;

    ALTER TABLE melons 
    ALTER COLUMN user_number SET DEFAULT nextval('personal_number');

    -- single sequence shared by both tables

    CREATE SEQUENCE common_sequence START WITH 100;

    CREATE TABLE phones (
        apple_id INT DEFAULT nextval('common_sequence') NOT NULL, 
        apple_name VARCHAR(50)
    )

     CREATE TABLE laptops (
        apple_serial_number INT DEFAULT nextval('common_sequence') NOT NULL, 
        apple_name VARCHAR(50)
    )

```

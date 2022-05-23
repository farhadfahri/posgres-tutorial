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
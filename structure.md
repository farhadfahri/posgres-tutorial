## Database 

### Datatypes

#### BASIC SETUP

```sql
CREATE TABLE persons(
    person_id SERIAL PRIMARY KEY, 
    first_name VARCHAR(20) NOT NULL, 
    last_name VARCHAR(20) NOT NULL
); 
```

#### ADD COLUMN CONSTRAINTS

```sql
ALTER persons
ADD COLUMN age NOT NULL;

ALTER TABLE persons
ADD COLUMN nationality VARCHAR(20)
ADD COLUMN email VARCHAR(100) UNIQUE;
```

#### RENAME TABLE

```sql
ALTER TABLE persons 
RENAME TO users;
```

#### DROP, CHANGE DATA TYPE, SET DEFAULT

```sql
ALTER TABLE users
RENAME COLUMN age TO person_age; 

ALTER TABLE users
DROP COLUMN person_age;

ALTER TABLE users
ADD COLUMN age VARCHAR(10);


ALTER TABLE users
ALTER COLUMN age TYPE INT












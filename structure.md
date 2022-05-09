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
USING age::integer;

```


#### CONSTRAINTS
 
 ```sql
 CREATE TABLE web_links (
     link_id SERIAL PRIMARY KEY, 
     link_url VARCHAR(255) NOT NULL, 
     link_target VARCHAR(20)
 );

 INSERT INTO web_links(link_url, link_target)
 VALUES ('http://google.com', '_blank');


-- add constraint

 ALTER TABLE web_links
 ADD CONTRAINT unique_web_url UNIQUE (link_url);

 -- to set a column to accept only defined allowed values

 ALTER TABLE web_links
 ADD COLUMN is_enable VARCHAR(2);


 ALTER TABLE web_links
 ADD CHECK (is_enable IN ('Y', 'N'));

```


#### TYPE CONVERSION

CAST (expression AS target_data_type)

```sql
SELECT CAST('10' AS INTEGER) --  => 10
SELECT CAST('10n' AS INTEGER) -- => error

SELECT CAST('2021-12-21' AS DATE) -- => 2021-12-21
SELECT CAST('01-MAY-2020' AS DATE) -- => 2020-06-01

SELECT CAST('true' AS BOOLEAN) -- => true
SELECT CAST('false' AS BOOLEAN)-- => false
SELECT CAST('T' AS BOOLEAN) -- => true 
SELECT CAST('F' AS BOOLEAN)-- => false
SELECT CAST('1' AS BOOLEAN) -- => true
SELECT CAST('0' AS BOOLEAN) -- => false

SELECT CAST ('14,7888' AS DOUBLE PRECISION) -- => 14.7888

```

expression::type

```sql
SELECT 
'10'::INTEGER,
'2020-12-12'::DATE
'2020-12-22 10:30:25.467'::TIMESTAMP
'2020-12-22 10:30:25.467'::TIMESTAMPTZ

-- interval
'10 minute'::interval
'4 hours'::interval
'1 day':: interval
```

#### CONVERSION FUNCTIONS

1. Postgres to_char functions allow converion of
- a timestamp
- an interval
- an integer
- a double-precision 
- numeric value

2. TO_CHAR(expression, format)
3. TO_NUM(string, format)
4. TO_DATE(text, format)
5. TO_TIMESTAMP(timestamp, format)







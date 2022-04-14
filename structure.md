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











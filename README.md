# posgres-tutorial

## Installation

```bash
docker-compose up -d
```

source: [https://www.udemy.com/course/postgresqlmasterclass/]

## Database 

### Create role with password and permission

```sql
CREATE ROLE tima WITH
	LOGIN
	NOSUPERUSER
	CREATEDB
	NOCREATEROLE
	INHERIT
	NOREPLICATION
	CONNECTION LIMIT -1
	PASSWORD 'xxxxxx';
```

### Create movies database 
```sql
CREATE DATABASE movies
    WITH 
    OWNER = postgres
    ENCODING = 'UTF8'
    CONNECTION LIMIT = -1;
```

### CREATE TABLES for movies database

```sql
CREATE TABLE actors (
	actor_id SERIAL PRIMARY KEY, 
	first_name VARCHAR(150), 
	last_name VARCHAR(150) NOT NULL, 
	gender CHAR(1),
	date_of_birth DATE,
	created_at DATE, 
	updated_at DATE
);

CREATE TABLE directors (
	director_id SERIAL PRIMARY KEY,
	first_name VARCHAR (150),
	last_name VARCHAR (150),
	date_of_birth DATE, 
	created_at DATE, 
	updated_at DATE
);

CREATE TABLE movies (
	movie_id SERIAL PRIMARY KEY, 
	movie_name VARCHAR (100) NOT NULL, 
	movie_length INT, 
	movie_lang VARCHAR (20), 
	age_certificate VARCHAR (10), 
	release_date DATE, 
	director_id INT REFERENCES directors (director_id)
);

CREATE TABLE movies_revenues (
	revenue_id SERIAL PRIMARY KEY, 
	movie_id INT REFERENCES movies(movie_id), 
	revenues_domestic NUMERIC (10, 2), 
	revenues_international NUMERIC (10,2)
);

CREATE TABLE movie_actor (
	movie_id INT REFERENCES movies (movie_id),
	actor_id INT REFERENCES actors (actor_id), 
	PRIMARY KEY (movie_id, actor_id)
	
);

CREATE TABLE customers (
	customer_id SERIAL PrIMARY KEY, 
	first_name VARCHAR(50), 
	last_name VARCHAR (50), 
	email VARCHAR (150),
	age INT
);

```

### INSERT WITH RETURNING
Once value entered it will return all the new created rows

```sql

INSERT INTO customers (first_name, last_name, email, age)
VALUES ('Leo', 'Messi', 'leo_messi@rm.com', 23) RETURNING *;

```

### UPDATE WITH RETURNING

```sql

UPDATE customers
SET 
	first_name = 'Jacopo', 
	last_name = 'Messina', 
	email = 'jacopo.messina@gmail.com'
WHERE customer_id = 1
RETURNING *;

```

### DELETE 

```sql
DELETE FROM WHERE customer_id = '1'; 
```

### UPSERT 
```sql
CREATE TABLE t_tags (
	id SERIAL PRIMARY KEY, 
	tag TEXT UNIQUE, 
	update_at TIMESTAMP DEFAULT NOW()
);

INSERT INTO t_tags (tag)
VALUES ('Pen'), ('Pencil');

-- do nothing on conflict 

INSERT INTO t_tags (tag)
VALUES ('Pencil'), ('Pennito')
ON CONFLICT (tag) 
DO NOTHING;

-- update tag on conflict

INSERT INTO t_tags (tag)
VALUES ('Pencil')
ON CONFLICT (tag) 
DO UPDATE SET 
	tag = EXCLUDED.tag
	update_at = NOW();

```

### QUERYING DATA

```sql
SELECT first_name || ' ' || last_name AS "Full name" FROM actors; 

```

### QUERYING DATA WITH ORDER BY

sorting data based on single column

```sql
SELECT * FROM actors 
ORDER BY movie_name
```

sorting data on multiple columns sort data 
based on ASC and DESC directions with combination
of columns 

```sql 
SELECT * FROM actors
ORDER BY 
	release_data DESC,  
	movie_name ASC
; 
```

sorting data by expression 
```sql
SELECT first_name, 
LENGTH(first_name) AS characters_legth
FROM actors
ORDER BY characters_legth;
```

sorting data with null values

by default null values will be at the end

```sql
SELECt * FROM actors
ORDER BY first_name;
```

results in the same result

```sql
SELECT * FROM actors
ORDER BY first_name NULLS LAST;
```

sort by descending, wii have the same result

```sql
SELECT * FROM actors
ORDER BY first_name DESC;
```

```sql
SELECT * FROM actors
ORDER BY first_name NULLS LAST;
```


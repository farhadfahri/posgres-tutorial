# posgres-tutorial

## Installation

```bash
docker-compose up -d
```

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

### CREATE TABLEs for movies database

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

```



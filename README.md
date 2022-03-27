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

### Create tables for movies database

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
```



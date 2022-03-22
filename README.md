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



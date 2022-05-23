## STRING FUNCTIONS


### UPPER


```sql 
    SELECT UPPER('amazing postgresql')

    SELECT 
        UPPER(first_name) AS first_name, 
        UPPER(last_name) AS last_name
    FROM directors;

    SELECT LOWER('Amazing Posgresql');

    -- Init

    SELECT INITCAP ('the world is changing with a lightning speed'); 

    SELECT INITCAP(
        CONCAT (first_name, ' ', last_name)
    ) AS full_name

    FROM directors
    ORDER BY first_name;

```

### LEFT, RIGHT, REVERSE
```sql 
    SELECT LEFT(first_name, 1) AS INITIAL 
    FROM directors
    ORDER BY 1; 

    SELECT movie_name 
    LEFT (movie_name, 6)
    FROM movies;

    -- same logic for RIGHT
    -- reverses the string 

    SELECT REVERSE('Amazing PostgreSQL');

```

### SPLIT PART

```sql 
-- SPLIT_PART (string, delimeter, position)

    SELECT 
        movie_name, 
        release_date, 
        SPLIT_PART(release_date::text, '-', 1) as release_year
    FROM movies;
```

### TRIM, LTRIM, RTRIM, BRIM

```sql 
    -- The TRIM() function removes the longest string that contains a specific character from a string

    TRIM([LEADING | TRAILING | BOTH] [characters] FROM string)

    SELECT 
        TRIM (
            LEADING
            FROM ' Amazing Postgresql'
        ), 
        TRIM (
            TRAILING
            FROM 'Amazing Posgresql   '
        ), 
        TRIM('  Amazing Posgresql   ')

    -- all result in => 'Amazing Posgresql'
```

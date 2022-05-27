## STRING FUNCTIONS


### UPPER


```sql 
    SELECT UPPER('amazing postgresql')

    SELECT 
        UPPER(first_name) AS first_name, 
        UPPER(last_name) AS last_name
    FROM directors;

    SELECT LOWER('Amazing Posgresql');

    -- write first letters in capital letter

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


    -- remove leading zero 

    SELECT 
        TRIM (
            LEADING '0'
            FROM 
                CAST (00012345 AS CAST)
        );
```

### TRIM, LTRIM, RTRIM, BRIM

```sql
    -- function pads a string on the left to a specified length with a sequence of characters

    LPAD(string, length[, length])

    -- the fill argument is optional. If you omit the fill argument, its default value is space

    SELECT LPAD('Database', 5, '*') -- => *****Database 
```

### SUBSTRING, REPLACE

```sql
    SELECT substring ('What a wonderful world' from 1 for 4) -- => What
    SELECT substring ('What a wonderful world' for 7) -- => What a

    SELECT  
        first_name, 
        last_name, 
        SUBSTRING(first_name, 1, 1) AS initial
    FROM 
        directors
    ORDER BY 
        last_name

```

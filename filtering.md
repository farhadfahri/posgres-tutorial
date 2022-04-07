## Database 

### Filtering data

add parenthesis and the order of AND OR does affect the
output

```sql
SELECT * FROM movies m 
WHERE  (m.movie_lang = 'English' OR m.movie_lang = 'Chinese')
AND m.age_certificate = '12'
ORDER BY m.movie_lang;
```

AND operator is processed first and OR operator processed second. 
it can be seen as AND for MULTIPLICATION and OR for ADDITION

3*2+1 = 7,   3*(2+1) = 9 similar logic



Limit and offet the result. Offset number will start taking data after. 

```sql
SELECT * FROM movies_revenues mr 
ORDER BY mr.revenues_domestic DESC NULLS LAST
LIMIT 5 offset 4
;
```

Fetch number of rows 

```sql
SELECT * FROM directors d 
ORDER BY d.date_of_birth
FETCH FIRST 5 ROWS only;
```

With combination with OFFSET in cab be used either 
before FETCH or after FETCH

```sql
SELECT * FROM movies m 
ORDER BY m.movie_length DESC 
OFFSET 5 
FETCH FIRST 5 ROWS ONLY;
```

```sql
IN 
NOT IN
BETWEEN low_value AND high_value
```


-- Operators to query data using 'pattern matching'
-- Returns true or false 
-- Both let you search for patterns in strings by using tow special characters 

-- % percent sign matches any sequence of zero or more characters 
-- Underscore sign (_) matches single character

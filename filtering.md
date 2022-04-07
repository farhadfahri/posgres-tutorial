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
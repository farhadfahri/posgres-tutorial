## Database 

### Datatypes

* BOOLEAN

Following are some valid literals for boolean values

| TRUE        | FALSE       |
| ----------- | ----------- |
| TRUE        | FALSE       |
| 'true'      | 'false'     |
| 't'         | 'f'         |
| 'y'         | 'n'         |
| 'yes'       | 'no'        |
| '1'         | '0'         |

* CHARACTERS


| CHARACTER TYPES           | NOTES                        |
| ------------------------- | ---------------------------- |
| CHARACTER(n), CHAR(n)     | fixed-length, blank padded   |
| VARCHAR(n)                | var length with length limit |
| TEXT, VARCHAR             | var unlimited length         |

* NUMERIC

- Numbers column can hold various numbers but NULL values
- Math operations can be performed on numeric columns
- Two main types of numbers are
  Integers - can hold both posivite and negative values
  Fixed-point floating numbers  - Two format of fractions of whole numbers

- Three main types of integers


| Name         | bytes       | lower range             | Upper range         |
| ------------ | ----------- | ----------------------- | ------------------- |
| smallint     | 2 bytes     | -32768                  | 32768               |
| integer      | 4 bytes     | -2147483648             | 2147483648          |
| big interger | 8 bytes     | -9223372036854775808    | 9223372036854775807 |


- Auto-increment datatype

| Name         | bytes       | lower range | Upper range         |
| ------------ | ----------- | ----------- | ------------------- |
| smallserial  | 2 bytes     | 1           | 32768               |
| serial       | 4 bytes     | 1           | 21474836487         |
| big serial   | 8 bytes     | 1           | 922337203685477507  |
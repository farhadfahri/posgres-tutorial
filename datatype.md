## Database 

### Datatypes

#### BOOLEAN

Following are some valid literals for boolean values

| TRUE        | FALSE       |
| ----------- | ----------- |
| TRUE        | FALSE       |
| 'true'      | 'false'     |
| 't'         | 'f'         |
| 'y'         | 'n'         |
| 'yes'       | 'no'        |
| '1'         | '0'         |

#### CHARACTERS


| CHARACTER TYPES           | NOTES                        |
| ------------------------- | ---------------------------- |
| CHARACTER(n), CHAR(n)     | fixed-length, blank padded   |
| VARCHAR(n)                | var length with length limit |
| TEXT, VARCHAR             | var unlimited length         |

#### NUMERIC

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


#### FIXED POINT NUMBERS DECIMAL

numeric(precision, scale)

precision scale - Maximum number of digits to the left and right of the decimal points


decimal(precision, scale)


#### FLOATING TYPES

Two types of floating. Allows digits to float

| NAME   | DESCRIPTION                                 |
| ------ | ------------------------------------------- |
| real   | allows precision point to 6 decimal digits  |
| double | allows precision point to 15 decimal digits |


#### DATE, TIME, TIMESTAMP, TIMESTAMPTZ

Data type available

| TYPE        | STORES                  | KEYWORD    | FORMATS                    |
| ----------- | ----------------------- | ---------  | -------------------------- | 
| Date        | Date only               | DATE       | YY-MM-DD                   |
| Time        | Time only               | TIME       | HH:MM:SS                   |
| Timestamp   | Date, time              | DATETIME   | YY-MM-DD HH:MM:SS          |
| Timestamptz | Date, time, timezone    | DATETIMETZ | YY-MM-DD HH:MM:SS TZ       |

Internally when we saving with TZ (UTC format) is saved, however when we are
retrieving it will be converted to TZ which is installed internally


#### ARRAYS

- Every data type has its own companion array type.

Integer has an integer[] array type and so on.

```sql
CREATE TABLE table_array(
    id SERIAL,
    name VARCHAR(100),
    phone text []
)

INSERt INTO table_array 
VALUES ('Adam', ARRAY
        [('542-101-3992'), ('543-122-2331')]
    );

SELECT name FROM table_array
WHERE phone[0] = '542-101-3993';
```

#### HSTORE

- hstore is data type that store data into key-value pair. 
- the hstore module implements the hstore data type.
- the keys and values are just strings only.

```sql

CREATE EXTENSION IF NOT EXISTS hstore; 

CREATE TABLE table_hstore (
    book_id SERIAL PRIMARY KEY, 
    title VARCHAR(100) NOT NULL,
    book_info hstore
); 

INSERT INTO table_hstore(title, book_info) 
VALUES (
    'Ricar Pustini', 
    '
        "publisher" => "New Dawn", 
        "paper_cost" => "10.00", 
        "e_cost" => "5.85"
    '
);

SELECT book_info -> 'publisher' FROM table_hstore;
```


#### JSON
- The JSON datatype is actually text under the hood, with a verification that format is valid json.
- The JSONB implements binary version of JSON datatype.
- The JSON datatype, being a text datatype, store the data presentation exactly as it is sent to POSTGRESQL
including whitespace and indentification and also multiple-keys when present 
- The JSONB is advance binary storage format with full processing, indexing and searching capabilites. 

```sql
CREATE TABLE json_table (
    id SERIAL PRIMARY KEY, 
    docs JSON
);

INSERT INTO json_table (docs) VALUES
('[1,2,3,4,5,6]'),
('[1,2,3,4,5,6]'),
('{"key": "value"}')

-- it won't work since we have to convert to JSONB
SELECT * FROM table_json
WHERE docs @> '2'; 


ALTER TABLE table_json
ALTER COLUMN docs TYPE JSONB

-- adding index

CREATE INDEX ON table_json USING GIN (docs->'Publisher' jsonb_path_ops);

```

#### NETWORK ADDRESSES

1. Postgresql offers data types to store IPv4, IPv6, and MAC addresses. 
2. Network address types: 

| Name     | Storage size  | Notes                              |
| -------- | ------------- | ---------------------------------- |
| cidr     | 7 or 19 bytes | IPv4 and IPv6 networks             |
| inet     | 7 or 19 bytes | IPv4 and IPv6 hosts and networks   |
| macaddr  | 8 bytes       | MAC addresses                      |
| macaddr8 | 8 bytes       | MAC addresses                      |

it is better to use these types instead of text to store network addresses
because these types offer input error checking and speciliazed operators and 
functions. 


3. Special soring mechanism

When sorting inet or cidr data types, IPv4 addresses will always sort before IPv6 addresses,
including IPv4 addresses encapsulated or mapped to IPv6 addresses. 

4. Index types are bundle with indexing support and advanced functions and operator support.


```sql
CREATE TABLE table_netaddr (
    id SERIAL PRIMARY KEY, 
    ip INET
)

INSERT INTO table_netaddr (ip) VALUES
('4.35.221.243'),
('4.152.207.128'),
('4.152.207.238'),
('12.1.223.132'),
('12.8.192.60'),

SELECT 
    ip, 
    set_masklen(ip, 24) as inet_24, 
    set_masklen(ip::cidr, 24) as cidr_24, 
    set_masklen(ip::cidr, 27) as cidr_27, 
    set_masklen(ip::cidr, 28) as cidr_28

FROM table_netaddr;

```








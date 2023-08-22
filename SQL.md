Structures Query Language is used to manipulate Relational Databases (RDBMS).
Two type of commands:
- Data Definition Language
- Data Manipulation Language

### Commonly used Datatypes in SQL:

- CHAR
- VARCHAR
- BINARY
- TEXT
- BLOB
- ENUM
- SET
- BOOL
- INT
- FLOAT
- DOUBLE
- DECIMAL
- DATE
- DATETIME
- TIMESTAMP
- TIME

### Column constraints:
- NOT NULL
- UNIQUE
- PRIMARY KEY
- FOREIGN KEY
- CHECK
- DEFAULT
- CREATE INDEX

### Usecase:

1) Creating a table:
```SQL
CREATE TABLE IF NOT EXISTS <tablename> (index INT PRIMARY KEY,
										name VARCHAR(60));
```

2) Selecting data:
```SQL
SELECT * FROM TABLE <tablename>
```
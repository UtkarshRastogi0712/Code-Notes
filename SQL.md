#SQL
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

#### Creating a table:
```SQL
CREATE TABLE IF NOT EXISTS <tablename> (index INT PRIMARY KEY,
										name VARCHAR(60));
```

#### Selecting data:
```SQL
SELECT * FROM <tablename>;
```

#### Column Alias:
```SQL
SELECT name AS alias FROM <tablename>;
```

#### Join:
```SQL
SELECT one.col, two.col FROM one <modifier> JOIN two ON one.col = two.col;
```
> Modifier list:
> - INNER
> - FULL
> - LEFT
> - RIGHT
> - CROSS
> - NATURAL

#### Order by:
```SQL
SELECT * FROM <tablename> ORDER BY <column> [DESC];
```

#### Filter:
```SQL
SELECT * FROM <tablename> where <column> IS NOT NULL;
```
> Other filter:
> - BETWEEN <> AND <>;
> - LIKE "%str_";
> - IN (<>,<>,<>,...);
> - all logical relational operators;

#### Aggregate:
```SQL
--Type one
SELECT COUNT(<column name>) FROM <tablename>;
--Type Two
SELECT COUNT(DISTINCT <column name>) FROM <tablename> GROUP BY <column name> HAVING <expression>;
```
> Aggregate operations:
> - AVG
> - COUNT
> - MAX
> - MIN
> - SUM

#### Nested Queries:
```SQL
SELECT COUNT(*) FROM <tablename> WHERE <variable> IN (
	SELECT AVG(<column name>) FROM <tablename> GROUP BY <column name>
);
```
> Nested return type:
> - =
> - IN
> - EXISTS
> - relational operations
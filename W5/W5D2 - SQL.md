### Learning Goals 
- Understand why we need databases
- Know what a "Relational DataBase Management System" is
- Be able to access data in a database and perform basic operations on the data

## #Databases
- There are diffenrent models of databases
	- They differ in how they store data and how that data can therefore be accessed 
- We're going to use a relational database model. 'Relational' refers to the use of tables to store and organize data
	- Each table is referred to as a "relation", as it is a collection of *related* data entries
- We can imagine a relational database as an excel spreadsheet with a collection of related tables
	- [Sample Dataase](https://docs.google.com/spreadsheets/d/11Gwdlqhln0PIX2KDXnr2UozAnRog2GverwyjPIXHN2o/edit#gid=0)
		- Foreign Key - references a *primary* key and is *commonly* named n_id
		- Primary Key - the main ID of the table
		- Each Primary key can only belong to one owner
		- Joins table - Specifically for correlating between two tables

#### For our purposes, there are two parts to storing and accessing data

1. DataBase Management System
    - An application that stores data at scale and can be queried for data

2. The Querying Language
    - The language we use to interact with the database management system to create our database, insert data, and query (i.e. ask) it for data

### "Relational DataBase Management System" (RDBMS)

- An application that stores data at scale and organizes the data in _tables_

We will be using:

- PostgreSQL, aka Postgres (open source)
    - We'll be using this for the next two days, and for most projects
- SQLite (open source)
    - Thursday's project uses this

## #SQL
- The way we communicate with our database
- SQL stands for "Structured Query Language"
    - previously spelled SEQUEL, which stood for "Structured English Query Language"
- It's a domain-specific language (**DSL**) for _relational_ databases (other DSLs you've encountered: HTML, RSpec)

### What can SQL do?
- SQL can create new databases
- SQL can create new tables in a database
- SQL can insert records in a database
- SQL can update records in a database
- SQL can delete records from a database
- SQL can retrieve data from a database

### Column Types

Every column must have a data type specified. Some common types
- `varchar`
- `boolean`
- `integer`
- `float
- `date
- many, many more

### PostgreSQL Shell Commands

- `$ psql`
- `CREATE DATABASE lecture;`
- `$ psql lecture`
- `\d` - list tables
- `\d table` - show schema for table
- `\?` to list meta commands
- end queries with a `;`

#### lecture_demo.sql
```sql
DROP TABLE IF EXISTS sf_instructors;

CREATE TABLE sf_instructors (
  id INTEGER PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  pod_leader_id INTEGER
);

\echo "Created SF Instructors Table"

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (1, 'Darren', NULL);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (2, 'Jen', NULL);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (3, 'Mike', NULL);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (4, 'Ryan', NULL);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (5, 'Carlos', 4);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (6, 'Walker', 3);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (7, 'Michelle', 3);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (8, 'Vanessa', 3);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (9, 'Joe', 3);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (10, 'Lina', 4);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (11, 'Erik', 4);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (12, 'Julia', 4);

INSERT INTO
  sf_instructors (id, name, pod_leader_id)
VALUES
  (13, 'Zack', 4);


DROP TABLE IF EXISTS ny_instructors;
CREATE TABLE ny_instructors (
  id INTEGER PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  pod_leader_id INTEGER
);

\echo "Created NY Instructors Table"

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (1, 'Darren', NULL);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (2, 'David', NULL);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (3, 'Josh', NULL);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (4, 'Andy', NULL);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (5, 'Rosemary', 2);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (6, 'Paloma', 2);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (7, 'Richard', 2);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (8, 'Valerie', 3);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (9, 'Ara', 3);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (10, 'Taihyung', 4);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (11, 'Megan', 4);

INSERT INTO
  ny_instructors (id, name, pod_leader_id)
VALUES
  (12, 'Daniel', 4);


-- Many-Many relationship between app_academy and hack_reactor

DROP TABLE IF EXISTS friendships;
CREATE TABLE friendships (
  id INTEGER PRIMARY KEY,
  sf_id INTEGER NOT NULL,
  ny_id INTEGER NOT NULL
);

\echo "Created Friendships Table"

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (1, 1, 4);

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (2, 1, 2);

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (3, 1, 3);

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (4, 1, 1);

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (5, 6, 1);

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (6, 3, 2);

INSERT INTO
  friendships (id, sf_id, ny_id)
VALUES
  (7, 2, 2);

-- One-to-Many relationship between app_academy people and possessions

DROP TABLE IF EXISTS possessions;
CREATE TABLE possessions (
  id INTEGER PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  type VARCHAR(255),
  cost INTEGER,
  owner_id INTEGER
);

\echo "Created Possessions Table"

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (1, 'laptop', 1050, 'tech', 1);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (2, 'laptop', 900, 'tech', 2);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (3, 'laptop', 1100, 'tech', 3);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (4, 'mug', 10, 'home', 4);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (5, 'mug', 5, 'home', 1);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (6, 'phone', 100, 'tech', 2);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (7, 'car', 10000, 'tech', 8);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (8, 'headphones', 40, 'tech', 5);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (9, 'headphones', 30, 'tech', 8);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (10, 'mug', 3, 'home', 8);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (11, 'laptop', 800, 'tech', 4);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (12, 'standing desk', 200, 'home', 4);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (13, 'black jacket', 60, 'attire', 2);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (14, 'shoes', 50, 'attire', 3);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (15, 'skateboard', 200, 'attire', 3);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (16, 'running shoes', 100, 'attire', 5);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (17, 'climbing shoes', 165, 'attire', 4);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (18, 'basketball', 40, 'home', 5);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (19, 'lunch box', 30, 'home', 10);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (20, 'hydro flask', 40, 'home', 8);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (21, 'laptop', 1200, 'tech', 4);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (22, 'laptop', 975, 'tech', 5);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (23, 'laptop', 1100, 'tech', 7);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (24, 'laptop', 2000, 'tech', 6);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (25, 'laptop', 1400, 'tech', 9);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (26, 'laptop', 1700, 'tech', 10);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (27, 'laptop', 1600, 'tech', 12);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (28, 'laptop', 1200, 'tech', 8);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (29, 'brewing equipment', 3000, 'tech', 9);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (30, 'mug', 400, 'home', 6);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (31, 'lunch box', 1000, 'home', 12);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (32, 'keyboard', 500, 'tech', 13);

INSERT INTO
  possessions (id, name, cost, type, owner_id)
VALUES
  (33, 'board game', 50, 'home', 7);
```
#### Terminal Commands

`CREATE DATABASE`
psql lecture < lecture_demo.sql

#### The basics of SQL queries

- All sql commands must end with semicolon ;
- `SELECT` : choose which columns to extract data from
- `FROM`: specifies the _relation_ (table) you're getting data from
- `WHERE`/`WHERE NOT`: filters the data according to a logical expression
    - `=`, `>=`, `<=`, `>`, `<`, `<>`/`!=`
    - `IN`, `BETWEEN`, `LIKE`, (`%`) - wildcard for any number of characters `foo%` == foobar
    - `AND`, `OR`
- All names must use 'single quotes'

### Challenges
- Select my id
	- ![[CleanShot 2023-06-20 at 10.59.02@2x.png]]
	- 
- Select all of my possessions using my id
	- ![[CleanShot 2023-06-20 at 10.58.31@2x.png]]
	- 
- Select the names of the SF instructors whose names starts with a M
	- ![[CleanShot 2023-06-20 at 10.57.54@2x.png]]
	- 
- Get distinct names from possessions
	-  ![[CleanShot 2023-06-20 at 10.49.51@2x.png]]
	- 
- Get the name and cost of the second most expensive possession whose name has at least two words
	- ![[CleanShot 2023-06-20 at 10.48.14@2x.png]]
	- 
- Get the names of SF Instructors who do not have a pod leader
	- ![[CleanShot 2023-06-20 at 11.00.50@2x.png]]
	- 
- Get the average cost of all possessions
	- ![[CleanShot 2023-06-20 at 11.02.16@2x.png]]
- Count the total number of possessions
	- ![[CleanShot 2023-06-20 at 11.05.48.jpg]]
	- 
- Count the distinct type of possessions
	- ![[CleanShot 2023-06-20 at 11.10.15.jpg]]
- For each type of possession, show the type and the number of items
	- ![[CleanShot 2023-06-20 at 11.20.22.jpg]]
- For each type of possession with 5 or more items, show the type and number of each 
	- ![[CleanShot 2023-06-20 at 11.30.39.jpg]]
- Of the most common item, list the ones that costs over $1000
	- ![[CleanShot 2023-06-20 at 11.48.03.jpg]]
	- 
- How many types of possessions have a total cost over $200
	- ![[CleanShot 2023-06-20 at 11.58.49.jpg]]
	- 
- Who is the owner of the most expensive item
	- ![[CleanShot 2023-06-20 at 13.42.02.jpg]]
	- 
- Show the name of all possessions and their owner
	- `SELECT sf_instructors.name, possessions.name FROM possessions INNER JOIN sf_instructors ON possessions.owner_id = sf_instructors.id;
	- ![[CleanShot 2023-06-20 at 13.47.34.jpg]]
	- 
- Find the total number of possessions owned by each person
	```sql
	SELECT sf_instructors.name, COUNT(cost)
	FROM possessions
		FULL OUTER JOIN sf_instructors ON possessions.owner_id sf_instructors.id
	GROUP BY sf_instructors.name;
	```
- Get all aA pod leaders
	 ```sql
	 SELECT *
	 FROM sf_instructors
		JOIN sf_instructors AS pod_leaders ON sf_instructors.pod_leader_id pod_leaders.id
	```

#### Common SQL Filters and Commands
- `ORDER BY`: Sorts results based on a specific column
    - `ASC` or `DESC`
    - `ASC` is default
- `LIMIT`: how many rows you want in the result
- `OFFSET`: how many rows you want to skip from the top
- `DISTINCT`: De-duplicates data in a result (like `Array#uniq`)
    - `SELECT DISTINCT name, type`
    - `SELECT COUNT(DISTINCT name)`

#### Null
- Comparisons to `NULL` don't work in SQL
- `NULL` represents an unknown value
    - `NULL` is not a value, it is a non-value
- Use `IS NULL` and `IS NOT NULL` to check for null values

#### Using Aggregate Functions
- Aggregate functions combine data from a column into a single value
- You should _always_ use an alias with aggregate functions to make for clearer results
- `COUNT`, `SUM`, `AVG`, `MIN`/`MAX`, [and more](http://www.postgresql.org/docs/9.4/static/functions-aggregate.html)

#### GROUP BY
- `GROUP BY` groups rows with matching values for given column
    - Collapses each group of rows into a single row
- Any column we `SELECT` must be in our `GROUP BY`
- Aggregate functions in `SELECT` will apply to the individual groups, not the groups as a whole

#### WHERE vs HAVING
- `HAVING` works like `WHERE`, but...
    - `WHERE` gets evaluated **_before_** `GROUP BY`.
    - `HAVING` gets evaluated **_after_** `GROUP BY`.
- Since the `WHERE` clause gets executed before the `GROUP BY` clause, grouped entries cannot be filtered by `WHERE`
    - `HAVING` is same as the `WHERE` clause but is applied on grouped entries
    - **Aggregate functions** are not allowed in `WHERE`. You must use **aggregate functions** in `HAVING`

#### Order of operation execution in SQL
1. FROM
2. JOIN
3. WHERE
4. GROUP BY
5. HAVING
6. SELECT
7. ORDER BY
8. LIMIT / OFFSET

#### Can I use the result of a query in a different query?
- Ex: What is the most common possession -- and which ones cost more than $1,000?

#### Answer: Yes -- Use a subquery!
Sometimes it's useful to use the result of a query inside another query. This is a _Subquery_.
- Most commonly used in the `WHERE` clause:
    - `WHERE IN` _Subquery_
    - `WHERE NOT IN` _Subquery_
- When to use a subquery:
    - You'll want to use a subquery if your query follows the logic of "Get me this data A, as long as it is in this dataset B"

#### When do we join tables rather than using a subquery?
- When you have lots of data across many tables
- Subqueries use less memory than joins
- Subqueries use more CPU than joins (CPU is usually the bottleneck)
- In practice, this can differ between SQL engines

#### JOINS
- Combine data from multiple tables into one _relation_ using a JOIN
- Types of relationships between tables:
    - One-to-many (hierarchical)
        - Ex: Each TA has one pod leader, and each pod-leader has many TAs
    - Many-to-many (horizontal)
        - Ex: Each SF TA has many NY TA friends, and each NY TA has many SF TA friends


#### The 3 Most Common Types of JOINs
- `INNER JOIN`
    - returns only rows from `table1` and `table2` that match each other. This is the default.
- `LEFT OUTER JOIN` - same as `LEFT JOIN`
    - returns all rows in `table1`, whether or not they match `table2`. Not supported by all engines.
- `FULL OUTER JOIN`
    - returns all rows in `table1` and `table2`, whether or not their data matches up

#### Today, you're going to be writing SQL code in a ruby file
- Write an "execute" function to handle DB connection
- Enter SQL queries into "heredocs" (multi-line strings)
- This is how you'll be writing SQL today (to run specs), but please also use the `psql` interface to debug and see what your queries return.

#### Ruby and SQL
```ruby
require 'pg'
def execute(sql)
	# open connection to Postgres
	connection = PG::Connection.open(dbname: 'lecture')
	# execute query
	query_result = connection.exec(sql).values 
	#returns an array of arrays to represent a table
	# close connection to Postgres
	connection.close
	# return result of query
	query_result
end

def example_query
	# Final way adding the heredoc straight into the execute method with funny parentheses
	execute(<<-SQL)
		SELECT
		*
		FROM
		sf_instructors;
	SQL
	# Second, heredoc way of writing this method:

	# query = <<-SQL
		# SELECT
		# *
		# FROM
		# app_academy;
	# SQL
	
	# execute(query)
	# First way:
	# execute("SELECT * FROM app_academy;")
end
p example_query
```
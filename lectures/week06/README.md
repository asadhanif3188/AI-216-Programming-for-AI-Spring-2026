# AI-216: Programming for Artificial Intelligence
## Week 06 – Web Scraping, Data Sources & SQLite

---

## Lecture Overview

Until Week 5, we focused on **working with data that was already available**.

But in real AI systems, the first challenge is often:

> **Where does the data come from?**

In this lecture we introduce three key ideas:

- Web scraping (intro level)
- Databases and structured storage
- Ethical data collection

These topics connect programming skills with **real-world data pipelines** used in AI systems.

---

## Learning Objectives

After completing this lecture, students will be able to:

- Explain how web scraping works
- Extract simple information from web pages
- Store structured data in SQLite databases
- Connect Python programs to databases
- Understand ethical issues in data collection

---

# 1. Where Data Comes From in AI Systems

In real-world AI projects, data may come from:

- APIs
- Web scraping
- Databases
- Logs and sensors
- Public datasets

Example pipeline:

```text
Website → Scraper → Cleaning → Database → ML Model
```

Understanding this pipeline is essential before training machine learning models.

---

# 2. Introduction to Web Scraping

Web scraping is the process of **automatically extracting data from websites**.

Common Python tools:

- `requests` → download web pages
- `BeautifulSoup` → parse HTML

Install required libraries:

```python
pip install requests
pip install beautifulsoup4
```

---

## Basic Example – Downloading a Web Page

We first fetch the HTML of a webpage using the `requests` library.

Example website (safe for practice):

`https://example.com`

```python
import requests

url = "https://example.com"
response = requests.get(url)

print("Status Code:", response.status_code)
print(response.text[:300])
```

Concepts:

- HTTP request
- HTML response
- Inspecting raw webpage structure

---

## Basic Example – Scraping a Simple Educational Website

Practice site for scraping:

`http://quotes.toscrape.com`

This website is intentionally built for learning web scraping.

```python
import requests
from bs4 import BeautifulSoup

url = "http://quotes.toscrape.com"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

print(soup.title.text)
```

---

## Intermediate Example – Extracting Quotes from a Webpage

The site `quotes.toscrape.com` contains quotes structured like this:

```html
<span class="text">"Quote text"</span>
<small class="author">Author Name</small>
```

Scraping quotes:

```python
quotes = soup.find_all("span", class_="text")

for q in quotes:
    print(q.text)
```

---

## Intermediate Example – Extracting Quote + Author

```python
quotes = soup.find_all("div", class_="quote")

for q in quotes:
    text = q.find("span", class_="text").text
    author = q.find("small", class_="author").text

    print(text, "-", author)
```

This demonstrates **nested HTML parsing**.

---

## Intermediate Example – Extracting Multiple Pages

Many websites contain multiple pages.

Example:

`http://quotes.toscrape.com/page/1/`

```python
import requests
from bs4 import BeautifulSoup

url = "http://quotes.toscrape.com/page/1/"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")
quotes = soup.find_all("div", class_="quote")

for q in quotes:
    text = q.find("span", class_="text").text
    author = q.find("small", class_="author").text

    print(text, "-", author)
```

Students can modify the URL to scrape **multiple pages**.

---

## Advanced Example – Creating a Structured Dataset from Scraped Data

```python
import pandas as pd

quotes_list = []
authors_list = []

quotes = soup.find_all("div", class_="quote")

for q in quotes:
    quotes_list.append(q.find("span", class_="text").text)
    authors_list.append(q.find("small", class_="author").text)


df = pd.DataFrame({
    "Quote": quotes_list,
    "Author": authors_list
})

print(df)
```

Now scraped data becomes **structured data** suitable for analysis.

---

## Advanced Example – Scraping Table Data

Example practice site with tables:

`https://www.scrapethissite.com/pages/simple/`

```python
import requests
from bs4 import BeautifulSoup

url = "https://www.scrapethissite.com/pages/simple/"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

countries = soup.find_all("div", class_="country")

for c in countries:
    name = c.find("h3", class_="country-name").text.strip()
    capital = c.find("span", class_="country-capital").text
    population = c.find("span", class_="country-population").text

    print(name, capital, population)
```

This example shows how web scraping can be used to collect **real datasets from structured webpages**.

---

## Realistic Mini Pipeline

A simple data collection pipeline could look like this:

```python
# Step 1: Download webpage
# Step 2: Parse HTML with BeautifulSoup
# Step 3: Extract structured fields
# Step 4: Store results in a list
# Step 5: Convert to Pandas DataFrame
# Step 6: Save to CSV
```

Example:

```python
import pandas as pd

# df created from scraped data

df.to_csv("scraped_quotes.csv", index=False)
```

This demonstrates how web scraping becomes the **first stage of a data pipeline**.

---

# 3. Introduction to Databases

In many real-world systems, scraped or collected data must be **stored for later use**. Saving data only in variables or CSV files is not sufficient when:

- The dataset becomes large
- Multiple programs need to access the same data
- Data must persist between program runs

This is where **databases** are used.

---

## What is a Database?

A **database** is an organized collection of data that allows efficient storage, retrieval, and management.

Instead of storing information in scattered files, a database stores it in a **structured format**.

Example (table structure):

| id | name   | price |
|----|--------|-------|
| 1  | Laptop | 120000|
| 2  | Mouse  | 1500  |
| 3  | Keyboard | 4500 |

Each row is called a **record**.
Each column represents a **field (attribute)**.

---

## Why Databases Are Important in AI Systems

Databases allow us to:

- Store large datasets
- Retrieve data efficiently
- Maintain structured data
- Support data pipelines for machine learning

Example AI workflow:

```text
Web Scraping → Data Cleaning → Database → Machine Learning Model
```

Instead of repeatedly scraping the same website, data is stored once in a database.

---

## Basic Database Concepts

Students new to databases should understand a few fundamental terms.

### Table

A **table** is similar to a spreadsheet where data is organized into rows and columns.

Example:

| StudentID | Name  | Marks |
|-----------|-------|-------|
| S01       | Ali   | 78    |
| S02       | Sara  | 92    |

---

### Row (Record)

A **row** represents a single entry in the table.

Example row:

```text
S01 | Ali | 78
```

---

### Column (Field)

A **column** represents a specific attribute of the data.

Examples:

- Name
- Price
- Marks

---

### Primary Key

A **primary key** uniquely identifies each row in a table.

Example:

```text
StudentID
ProductID
OrderID
```

Primary keys prevent duplicate records.

---

## Types of Databases

There are two major categories of databases.

### Relational Databases

Data is stored in **tables with rows and columns**.

Examples:

- SQLite
- MySQL
- PostgreSQL

Relational databases use **SQL (Structured Query Language)** to access data.

---

### NoSQL Databases

Used for flexible or large-scale data storage.

Examples:

- MongoDB
- Cassandra

These are often used in large-scale distributed systems.

---

## Why We Use SQLite in This Course

SQLite is a lightweight relational database.

Advantages:

- No separate server required
- Built directly into Python
- Simple file-based database
- Easy for beginners

A SQLite database is stored as a single file:

```text
products.db
```

---

## Example: Data Stored in SQLite

Imagine storing scraped product data.

Table: **products**

| id | name | price |
|----|------|------|
| 1 | Laptop | 120000 |
| 2 | Mouse | 1500 |
| 3 | Keyboard | 4500 |

Later, Python programs can retrieve and analyze this information.

---

## Databases vs CSV Files

Why databases are used instead of CSV files.

| Feature | CSV File | Database |
|--------|----------|---------|
| Data size | Small datasets | Large datasets |
| Querying | Limited | Powerful queries |
| Structure | Flat | Structured tables |
| Performance | Slower for large data | Faster retrieval |

CSV files are useful for **data exchange**, while databases are better for **data storage and management**.

---

## Simple SQL Concept (Preview)

SQL is used to interact with relational databases.

Example query:

```sql
SELECT * FROM products
```

Meaning:

> Retrieve all records from the products table.

Another example:

```sql
SELECT name, price FROM products
```

This retrieves only selected columns.

Students will not learn full SQL in this course, but understanding these basics helps connect Python programs with databases.

---

# 4. Working with SQLite in Python

Python provides built‑in support for SQLite through the **`sqlite3`** module. This allows programs to create databases, store data, and retrieve it later.

SQLite databases are stored as a **single file** on disk.

Example:

```text
products.db
```

This makes SQLite ideal for small applications, experiments, and data collection pipelines.

---

## Basic Workflow

Typical steps when working with SQLite in Python:

```text
1. Connect to database
2. Create a cursor
3. Execute SQL queries
4. Commit changes
5. Close connection
```

---

## Basic Example – Connecting to a Database

```python
import sqlite3

conn = sqlite3.connect("store.db")
cursor = conn.cursor()

print("Database connected successfully")

conn.close()
```

If the database file does not exist, SQLite **automatically creates it**.

---

## Example – Creating a Table

```python
import sqlite3

conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    name TEXT,
    price INTEGER
)
""")

conn.commit()
conn.close()
```

This creates a table named **products**.

---

# Creating Multiple Tables

Real systems often contain **multiple related tables**.

Example database structure:

```text
products table
customers table
orders table
```

### Example

```python
conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("""
CREATE TABLE customers (
    id INTEGER PRIMARY KEY,
    name TEXT,
    city TEXT
)
""")

cursor.execute("""
CREATE TABLE orders (
    id INTEGER PRIMARY KEY,
    customer_id INTEGER,
    product_name TEXT,
    quantity INTEGER
)
""")

conn.commit()
conn.close()
```

Now the database contains **three tables**.

---

# CRUD Operations

CRUD stands for:

```text
Create
Read
Update
Delete
```

These operations form the basis of database interaction.

---

## CREATE – Inserting Data

```python
conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("""
INSERT INTO products (name, price)
VALUES ('Laptop', 120000)
""")

cursor.execute("""
INSERT INTO customers (name, city)
VALUES ('Ali', 'Karachi')
""")

conn.commit()
conn.close()
```

---

## CREATE – Inserting Multiple Records

```python
products = [
    ('Mouse', 1500),
    ('Keyboard', 4500),
    ('Monitor', 35000)
]

conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.executemany("INSERT INTO products (name, price) VALUES (?, ?)", products)

conn.commit()
conn.close()
```

---

## READ – Retrieving Data

```python
conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("SELECT * FROM products")
rows = cursor.fetchall()

for row in rows:
    print(row)

conn.close()
```

---

## READ – Filtering Data

```python
cursor.execute("SELECT name, price FROM products WHERE price > 5000")
rows = cursor.fetchall()

for row in rows:
    print(row)
```

---

## UPDATE – Modifying Existing Records

```python
conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("""
UPDATE products
SET price = 130000
WHERE name = 'Laptop'
""")

conn.commit()
conn.close()
```

---

## DELETE – Removing Records

```python
conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("DELETE FROM products WHERE name = 'Mouse'")

conn.commit()
conn.close()
```

---

# Example – Working with Multiple Tables

Consider the following scenario:

- A **customer** places an order
- The order references a product

Example insertion:

```python
conn = sqlite3.connect("store.db")
cursor = conn.cursor()

cursor.execute("""
INSERT INTO orders (customer_id, product_name, quantity)
VALUES (1, 'Laptop', 2)
""")

conn.commit()
conn.close()
```

---

## Example – Simple Join Query

Sometimes we need to combine data from multiple tables.

```python
query = """
SELECT customers.name, orders.product_name, orders.quantity
FROM customers
JOIN orders ON customers.id = orders.customer_id
"""

cursor.execute(query)
rows = cursor.fetchall()

for row in rows:
    print(row)
```

This retrieves **customer orders with names instead of IDs**.

---

# Storing Scraped Data in a Database

Now we can connect this with web scraping.

Pipeline example:

```text
Website → Scraping → Extract Data → Store in SQLite
```

Example:

```python
cursor.execute(
    "INSERT INTO products (name, price) VALUES (?, ?)",
    (product_name, product_price)
)
```

This demonstrates how **data collection pipelines store information for later analysis**.

---

# 5. Ethical Data Collection

Not all web scraping is acceptable.

Key principles:

- Respect **robots.txt** rules
- Avoid overloading servers
- Do not scrape private data
- Respect website terms of service

Example robots file:

```text
User-agent: *
Disallow: /private
```

Meaning: bots should not access `/private` pages.

---

## Ethical vs Unethical Data Collection

Ethical:

- Public datasets
- Academic research
- Rate-limited scraping

Unethical:

- Scraping private user information
- Ignoring robots rules
- Excessive automated traffic

Responsible AI requires **ethical data practices**.

---

# 6. Mini Pipeline Example

Example workflow combining everything learned.

```python
# 1. Scrape webpage
# 2. Extract product data
# 3. Convert to DataFrame
# 4. Store in SQLite database
```

This represents the early stage of **real AI data pipelines**.

---

# 7. ChatGPT Prompts for Learning (Allowed Use)

Students may use AI tools for learning and debugging.

---

## A. Understanding Web Scraping

"Explain how requests and BeautifulSoup work together."

"Why do we parse HTML instead of searching strings?"

"What is the difference between find() and find_all()?"

---

## B. Debugging Scraping Code

"Why does my scraper return None when extracting elements?"

"How can I inspect the HTML structure of a webpage?"

"Explain this BeautifulSoup code step by step."

---

## C. SQLite & Databases

"How does SQLite store tables internally?"

"Explain how Python interacts with SQLite databases."

"Why do we use parameterized queries (?, ?) in SQL?"

---

## D. Ethical Data Collection

"What are ethical concerns in web scraping?"

"How can developers ensure responsible data collection?"

---

<!-- # 8. Looking Ahead

Next week we will explore:

- Exploratory Data Analysis (EDA)
- Data visualization
- Feature preparation for machine learning

Understanding where data comes from is essential before building AI models.

---

**End of Week 06 Lecture** -->


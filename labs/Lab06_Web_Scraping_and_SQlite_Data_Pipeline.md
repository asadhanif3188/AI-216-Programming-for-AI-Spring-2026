# AI-216 – Programming for Artificial Intelligence
## Lab 06: Web Scraping and SQLite Data Pipeline

---

### Week #: 06
### Topic: Web Scraping, SQLite Databases & Ethical Data Collection

---

## 1. Objective

The objective of this lab is to help students understand **where real-world data comes from and how it is stored for later analysis**.

Students will:

- Perform basic web scraping using `requests` and `BeautifulSoup`
- Extract structured information from webpages
- Store collected data in a SQLite database
- Perform basic database queries using Python
- Understand responsible and ethical data collection

This lab is inspired by the structure of previous SQLite database exercises and database practice workflows, but the problem scenarios and datasets are different.

---

## 2. Tools & Requirements

Required Python libraries:

- requests
- beautifulsoup4
- sqlite3 (built into Python)

Optional for testing:

- pandas

Install required libraries if needed:

```bash
pip install requests
pip install beautifulsoup4
```

---

# 3. Part A – Web Scraping Practice

Practice website for scraping:

```
http://quotes.toscrape.com
```

This website is designed for learning scraping.

---

### Task 1 – Extract Quote Information

Write a Python program that:

1. Downloads the webpage.
2. Extracts all quotes from the page.
3. Extracts the author of each quote.
4. Stores the results in a list of dictionaries.

Example structure of your collected data:

```python
{
    "quote": "Text of the quote",
    "author": "Author Name"
}
```

Focus Concepts:

- HTTP requests
- HTML parsing
- `find()` and `find_all()`

---

### Task 2 – Collect Multi‑Page Data

Extend your scraper so that it collects quotes from **at least three pages** of the website.

Example pages:

```
http://quotes.toscrape.com/page/1/
http://quotes.toscrape.com/page/2/
http://quotes.toscrape.com/page/3/
```

Requirements:

1. Combine all scraped data into one dataset.
2. Count how many quotes were collected in total.
3. Print the first five quotes with authors.

Focus Concepts:

- Iterating over URLs
- Data aggregation

---

# 4. Part B – Creating a SQLite Database

Create a SQLite database named:

```
quotes.db
```

---

### Task 3 – Database Setup

Create the following table structure.

Table: **quotes**

Columns:

| Column | Type |
|------|------|
| id | INTEGER PRIMARY KEY |
| quote | TEXT |
| author | TEXT |

Requirements:

1. Connect to the database.
2. Create the table if it does not already exist.
3. Print confirmation when the table is created.

Focus Concepts:

- sqlite3 connection
- SQL table creation

---

### Task 4 – Store Scraped Data

Insert the scraped quotes into the database.

Requirements:

1. Insert all quotes collected in Part A.
2. Use parameterized queries (`?`).
3. Commit changes after insertion.

Focus Concepts:

- INSERT queries
- executemany()

---

# 5. Part C – Database Queries

Perform the following queries using Python and SQLite.

---

### Task 5 – Reading Data

1. Retrieve all quotes from the database.
2. Print the total number of stored quotes.
3. Display the first 10 quotes.

Focus Concepts:

- SELECT queries
- fetchall()

---

### Task 6 – Filtering Data

Write queries that:

1. Retrieve all quotes written by a specific author.
2. Count how many quotes each author has in the dataset.
3. Display authors sorted by number of quotes.

Focus Concepts:

- WHERE clause
- GROUP BY
- ORDER BY

---

# 6. Part D – Updating and Cleaning Data

---

### Task 7 – Update Records

Write a program that:

1. Selects one author from the database.
2. Updates that author's name to uppercase.

Focus Concepts:

- UPDATE query

---

### Task 8 – Delete Records

Remove quotes that contain fewer than **30 characters**.

Focus Concepts:

- DELETE query
- conditional filtering

---

# 7. Part E – Mini Data Pipeline

Combine scraping and database storage into a simple pipeline.

Steps:

1. Scrape quote data.
2. Store it in SQLite.
3. Query the database to produce a report.

Your program should print:

```
Total quotes stored
Total unique authors
Author with the most quotes
```

Focus Concepts:

- data pipeline thinking
- structured storage

---

# 8. Ethical Data Collection

Before scraping a website, always check the website's **robots.txt** file.

Example:

```
https://github.com/robots.txt
```

Tasks:

1. Download the robots.txt file using Python.
2. Print the first 20 lines of the file.
3. Identify at least two directories that bots should not crawl.

Focus Concepts:

- ethical scraping
- respecting website rules

---

# 9. GitHub Submission

Submit your lab in the following structure:

```
AI-216-Programming-for-AI/
└── labs/
    └── week06/
        ├── lab06.py or lab06.ipynb
        ├── quotes.db
        └── README.md
```

Your README must explain:

- How data was scraped
- How the SQLite database was structured
- One ethical concern related to scraping

---

# 10. Evaluation Criteria

| Criterion | Weight |
|---------|--------|
| Web scraping implementation | 30% |
| SQLite database design | 25% |
| Query logic and filtering | 20% |
| Data pipeline integration | 15% |
| Code clarity & documentation | 10% |

---

**End of Lab 06**


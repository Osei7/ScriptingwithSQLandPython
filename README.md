# Coffee Shop Employee Management System

## Project Overview
This project is designed to manage and analyze employee data for a chain of coffee shops. It includes scripts to create a PostgreSQL database, populate it with employee data, and perform various analytical queries. This project showcases advanced database management, data engineering, scripting skills, and the ability to write and optimize SQL queries.

## Repository Structure

### Python Scripts
- **`sql_with_python_final.py`**: Main script used to set up the database, create tables, and insert data. This script demonstrates proficiency in Python programming, use of libraries such as `psycopg2` for database connections, and `pandas` for data manipulation.
- **`sql_queries.py`**: Contains all SQL queries used in the project. This file is imported into the main script to maintain clean code and enhance readability and maintainability.

### Configuration Files
- **`private.cfg`**: Configuration file storing database credentials and parameters. This file is not included in the repository for security reasons but is crucial for the operation of the main script.

### Data Files
- **`coffeeshop.csv`**: CSV file containing initial data for populating the `employees` table in the database.

## Setup and Installation

### Requirements
- Python 3.8+
- PostgreSQL
- Libraries: `psycopg2-binary`, `pandas`

### Installation
1. Ensure Python and PostgreSQL are installed on your system.
2. Install required Python libraries:
   ```
   pip install psycopg2-binary pandas
   ```
3. Clone this repository to your local machine.

### Configuration
1. Create a `private.cfg` file in the project root with the following content:
   ```
   [SQL]
   DB_NAME_DEFAULT = your_default_db_name
   DB_USER = your_db_username
   DB_PASSWORD = your_db_password
   ```

## Usage

To run the project:
1. Navigate to the project directory.
2. Run the script:
   ```
   python sql_with_python_final.py
   ```

## SQL Queries

The project includes several key SQL operations, outlined in the `sql_queries.py` file:

### Table Creation
- **Employees Table**:
  ```sql
  CREATE TABLE IF NOT EXISTS employees (
      employee_id INT PRIMARY KEY,
      first_name VARCHAR(50),
      last_name VARCHAR(50),
      email VARCHAR(50),
      hire_date DATE,
      shop_name VARCHAR(50),
      salary INT
  )
  ```

### Data Insertion
- **Insert into Employees**:
  ```sql
  INSERT INTO employees (employee_id, first_name, last_name, email, hire_date, shop_name, salary)
  VALUES (%s, %s, %s, %s, %s, %s, %s)
  ```

### Analytical Queries
Here is the extended `README.md` section on SQL queries, now including detailed explanations for each query along with the three additional ones I previously generated for you. This section clearly explains the purpose and functionality of each SQL operation in your Coffee Shop Employee Management System:

---

## Analytical Queries
- **Average, Minimum, and Maximum Salary**:
  ```sql
  SELECT ROUND(AVG(salary), 0), MIN(salary), MAX(salary) FROM employees;
  ```
  **Purpose**: This query calculates and returns the average, minimum, and maximum salaries among all employees in the database. The results help understand salary distribution and disparities.

- **Employee Count by Shop**:
  ```sql
  SELECT shop_name, COUNT(*) FROM employees GROUP BY shop_name ORDER BY COUNT(*) DESC;
  ```
  **Purpose**: This query determines the number of employees working at each coffee shop, ordered from the most to the least staffed. It provides insights into staffing levels across different locations.

- **Average Salary by Shop**:
  ```sql
  SELECT shop_name, ROUND(AVG(salary), 0) FROM employees GROUP BY shop_name ORDER BY AVG(salary);
  ```
  **Purpose**: This query calculates the average salary per coffee shop and orders the results from lowest to highest. It can be used to analyze salary fairness and competitiveness among shops.

- **Employee Tenure and Average Salary by Shop**:
  ```sql
  SELECT shop_name, ROUND(AVG(EXTRACT(YEAR FROM AGE(hire_date))), 2) AS average_tenure, ROUND(AVG(salary), 0) AS average_salary FROM employees GROUP BY shop_name ORDER BY average_tenure DESC;
  ```
  **Purpose**: This query evaluates the average tenure of employees and the average salary at each shop, sorted by tenure. It helps in assessing if longer tenure correlates with higher salaries and may indicate employee satisfaction and retention rates.

- **Employee Distribution by Hire Year**:
  ```sql
  SELECT EXTRACT(YEAR FROM hire_date) AS hire_year, COUNT(*) AS number_of_hires FROM employees GROUP BY hire_year ORDER BY hire_year;
  ```
  **Purpose**: This query analyzes hiring trends over the years, showing how many employees were hired each year. It is valuable for understanding growth phases or recruitment drives.

- **Detailed Employee List by Shop with Salary Range**:
  ```sql
  SELECT shop_name, first_name, last_name, salary FROM employees ORDER BY shop_name, salary DESC;
  ```
  **Purpose**: This query lists all employees within each shop, ordered by salary in descending order. It provides a detailed payroll review, helping to identify the highest and lowest earners at each location and potentially guide compensation strategies.


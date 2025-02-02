📌 SQL Queries for Database Testing

📖 Overview
This repository contains SQL scripts useful for database testing in automation. These scripts help with data validation, test data setup, cleanup, and integrity checks during automated testing.

🎯 Use Cases
✅ Validate data correctness after test execution
✅ Prepare test data before running automation
✅ Clean up data after tests to maintain consistency
✅ Verify database constraints, joins, and indexing
✅ Automate SQL query execution in Selenium, Rest Assured, or API tests

📂 Project Structure

📦 database-testing-sql-scripts
 ┣ 📜 01_data_validation.sql
 ┣ 📜 02_test_data_setup.sql
 ┣ 📜 03_test_data_cleanup.sql
 ┣ 📜 04_joins_and_constraints.sql
 ┣ 📜 05_performance_queries.sql
 ┣ 📜 README.md
 
🚀 SQL Scripts & Usage

📌 1. Data Validation Queries
🔹 Verify data correctness in key tables after tests.

-- Verify if a user exists in the database after registration
SELECT * FROM users WHERE email = 'testuser@example.com';

-- Check if order status is updated correctly after payment
SELECT order_id, status FROM orders WHERE order_id = 1001 AND status = 'Paid';

📌 2. Test Data Setup Queries
🔹 Insert test data into tables before test execution.

-- Insert a test user for automation
INSERT INTO users (id, name, email, created_at)
VALUES (101, 'Test User', 'testuser@example.com', NOW());

-- Add test products before running UI automation
INSERT INTO products (product_id, name, price, stock)
VALUES (501, 'Test Product', 99.99, 10);

📌 3. Test Data Cleanup Queries
🔹 Remove test records after test execution.

-- Delete test user to maintain database consistency
DELETE FROM users WHERE email = 'testuser@example.com';

-- Remove test orders older than 7 days
DELETE FROM orders WHERE created_at < NOW() - INTERVAL '7 days';

📌 4. Queries for Joins & Constraints Testing
🔹 Verify database integrity, relationships, and constraints.

-- Check if a user has placed orders (JOIN example)
SELECT u.name, o.order_id, o.status 
FROM users u 
JOIN orders o ON u.id = o.user_id 
WHERE u.email = 'testuser@example.com';

-- Validate foreign key constraint (user should have at least one order)
SELECT u.id, COUNT(o.order_id) AS order_count
FROM users u 
LEFT JOIN orders o ON u.id = o.user_id
GROUP BY u.id
HAVING COUNT(o.order_id) = 0;

📌 5. Performance & Index Testing Queries
🔹 Optimize queries and test index performance.

-- Find slow queries (for performance tuning)
EXPLAIN ANALYZE SELECT * FROM orders WHERE status = 'Pending';

-- Check if an index is used in a query
EXPLAIN SELECT * FROM users WHERE email = 'testuser@example.com';

⚙️ How to Run Queries

You can execute these queries in:
🔹 MySQL Workbench (for MySQL databases)
🔹 pgAdmin (for PostgreSQL)
🔹 SQL Server Management Studio (SSMS) (for SQL Server)
🔹 Automation Scripts using JDBC (Java), PyODBC (Python), or SQLAlchemy

🔗 Integration with Automation Frameworks
💡 Using SQL queries in Selenium with Java (JDBC Example):

Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/testdb", "username", "password");
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM users WHERE email = 'testuser@example.com'");
while (rs.next()) {
    System.out.println("User Found: " + rs.getString("name"));
}
con.close();

💡 Using SQL queries in Python with PyODBC:

import pyodbc

conn = pyodbc.connect('DRIVER={SQL Server};SERVER=localhost;DATABASE=testdb;UID=user;PWD=password')
cursor = conn.cursor()
cursor.execute("SELECT * FROM users WHERE email = 'testuser@example.com'")
for row in cursor.fetchall():
    print("User Found:", row.name)
conn.close()

📌 Best Practices for Database Testing

✅ Use test-specific databases to avoid impacting production data
✅ Always rollback transactions after running tests
✅ Use parameterized queries to prevent SQL injection
✅ Avoid using DELETE without WHERE (to prevent data loss)
✅ Regularly optimize indexes for better query performance

🤝 Contributing

🔹 Feel free to add more SQL queries for different test scenarios.
🔹 Open a pull request if you find any improvements.
🔹 Raise an issue for bugs or suggestions.

📜 License

This repository is licensed under the MIT License.

📬 Connect with Me
💼 GitHub: KalpeshJain18
📧 Email: jainkalpesh597@gmail.com

🚀 Happy Testing! 🎯

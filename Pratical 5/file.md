
### **Aim:**
The aim is to create a relational database with tables, utilizing primary keys and foreign keys to establish relationships between the tables. 
This approach will ensure referential integrity and data consistency across the database.

### **Objective:**
The objective is to create a relational database with tables that have primary and foreign keys, establishing relationships between them. 
Additionally, the task involves using `ALTER TABLE` to modify the schema by adding or modifying columns in existing tables, allowing the database structure to evolve and adapt to future needs.

---

## 1. Types of Constraints in MySQL

In MySQL, the main types of constraints are:

- **NOT NULL**: Ensures a column cannot have `NULL` values.
- **UNIQUE**: Ensures all values in a column are unique.
- **PRIMARY KEY**: Combines `NOT NULL` and `UNIQUE` to uniquely identify rows.
- **FOREIGN KEY**: Enforces referential integrity by linking columns to other tables.
- **DEFAULT**: Provides a default value when none is specified.

---

## 2. Explanation of Primary and Foreign Keys

### **Primary Key**

#### **Definition**:
A **Primary Key** is a field or combination of fields in a table that uniquely identifies each row (record). It enforces both uniqueness and non-nullability of the data in that column (or columns).

#### **Key Characteristics**:
- **Uniqueness**: Every value in the primary key must be unique across all rows in the table. No two rows can have the same primary key value.
- **Non-NULL**: A primary key column cannot have `NULL` values. Every row must have a valid value for the primary key.
- **One per Table**: A table can have only one primary key, although it can consist of multiple columns (a composite key).
- **Index**: MySQL automatically creates a unique index on the primary key column(s) to speed up queries.

#### **Example**:
Let's create a table `students` where `student_id` is the primary key.

```sql
CREATE TABLE students (
    student_id INT NOT NULL,    -- Primary key column (non-null and unique)
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    PRIMARY KEY (student_id)    -- student_id is the primary key
);
```

### **Foreign Key**

#### **Definition:**
A **Foreign Key** is a column or a combination of columns in a table that refers to the primary key (or a unique key) in another table. It establishes a relationship between the two tables and enforces referential integrity.

#### **Key Characteristics:**

- **Relationship**: A foreign key creates a relationship between two tables. Typically, a foreign key column in the child table references a primary key in the parent table.
- **Referential Integrity**: It ensures that the foreign key values in the child table must either match a valid primary key value in the parent table or be `NULL` (if allowed).
- **Multiple Foreign Keys**: A table can have multiple foreign keys, each linking to different tables.
- **Can Contain NULL**: Foreign keys can contain `NULL` values unless explicitly restricted by the table schema.
- **Cascading Options**: You can define cascading actions on delete and update (e.g., `ON DELETE CASCADE`), which dictate how changes in the parent table should affect the child table.

#### **Example:**

Let's create two tables: `students` and `orders`. The `orders` table will have a `student_id` column that acts as a foreign key, referencing the `student_id` column in the `students` table.

```sql
-- Parent table: students
CREATE TABLE students (
    student_id INT NOT NULL,    -- Primary key column
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    PRIMARY KEY (student_id)
);

-- Child table: orders
CREATE TABLE orders (
    order_id INT NOT NULL,      -- Primary key column
    order_date DATE,
    student_id INT,             -- Foreign key column
    PRIMARY KEY (order_id),
    FOREIGN KEY (student_id) REFERENCES students(student_id)  -- Foreign key referencing students table
);
```

### **Advantages and Limitations of Constraints**

#### **Advantages of Constraints:**

- **Data Integrity**: Constraints ensure that the data is accurate and consistent (e.g., **PRIMARY KEY**, **UNIQUE**).
- **Prevents Invalid Data**: Constraints help in preventing the insertion of incorrect data (e.g., **NOT NULL**, **CHECK**).
- **Improves Data Quality**: Constraints help maintain valid and clean data (e.g., **CHECK** for valid ranges).
- **Enforces Relationships**: Constraints enforce referential integrity between tables (e.g., **FOREIGN KEY**).

#### **Limitations of Constraints:**

- **Performance Overhead**: Constraints can slow down insert, update, and delete operations due to the validation checks.
- **Complexity**: Overusing constraints, especially in large databases, can make the schema harder to maintain and manage.
- **Limited Flexibility**: Constraints enforce rigid rules, which may limit flexibility and make handling certain data variations more difficult.
- **Cannot Enforce All Business Logic**: Constraints ensure data integrity but cannot handle complex business rules, which may need to be coded separately in application logic.

#### **Conclusion:**
This approach ensures data integrity with primary keys (unique identifiers) and foreign keys (relationships between tables). By using `ALTER TABLE`, we can adjust the structure of tables, adding or modifying columns to meet future requirements.


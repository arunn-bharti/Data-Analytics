# SQL Practice of CRUD Operations

---

# Create Database

```sql
CREATE DATABASE db1;
```

---

# Create Table

```sql
CREATE TABLE stud(
    id SERIAL PRIMARY KEY,
    name VARCHAR(50) UNIQUE,
    age INT CHECK (age > 12),
    mark INT NOT NULL,
    grade CHAR(1),
    time TIMESTAMP DEFAULT NOW()
);
```

---

# Insert Data

```sql
INSERT INTO stud (name, age, mark, grade)
VALUES ('Arun', 20, 450, 'A');

INSERT INTO stud (name, age, mark, grade)
VALUES ('Dev', 22, 440, 'A');

INSERT INTO stud (name, age, mark, grade)
VALUES ('Neha', 21, 400, 'B');
```

---

# Select Data

```sql
SELECT * FROM stud;
```

---

# Update Data

```sql
UPDATE stud
SET age = 19
WHERE name = 'Neha';
```

---

# Drop Table

```sql
DROP TABLE stud;
```
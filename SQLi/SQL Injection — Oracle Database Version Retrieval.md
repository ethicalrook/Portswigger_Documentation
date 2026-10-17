# [SQL Injection — Oracle Database Version Retrieval]

**Lab:** PortSwigger Web Security Academy — SQL injection attack, querying the database type and version on Oracle    
**Difficulty:** Practitioner    
**Vulnerability:** UNION-based SQL injection  
  
### Objective  
Retrieve the Oracle database version string through the product category filter.  
  
### Approach  
- Tested `ORDER BY 1`, `ORDER BY 2`, and `ORDER BY 3` to infer that the original query returned **two columns**.  
- Identified Oracle's `V$VERSION` view and `BANNER` field as the version-information source.  
- Used `NULL` as a placeholder for the second column.  
- Closed the category string with `'` and used `--` to comment out the remaining SQL.  
  
### Successful Payload  
```sql  
Pets' UNION SELECT BANNER,NULL FROM V$VERSION--  
```  
  
### Key Learnings  
- UNION queries must return the same number of columns, with compatible data types in corresponding positions.  
- Injection syntax must match the original SQL context.  
- Oracle provides database version information through `V$VERSION`.  
- HTTP 200 alone does not prove successful SQL injection; inspect the response and verify the lab's success status.  
  
### Result  
**Lab solved:** Successfully retrieved the Oracle database version string.
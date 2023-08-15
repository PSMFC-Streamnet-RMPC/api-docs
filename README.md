# RMIS API

### **Supported Query String Operators:**

1. **Standard Comparison Operators**:
    - **`=`**: Equal to.
    - **`<>`**: Not equal to.
    - **`>`**: Greater than.
    - **`<`**: Less than.
    - **`>=`**: Greater than or equal to.
    - **`<=`**: Less than or equal to.
2. **Special Commands**:
    - **`page`**: Specify which page of results to retrieve (e.g., **`page=2`**).
    - **`perpage`**: Specify the number of results per page (e.g., **`perpage=10`**).
    - **`sort`**: Define sort order for results. Format is **`column|order`**, and multiple sorts can be comma-separated (e.g., **`sort=column1|asc,column2|desc`**).
    - **`search`**: Performs a general search on specified **`searchColumns`** in the schema. The columns are searched with a **`LIKE`** SQL operator.
    - **`fields`**: Specify specific fields/columns to retrieve in the result set, comma-separated (e.g., **`fields=column1,column2`**).
3. **Wildcard Search**:
    - If the value for a column contains **`!`**, it will be translated into a **`LIKE`** SQL operator with **`%`** replacing **`!`**. For example, **`column1=!value!`** will search for any row where **`column1`** contains the substring "value".
4. **Multiple Values**:
    - To specify multiple values for a string column, separate the values with a comma (e.g., **`column1=value1,value2`**). If used with the **`<>`** operator, it will use the **`NOT IN`** SQL operator.
    - **Important Note**: Before this function analyzes the query operators, JSON schema validation is performed. Therefore, the IN operator is only suitable for string fields. Single number fields with a comma in the value will not be recognized correctly and can result in unexpected behaviors. Ensure that only string fields use the comma-separated format when leveraging the IN operator.
5. **Date-Time Columns**:
    - For columns with a date-time format, the function will use the **`date(column)`** format in the SQL statement.

### **Notes:**

- The function prioritizes **`fields`** over **`search`** in the query string. If both are present, the function will apply filters based on **`fields`** first, then perform the search.
- If no sort conditions are specified in the query string, the results are sorted by the **`ID`** column by default.
- Pagination is applied at the end, using the **`LIMIT`** and **`OFFSET`** SQL clauses, with adjustments for certain database types like MS SQL and PostgreSQL.
- Error handling: If an error occurs, the function will return null values for the SQL statements and an error message.

### **Example:**

Given the query string **`column1=>=value1&column2=value2,value3&sort=column1|asc&page=2&perpage=5&search=searchValue`**, the function will generate:

- A SQL statement filtering rows where **`column1`** is greater than or equal to "value1", and **`column2`** is either "value2" or "value3".
- Sort the results in ascending order by **`column1`**.
- Return results for the 2nd page, with 5 results per page.
- Search specified search columns for the string "searchValue".

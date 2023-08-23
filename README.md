# RMIS API

### **Supported GET Query String Operators:**

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
    - **`search`**: Performs a general search on specified **`searchColumns`** in the schema. The columns are searched similar to a **`LIKE`** SQL operator.
    - **`fields`**: Specify specific fields/columns to retrieve in the result set, comma-separated (e.g., **`fields=column1,column2`**).
3. **Wildcard Search**:
    - If the value for a string column contains **`~`**, it will be treated as a wildcard character similar to a SQL wildcard. For example, **`column1=~value~`** will search for any row where **`column1`** contains the substring "value". The expression **`column1=~value`** will search for any row where **`column1`** ends with "value".

4. **Multiple Values**:
    - You may specify multiple values for any string field that defines an enumerated list (enum) of possible values.
    - Separate the values with a comma (e.g., **`column1=value1,value2`**). If used with the **`<>`** operator, it will select only records that **`DO NOT`** have any of the vales.
    - **Important Note**: Before this function analyzes the query operators, JSON schema validation is performed. Therefore, the multiple values operator is only suitable for string fields. Single number fields with a comma in the value will not be recognized correctly and can result in unexpected behaviors. Ensure that only string fields with an enum list use the comma-separated format when leveraging the IN operator.
<!--
5. **Date-Time Columns**:
    - For columns with a date-time format, the function will use the **`date(column)`** format in the SQL statement.
-->
### **Notes:**

- The > < <= >= <> operators will work on all data field types, but will be most useful for numbers and dates. 
- When using the > (greater than) or < (less than) operators for string
  fields, the comparison is done based on the 
  lexicographical (dictionary) order of the strings. In most databases, as in the RMIS database, 
  this lexicographical order is based on the ASCII values of the 
  characters in the strings.

  The > operator will return true if the first string is lexicographically 
  greater (comes later in the dictionary) than the second string, and 
  the < operator will return true if the first string is lexicographically 
  smaller (comes earlier in the dictionary) than the second string.

  Keep in mind that the comparison is case-sensitive, so uppercase letters 
  have lower ASCII values than lowercase letters, and consequently, 
  uppercase letters are considered "smaller" in lexicographic comparisons. 
  
- The operator evaluation prioritizes **`fields`** over **`search`** in the query string. If both are present, evaluation will apply filters based on **`fields`** first, then perform the search.
- If no sort conditions are specified in the query string, the results are sorted by the **`ID`** column by default.
- Pagination is applied at the end.

### **Example:**

Given the query string **`column1=>=value1&sort=column1|asc&page=2&perpage=5&search=searchValue`**, the function will generate:

- A SQL statement filtering rows where **`column1`** is greater than or equal to "value1".
- Sort the results in ascending order by **`column1`**.
- Return results for the 2nd page, with 5 results per page.
- Search specified search columns for the string "searchValue".

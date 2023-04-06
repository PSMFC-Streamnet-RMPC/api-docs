# api-docs
API Documentation

1. Filtering:
The query string should contain key-value pairs separated by the respective operator (<=, >=, <>, >, <, =). For example, key>=value. To filter using multiple conditions, separate each key-value pair with an ampersand (&).

Valid operators for filtering:

=: Equals
<>: Not equals
<: Less than
>: Greater than
<=: Less than or equal to
>=: Greater than or equal to
For string values, you can use the ! character as a wildcard. For example, name!john would return records where the name contains 'john'.

2. Sorting:
To sort the results, include a key-value pair with the key 'sort' and use the '=' operator. The value should be a comma-separated list of column names and their respective sorting orders ('asc' or 'desc'). For example: sort=name|asc,age|desc.

3. Pagination:
To paginate the results, include the following key-value pairs with '=' operator:

page: The page number (starting from 1)
perpage: The number of records per page
For example, page=2&perpage=20.

Here's a sample query string that filters, sorts, and paginates the results:

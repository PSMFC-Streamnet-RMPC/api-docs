# api-docs
API Documentation

## Filtering
The query string should contain key-value pairs separated by the respective operator (<=, >=, <>, >, <, =). For example, key>=value. To filter using multiple conditions, separate each key-value pair with an ampersand (&).

Valid operators for filtering:

- =: Equals
- <>: Not equals
- <: Less than
- &gt;: Greater than
- <=: Less than or equal to
- &gt;=: Greater than or equal to

For string values, you can use:
- Wilcard: the ! character can be used as a wildcard. For example, **first_name=J!** would return records where the *first_name* field starts with 'J'.
- List: multiple values may be included in a key-value pair like, **first_name=Jane,John,Sue**

## Sorting
To sort the results, include a key-value pair with the key 'sort' and use the '=' operator. The value should be a comma-separated list of column names and their respective sorting orders ('asc' or 'desc'). For example: sort=name|asc,age|desc.

## Pagination
To paginate the results, include the following key-value pairs with '=' operator:

page: The page number (starting from 1)
perpage: The number of records per page
For example, page=2&perpage=20.

Here's a sample query string that filters, sorts, and paginates the results:

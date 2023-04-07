# api-docs
API Documentation

## Filtering, Sorting, and Pagination in collection GET requests


Filtering, sorting, and pagination are essential techniques in RESTful APIs for managing large datasets. They enhance user experience and optimize performance by reducing the amount of data transferred over the network.

- *Filtering* narrows down a dataset based on specific criteria, allowing users to quickly find relevant information.

- *Sorting* orders a dataset by one or more attributes, enabling users to arrange the data according to their needs.

- *Pagination* divides a dataset into smaller chunks, allowing users to efficiently navigate through large datasets without overwhelming the client-side application or network resources.

While these features introduce some complexity in implementation, their benefits in terms of user experience, network efficiency, and server performance outweigh the drawbacks.

## Implementation



### Filtering
The query string should contain key-value pairs separated by the respective operator (<=, >=, <>, >, <, =). For example, key>=value. To filter using multiple conditions, separate each key-value pair with an ampersand (&).

Valid operators for filtering:

- =: Equals
- <>: Not equals
- <: Less than
- &gt;: Greater than
- <=: Less than or equal to
- &gt;=: Greater than or equal to

For string/date values, you can use:
- Wilcard: the ! character can be used as a wildcard. For example, **first_name=J!** would return records where the *first_name* field starts with 'J'. Or, **created=2022-02-!** would return only records where *created* equals February, 2022.
- List: multiple values may be included in a key-value pair like, **first_name=Jane,John,Sue**

### Sorting
To sort the results, include a key-value pair with the key 'sort' and use the '=' operator. The value should be a comma-separated list of field names and their respective sorting orders ('asc' or 'desc'). For example: sort=first_name|asc,created|desc.

### Pagination
To paginate the results, include the following key-value pairs with '=' operator:

- page: The page number (starting from 1)
- perpage: The number of records per page

For example, page=2&perpage=20.

Here's a sample query string that filters, sorts, and paginates the results:

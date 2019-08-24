#### REST API - CRUDS  reference

Resource vs HTTP Methods
Base url - http://localhost:8080/palmyra/{database}/

Assuming the table name is - `Users`

| Resource         | GET                                  | POST                                       | PUT                             | DELETE                   |
| ---------------- | ------------------------------------ | ------------------------------------------ | ------------------------------- | ------------------------ |
| /data/Users      | Return list of users with all fields | Create a new user                          | Create or Update user           | Method not allowed (405) |
| /data/Users/123  | Return specific user with all fields | Method not allowed (405)                   | Update specific user            | Delete specific user     |
| /query/Users     | Method not allowed (405)             | Return list of users with specified fields | Method not allowed (405)        | Method not allowed (405) |
| /query/Users/123 | Method not allowed (405)             | Return specific user with specified fields | Method not allowed (405)        | Method not allowed (405) |


**Samples**

[Query](../rest_ref/query.md)

[Mutation](../rest_ref/mutation.md)



### HTTP Response codes 

**2xx Success**

200 OK: Returned by a successful GET, PUT, POST or DELETE operation.

201 Created: Response for a successful resource creation by a POST request.

204 No content: Response for No data while searching for single item by Unique Key

**4xx Client Errors**

400 Bad Request: When an HTTP request body can’t be parsed. For example, if an API is expecting a body in a JSON format for a POST request, but the body of the request is malformed.

401 Unauthorized: Authentication is unsuccessful (or credentials have not been provided) while accessing the API.

403 Forbidden: If a user is not Authorized to perform an action although authentication information is correct.

404 Not Found: If the requested resource is not available on the server.(GET, PUT, DELETE) 

405 Method Not Allowed: If the user is trying to violate an API contract, for example, trying to update a resource by using a POST method.

**5xx Server Errors**

These errors occur due to server failures or issues with the underlying infrastructure.


#### REST API - System Configuration

The developer can create tables using their prefered database client such as heidisql or mysql workbench.

The tables should be created with proper primary key, foreign key references. It is recommended to have auto-increment primary keys. For more information refer to the [Data Model](datamodel.md) guide. 

After creating the tables, invoke the db synchronization action by the URL 

```
URL - http://{host}/palmyra/v1/{database}/dev/db/sync
Method - post
```

On successful synchronization 200 response code will be received.



After synchronization, the configuration tables (zit_xxx) will be populated with schema metadata. The administrator can modify the field  'zit_ci_type.name'  to change the type name. similarly 'zit_ci_fields.attribute' field can be modified to change the field names of the generated types. 



All the tables can be viewed in the below endpoint 

```
URL - http://{host}/palmyra/v1/{database}/type
Method - post
```



The table details can be viewed in the below endpoint 

```
URL - http://{host}/palmyra/v1/{database}/type/{type}
Method - post
```



Sample URL - http://{host}/palmyra/v1/{database}/type/country
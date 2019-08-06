Welcome to the palmyra wiki!



## Developer Reference

#### REST API - CRUDS  reference

Resource vs HTTP Methods

| Resource         | GET                                  | POST                                       | PUT                             | DELETE                   |
| ---------------- | ------------------------------------ | ------------------------------------------ | ------------------------------- | ------------------------ |
| /data/Users      | Return list of users with all fields | Create a new user                          | Create or Update user           | Method not allowed (405) |
| /data/Users/123  | Return specific user with all fields | Method not allowed (405)                   | Update specific user            | Delete specific user     |
| /query/Users     | Method not allowed (405)             | Return list of users with specified fields | Method not allowed (405)        | Method not allowed (405) |
| /query/Users/123 | Method not allowed (405)             | Return specific user with specified fields | Method not allowed (405)        | Method not allowed (405) |
| /bulk/Users      | Method not allowed (405)             | Create multiple users                      | Create or Update multiple users | Method not allowed (405) |

GET - /Users  also can be used to search records by providing attributes in the URL. But this will be a limited search functionality. flexible query options are as provided with the /query/Users.



#### Samples

[Query](DML/query)

[Mutation](DML/mutation)



### Standard HTTP codes 

##### 2xx Success

200 OK: Returned by a successful GET, PUT, POST or DELETE operation.

201 Created: Response for a successful resource creation by a POST request.

3xx Redirection

304 Not Modified: 

##### 4xx Client Errors

400 Bad Request: When an HTTP request body can’t be parsed. For example, if an API is expecting a body in a JSON format for a POST request, but the body of the request is malformed.

401 Unauthorized: Authentication is unsuccessful (or credentials have not been provided) while accessing the API.

403 Forbidden: If a user is not Authorized to perform an action although authentication information is correct.

404 Not Found: If the requested resource is not available on the server.(GET, PUT, DELETE) 

405 Method Not Allowed: If the user is trying to violate an API contract, for example, trying to update a resource by using a POST method.

##### 5xx Server Errors

These errors occur due to server failures or issues with the underlying infrastructure.



## Admin Reference

#### REST API - CRUDS  reference

The developer can create tables using their prefered database client such as heidisql or mysql workbench.

The tables should be created with proper primary key, foreign key references. It is recommended to have auto-increment primary keys. For more information refer to the [Concepts](Concepts) guide. 

After creating the tables, invoke the db synchronization action by the URL 

```
URL - http://{host}/palmyra/v1/{database}/dev/db/sync
Method - post
```

On successful synchronization 200 response code will be received.



After synchronization, the configuration tables (zit_xxx) will be populated with schema metadata. The administrator can modify the field  'zit_ci_type.name'  to change the type name. similarly 'zit_ci_fields.attribute' field can be modified to change the field names of the generated types. 
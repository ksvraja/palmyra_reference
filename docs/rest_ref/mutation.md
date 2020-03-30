
## Create new record

**creating individual record**

```
endpoint 	- https://{server-url}/palmyra/api/v1/{database}/data/{type}
method 		- POST
```

Request Body

```json
{
    "name" : "selvi",
    "dob" : "18-02-2000",
    "join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```



On successful creation, http status code - 200 will be returned

response format will be as below providing all the attributes of the given type.

```json
{
    "id" : 20,
    "name" : "selvi",
    "dob" : "18-02-2000",
    "join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```

*Note the 'id' of the record is also returned with the response*




**Creating record with relations**

While creating a record, the children of the record also can be created on the same request. 

Along with the fields of the record, provide the child records as below (as Array).

```
endpoint 	- https://{server-url}/palmyra/api/v1/{database}/data/{type}
method 		- POST
```

Request Body

```json
{
    "name" : "selvi",
    "dob" : "18-02-2000",
    "join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai", 
    "marks" : [
        {
            "month" : "july",
            "english" : 70,
            "tamil" : 82,
            "maths" : 72,
            "science" : 78
        }
    ]
}
```



On successful creation, http status code - 201 will be returned

response format will be as below providing all the attributes of the given type. Please note that the children records are not returned.

```json
{
    "id" : 20,
    "name" : "selvi",
    "dob" : "18-02-2000",
    "join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```

*Note the 'id' of the record is also returned with the response*





## Update record

**update single record**

```
endpoint 	- https://{server-url}/palmyra/api/v1/{database}/data/{type}/20
method 		- PUT
```

Request Body

```json
{
	"name" : "selvi",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```



On successful updation, http status code - 200 will be returned

response format will be as below providing all the attributes of the given type.

```json
{
    "id" : 20
	"name" : "selvi",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```

*Note the 'id' of the record is also returned with the response*

if the record is not found, http status code - 404 will be returned



**Update record and relations**

While Updating a record, the child records also can be created, updated or deleted on the same request. 

Along with the fields of the record, provide the child records as below (as Array).

```
endpoint 	- https://{server-url}:8080/palmyora/{database}/data/{type}/20
method 		- PUT
```

Request Body

```json
{
	"name" : "selvi",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai", 
    "marks" : [
        {
            "month" : "july",
        	"english" : 70,
        	"tamil" : 82,
        	"maths" : 72,
        	"science" : 78, 
            "_meta" :{
                action:"delete"
            }
        }
    ]
}
```

If no 'action' is specified in the request, 



On successful creation, http status code - 201 will be returned

response format will be as below providing all the attributes of the given type. Please note that the children records are not returned.

```json
{
    "id" : 20
	"name" : "selvi",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```

*Note the 'id' of the record is also returned with the response*





## Delete record

**Delete single record by id**

```
endpoint 	- https://{server-url}/palmyra/api/v1/{database}/data/{type}/20
method 		- DELETE
```

This method does not need a request body. 



On successful deletion, http status code - 200 will be returned



if the record is not found or already deleted, http status code - 404 will be returned

if the record has child records, the record will not be deleted and will return http status code - 304



**Delete record with children**

To delete a record with children, provide the meta information as below.

```
endpoint 	- https://{server-url}:8080/palmyora/{database}/data/{type}/20?mode=recursive&depth=1
method 		- DELETE
```



*Optional Request Body --  to be revisited*

```json
{
    "code" : "ST20420"
    "_meta" :{
        action:"delete"
        mode : "recursive"
        depth : "1"
    }
 }
```

On successful deletion, http status code - 201 will be returned.
if the primary record is not found, http status code - 304 will be returned.

for one-to-many relationship - The primary record will be deleted, and child records might be deleted or the primary record reference set to null, depends on the configuration of the system.

for many-to-many relationship - only the link will be removed between parent and child.



***caution:*** The default depth is 1 - the primary and the next level referencing child records are deleted. The depth should be modified based on the data model impact of the system.
## Query for the data

```
endpoint 	- https://{server-url}:8080/palmyora/{database}/query/{type}
method 		- POST
```

type - table or pre-defined object to be queried 



Request Body

```json
{
 	"fields" : [ "name", "dob", "join_date" ],	
	"orderBy" : [ "+name", "-dob" ],	
	"criteria" : {
		"attribute" : "condition"
	},
	"groupBy" : [
		{
			"attribute" : "pricing",
			"function" : "sum",
			"label" : "group_data_label"
		}
	],
	"offset" : 0,
	"limit" : 25,
    "total" : false
}
```



Parameter details

| Parameter   | required | notes                                                        |
| ----------- | -------- | :----------------------------------------------------------- |
| fields      | no       | list of fields to be retrieved. if the list is not provided, all the fields in the type will be returned. |
| orderBy     | no       | ascending order (+) or descending order (-) of the given attribute. |
| criteria    | no       | filtering criteria to be applied. for more details, check the criteria section. |
| groupBy     | no       | grouping of the information by the given attribute and aggregate function provided.  check the group section for supported aggregate functions.  Label the resulting data and can be used as 'attribute' |
| offset      | yes      | pagination starting row                                      |
| limit       | yes      | number of records to be retrieved                            |
| meta-header | no       | default to false,  explained as below.                       |
| total       | no       | default to false,  If true, will provide the total record counts for the query. |



The response data will be provided as below. 

```json
{
	"result" : [{
		"name" : "senthil",
        "dob" : "18-02-2000",
        "join_date" : "18-02-2018"
	},{
		"name" : "selvi",
        "dob" : "23-07-2000",
        "join_date" : "18-02-2018"
	}],
    "count" : 15,
    "offset" : 30,
    "total" :200    
}
```







## Get the result data as List

If the data should be retrieved as List of Tuples and does not require the above structure, query the data with the URL  as below. (adding 'list' to the URL) 
```
endpoint 	- https://{server-url}:8080/palmyora/{database}/query/{type}/list
method 		- POST
```

The response data will be as below. 



```json
[
	{
		"name" : "senthil",
		"dob" : "18-02-2000",
		"join_date" : "18-02-2018"
	},
	{
		"name" : "selvi",
		"dob" : "23-07-2000",
		"join_date" : "18-02-2018"
	}
]
```



If no data found matching the criteria.  an empty array will be returned.



```json
[]
```





## Query for the Single record

```
endpoint 	- https://{server-url}:8080/palmyora/{database}/query/{type}/{id}
method 		- POST
```

type - table or pre-defined object to be queried 



Request Body (can be empty)

```json
{
 	"fields" : [ "name", "dob", "join_date" ]
}
```



Parameter details

| Parameter   | required | notes                                                        |
| ----------- | -------- | :----------------------------------------------------------- |
| fields      | no       | list of fields to be retrieved. if the list is not provided, all the fields in the type will be returned. |



The response data will be provided as below. 

```json
{
	"name" : "senthil",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018"
}
```



## Query with GET method

##### Read - Get single record by known id

```
endpoint 	- https://{server-url}:8080/palmyora/{database}/data/{type}/{id}
method 		- GET
```

type - table or pre-defined object to be queried
id - the identifier (primary key) of the record.

response format will be as below providing all the fields of the given type.

```json
{
	"name" : "selvi",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018", 
    "father" : "madhan",
    "city" : "chennai"
}
```

if the record is not found, http status code - 404 will be returned



##### Read - Get single record by known id with specific fields

```
endpoint 	- https://{serverurl}:8080/palmyora/{database}/data/{type}/{id}/fields
method 		- POST
```

id - the identifier (primary key) of the record.

Request Body

```json
{
 	"fields" : [ "name", "dob", "join_date" ]
}
```



response format will be as below providing all the fields of the given type.

```json
{
	"name" : "selvi",
	"dob" : "18-02-2000",
	"join_date" : "18-02-2018"
}
```




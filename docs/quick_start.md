## Pre-requisites 
* MariaDB 10.3.x or later / MySQL server 
* Java 8 

## Download Palmyra 

Download the release package from the GitHub repository. 

[Download Palmyra](https://github.com/palmyra-io/palmyra/releases)

The release package contains the folders/files as below. Extract the package in a directory.

* start_palmyra.bat/sh -   Executes java command to start the server
* resources – contains the database configuration file – spring.properties
* palmyra – contains the application war and server runtime (jetty)
* mysql – contains the SQL scripts for database setup.

## Setup

Step 1 - Initializing the database.   
The developer can setup a sample database, using – ‘mysql/SampleDB.sql’. or
Add Palmyra base tables to your existing schema using ‘mysql/create_base_tables.sql’

Step2 – Configure the connection parameters.  
	Specify the database IP, user, password and schema details in the file 
‘resources/spring.properties’

Step3 – Start the server  
 Windows - execute the command ‘start_palmyra.bat’.  
for Linux -  execute the command ‘start_palmyra.sh’. 

Step4 – synchronize the server with your database  
 http://localhost:8080/palmyra/v1/palmyra/dev/db/sync  
 
if you have provided a different schema name other than ‘palmyra’, change the URL as below.  http://localhost:8080/palmyra/v1/{schema}/dev/db/sync	


## Access the API
To view the list of tables available in the API

http://localhost:8080/palmyra/v1/palmyra/type

To view the particular table details

http://localhost:8080/palmyra/v1/palmyra/type/{table_name}

Refer to the API [quick reference](concepts/crud.md) or detailed references on [Query](rest_ref/query.md) and [Mutation](rest_ref/mutation.md)
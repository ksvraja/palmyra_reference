# palmyra
Palmyra provides Instant JSON REST API to access the data in the MySQL database. It automates the task of CRUD operations, while freeing the developer from Database transactions, concurrency, basic validations etc., 

Added with the power of groovy scripting, the developer can also add business rules while performing CRUD operations.


## Pre-requisites 
* MariaDB 10.2 / MySQL server 
* Java 8 

## Installation 
Download the packaged release file from release section. Extract the zip file in the local folder. The extracted files should contain the folders/files as below.

* start_palmyra.bat/sh -   Executes java command to start the server
* resources – contains the database configuration file – spring.properties
* palmyra – contains the application war and server runtime (jetty)
* mysql – contains the SQL scripts for database setup.



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

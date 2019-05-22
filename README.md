# Service Interface for Vehicle Use
Service interface for vehicle use (SIVU) is a data specification for free-floating vehicles providers REST API. 
SIVU must be used by all operators that signed the charter "vélo/2RM libre-service" of the city of Paris. 

## Contents
+ [Charter Specification](#charter-specification)
+ [API Specification](#api-specification)
+ [Data Specification](#data-specification)

## Charter Specification
The operators that signed the charter of the city of Paris about vehicles in free-floating committed themselves to provide an authenticated REST API that provides their vehicle fleet information. 
This charter commits the city of Paris to not share this information and to use it in a specific field of analysis. 

## API Specification
The API has to be an HTTP REST API that gives a total access to the whole vehicle fleet information as specified in [data specification](#data-specification). This information has to be in real time or at regular interval of 3 hours starting midnight. The login/pass or 
the token must be given by the operator to the city of Paris. 
The response returns by the API has to be a JSON or XML file without pagination. 

### HTTP response status code
If an error appears, the API has to return a status code as follows : 

| Status code  |       Description       |
| -----------  |  ---------------------  |
|     200      |   Successful request    |
|     400      |   Bad request           |
|     401      |   Unauthorized          |
|     403      |   Forbidden             |
|     404      |   Not Found             |
|     500      |   Internal Servor Error |
|     503      |  Service Unavailable    |


## Data Specification

|      Attribute    |    Value Type   |  
| :---------------- |:-------------:  | 
| operator_name     |    String       |   
| vehicle_id        |    UUID         |   
| marker_time       |    Timestamp    |   
| longitude-x       |    Float        |  
| latitude-y        |    Float        |   
| vehicle_type      |    String       |   
| vehicle_activity  |    String       |  

### Vehicle_type

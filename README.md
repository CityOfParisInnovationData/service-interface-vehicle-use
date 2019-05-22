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
the token must be given by the operator to the city of Paris.<br>
The response returns by the API has to be a JSON or XML file **without pagination**. 

### Example
If the city of Paris makes an HTTP GET request to, let's say XYZ's SIVU API returning JSON file, every JSON object from the response file must be as follows :

```json
  {
    "operator_name": "XYZ",
    "marker_time": "20190622-12:00:00",
    "vehicle_id": 00001,
    "longitude-x": 2.357163,
    "latitude-y": 48.822855,
    "vehicle_activity": "parking",
    "vehicle_type": "scooter"
  }
```

### HTTP response status code
The SIVU API has to return a status code as follows : 

| Status code  |       Description       |
| -----------  |  ---------------------  |
|     200      |   Successful request    |
|     400      |   Bad request           |
|     401      |   Unauthorized          |
|     403      |   Forbidden             |
|     404      |   Not Found             |
|     500      |   Internal Servor Error |
|     503      |   Service Unavailable   |


## Data Specification

|      Attribute    |    Value Type   |  
| :---------------- |:-------------:  | 
| operator_name     |    String       |   
| vehicle_id        |    UUID         |   
| marker_time       |    ISO 8601     |   
| longitude-x       |    Float        |  
| latitude-y        |    Float        |   
| vehicle_type      |    String       |   
| vehicle_activity  |    String       |  

### Vehicle_type

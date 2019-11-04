# Service Interface for Vehicle Use
Service interface for vehicle use (SIVU) is a data specification for free-floating vehicles providers REST API. 
SIVU must be used by all operators that signed the charter "vélo/2RM libre-service" of the city of Paris. 

## Contents
+ [Charter Specification](#charter-specification)
+ [Vehicle Monitoring](#vehicle-monitoring)
+ [Data Specification](#data-specification)
+ [Data Validation](#data-validation)

## Charter Specification
The operators that signed the charter of the city of Paris about vehicles in free-floating committed themselves to provide an authenticated REST API that provides their vehicle fleet information. 
This charter commits the city of Paris to not share this information and to use it in a specific field of analysis. 

## Vehicle Monitoring

### API Specification
The SIVU API is an HTTP REST API that gives a total access to the whole vehicle fleet information as specified in [data specification](#data-specification). This information has to be in real time or at regular interval of 3 hours starting midnight. The login/pass or 
the token must be given by the operator to the city of Paris.<br>
The response returns by the API is a JSON file **without pagination**. 

### Schema
Every JSON object from the response file have the following schema :

```json
  {
    "operator_name": "XYZ",
    "marker_time": "20190411T12:00:00+01:00",
    "vehicle_id": 00001,
    "longitude-x": 2.357163,
    "latitude-y": 48.822855,
    "vehicle_activity": "parking",
    "vehicle_type": "scooter"
  }
```

### HTTP response status code
The SIVU API returns a status code as specified in HTTP/1.1 standard ([RFC 7231](https://tools.ietf.org/html/rfc7231)) : 

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
Requests are made with HTTP GET and the **vehicle-monitoring** endpoint. 

|      Attribute    |    Value Type   |  
| :---------------- |:-------------:  | 
| operator_name     |    String       |   
| vehicle_id        |    UUID         |   
| marker_time       |    ISO 8601     |   
| longitude-x       |    Float        |  
| latitude-y        |    Float        |   
| vehicle_type      |    Enum         |   
| vehicle_activity  |    Enum         |  

### Vehicle_type

|vehicle_type|
| ---------- |
| [scooter](https://en.wikipedia.org/wiki/Motorized_scooter)    |
| [motorscoot](https://en.wikipedia.org/wiki/Scooter_(motorcycle)) |
| [bike](https://en.wikipedia.org/wiki/Bicycle)       |

### Vehicle_activity

| vehicle_activity |              description                   |   
| ---------------- |  --------------------------------------    |  
| parking          | a functional vehicule                      |
| riding           | a vehicle is currently used by a customer  |
| nok              | not ok, a vehicle is not functional on public space<sup>*</sup>|
| removed          | a vehicule is removed from public space |

<sup>*</sup>All vehicles in maintenance in private storage space does not appear. 

## Data Validation

Before sending, operators should validate their data with an application like [goodtables.io](https://goodtables.io/). To do this, they will use the table schema [schema.json](https://github.com/CityOfParisInnovationData/service-interface-vehicle-use/edit/master/schema.json). 


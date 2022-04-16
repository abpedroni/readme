# Kraft Heinz - **ServiceNow.WebApi**
 <!--ts-->
 * [Introduction](#introduction)
 * [Requirements](#requirements)
 * [Building and running](#building)
   * [Dockerfile](#docker)
   * [Docker compose](#docker-compose)
   * [Scripts](#scripts)
 * [Endpoints](#endpoints)
 * [Diagram](#diagram)

<!--te-->

## **Introduction**
The Service Now API provides customized endpoints to be consumed by other Kraft Heinz apps
This Web Api provides the functionality:
- Search aged incident between 10 and 14 days; Update aged incident with a friendly reminder comment.

## **Requirements**

- .NET Core 3.1
- Visual studio 2019+ or Visual studio Code

## **Building**

### Local

Building locally can be done using the command `dotnet build` from the `src` folder of the project. To run the project simply run the command `dotnet run`. The API can be accessed on port `5000` for HTTPS.

Example: `dotnet run -p ServiceNow.WebApi/ServiceNow.WebApi.csproj`

http://localhost:5000/index.html

### **Docker**

Build the image by running the command `docker build -t kraftheinz-servicenow-webapi:v1 .`. Run the container on port `5000` with the command `docker run -it -p 5000:80 kraftheinz-servicenow-webapi:v1`.

> **Note**:
>
> 1. Remember the configured settings when the app was created.
> 2. The docker name must be lower case for it is case sensitive.
> 3. The default port is 80, make sure the port is available for use;

###  **Docker-compose**

At the `src` folder, run the command `docker-compose up`.

> **Note**:
>
> 1. There is a _.env_ file that handles the IMAGE_TAG and IMAGE_REPOSITORY variables, responsible for tagging and the docker's image repository source/path respectively, where the dockercompose will check whether the file exists and use it.
> 2. For local versioning of the container image, adjust the IMAGE_TAG property.

### **Scripts**

At the root folder, the file:
* `build.sh` will build, publish, check the docker compose config file, and generate a new image (check the name of image and tag version inside `.env` file in `src` folder).
* `run.sh` will do the same as the previous command and will execute the container at the link `http://localhost:80/`.


### **Endpoints**

1. Incidents Controller

```mermaid
graph LR
    ServiceNow:::someclass --> /incidents/filter-rules/aged10between14
    /incidents/filter-rules/aged10between14 --> GET
    
    ServiceNow:::someclass --> /incidents/id/comments/aged-fixed-comment/
    /incidents/id/comments/aged-fixed-comment/ -- id--> PUT
    classDef someclass fill:#f96;
```

### **Diagram**

Incidents search request sequence below is an example of a systemic call where the intent is to search for the Incidents.
  

```mermaid

sequenceDiagram

ExternalRequest->>WebApi: GET/incidents/filter-rules/aged10between14

WebApi ->>+ Application: Try to get aged incidents

ServiceNowAdapter-->>Application: External call to get aged incidents Between 10 and 14

Application-->>-WebApi: Returning Aged Incidents Emails

opt Possible HTTP Status codes
	WebApi-->> ExternalRequest: 200 - Return list of aged incidents email
	WebApi-->> ExternalRequest: 400 - Aged incident email not found
	WebApi-->> ExternalRequest: 500 - Internal Error Server
end

ExternalRequest->>WebApi: POST/incidents/{id}/comments/aged-fixed-comment/

WebApi ->>+ Application: Try to update incident by ID

ServiceNowAdapter-->>Application: External call to create a new comment at incident

Application-->>-WebApi: returning status code

opt Possible HTTP Status codes
	WebApi-->> ExternalRequest: 200 - Created a new comment at incident.
	WebApi-->> ExternalRequest: 400 - Some incorrect required fields
	WebApi-->> ExternalRequest: 500 - Internal Error Server
end
```

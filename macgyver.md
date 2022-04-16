# MacGyver.WebApi

* [What is MacGyver.WebApi?](#what-is)
* [Dependencies](#dependencies)
* [Creating your first project](#creating-your-first-project)
  * [Setup nuget source](#nuget-source-configuration)
  * [Install .Net Core template](#install-net-core-template)
  * [Create using Visual Studio](#create-using-visual-studio)
  * [Create using .Net Core CLI](#create-using-net-core-cli)
  * [Template commands](#template-commands-configuration)
  * [JSON configurations](#json-appsettings-config-file)
  * [Building and running](#building-and-running-your-first-project)
  * [Uninstall template](#uninstall-macgyver-template)
* [Solution Structure](#solution-structure)
  * [Folder structure](#folder-structure)
  * [References structure](#references-structure)
  * [Endpoints structure](#endpoints-structure)
* Diagrams
  * [Movie search](#movie-search-request-sequence-diagram)
* [FAQ](#faq)

## **What is the MacGyver.WebApi?**

Based on MacGyver character with his genius and expert levels, we were inspired putting inside this web api template preparing it with some base and standardized concepts ready to use and run for every developer.

The MacGyver is an architectural software model for .NET Core projects based on the [Hexagonal architecture](https://alistair.cockburn.us/hexagonal-architecture/) supporting and helping shiny devs and enthusiasts with base standarts implementation as nuget package and the most powerfull, its configurable throught a dotnet web api template.

This model allows for several topic standards to be applied, such as:

* Configuration (Appsettings, KeyVault, and AppConfiguration)
* Swagger with Open API
* Logging
* Error Handling
* Caching
* JSON Serializer
* Feature Management
* Metrics
* Authentication

> **Extra readings:**
>
> 1. [Ports](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/#ports)
> 2. [Primary or Driving Adapters](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/#primary-or-driving-adapters)
> 3. [Secondary or Driven Adapters](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/#secondary-or-driving-adapters)
> 4. [Inversion of control](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/#inversion-of-control)
> 5. [Application Layer](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/#application-layer)
> 6. [Domain Layer](https://herbertograca.com/2017/11/16/explicit-architecture-01-ddd-hexagonal-onion-clean-cqrs-how-i-put-it-all-together/#domain-layer)
> 7. [Domain-Driven Design (herbertograca)](https://herbertograca.com/2017/09/07/domain-driven-design/)
> 8. [Domain Driven Design (martinfowler.com)](https://martinfowler.com/bliki/DomainDrivenDesign.html)

## **Dependencies**

* [.NET SDK 3.1 or later](https://dotnet.microsoft.com/download/dotnet/3.1)
* [NuGet CLI 5.1 or later](https://www.nuget.org/downloads)
* Visual studio 2019+

## **Creating your first project**

### Nuget source configuration

The first step for creating a project is to setup the private NuGet package repository path. To achieve that, the private GitLab project URL must be added to the NuGet resource source by executing the following command.

```bash
dotnet nuget add source "https://nuget.pkg.github.com/stefanini-applications/index.json" \
  --name github \
  --username sophie-na \
  --password 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 \
  --store-password-in-clear-text
```

Verify if the new nuget source was added using the command `dotnet nuget list source`. You should be able to see the `github` source.

After the NuGet repository source was setup, there are two ways of creating a project based on the web api template:

* [Visual Studio Template](#visual-studio-template)
* [.Net Core Template](#.net-core-template)

> **Note**:
>
> * The user and access token were created with *read only* access.
> * Reference command: [dotnet nuget add source - .NET CLI](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-nuget-add-source)

### Install .Net Core template

Run the following command in terminal (bash, powershell, cmd):

```bash
dotnet new -i Macgyver.WebApi
```

> **Note**: Please check the [FAQ](#faq) if something goes wrong.

### Create using Visual Studio

1. Open Visual Studio;
2. Access *menu File > New > Project*;
3. Search for `Macgyver`, and click on *Next*;
4. Provide the project name, a path, and then click on *Next*;
5. Configuration fields will be shown such as *logging, caching, configuration source, adapter example, among others*. Select the desired options and click on *Create*

### Create using .Net Core CLI

Run the following command:

```bash
#Creating a webapi project with the name cliente
dotnet new macgyverwebapi \
   --name=cliente \
   --adapter-example MongoDb \
   --cache-type Memory \
   --log-type Stdout 
```

After running the command the files should be located on the folder:

![Result 1](docs/images/command1_folder_result.png)

> **Note**:
>
> * To know more about all the available commands access the [available table](#template-commands-configuration)
> * Please check the [FAQ](#faq) if something goes wrong.

### Template commands configuration

The following table contains all the available commands to setup the webapi based on the **Macgyver** template.

| Command                                         | Description                                                  |
| ----------------------------------------------- | ------------------------------------------------------------ |
| -P\|--ProjectName                               | Project name<br/>string - Optional<br/>Default: Macgyver     |
| -lt\|--log-type                                 | Sets the log type the app will be using to log.<br/>    Stdout                 - Standard console output<br/>    File                   - File<br/>    Seq                    - Centralized log<br/>    ApplicationInsights    - Azure application insights<br/>    MongoDb                - Mongo database<br/>Default: Stdout |
| -lmu--log-mongodb-url                           | Sets the mongodb database url.<br/>string - Optional         |
| -lmd--log-mongodb-dbname                        | Sets the mongodb data base name.<br/>string - Optional<br/>Default: local |
| -lmc--log-mongodb-collection                    | Sets the mongodb collection name<br/>string - Optional<br/>Default: log |
| -lmst--log-mongodb-selection-timeout            | Sets the mongodb selection timeout that expires after attempts to connect to it.<br/>string - Optional<br/>Default: 10 |
| -lsu--log-seq-url                               | Sets the seq url.<br/>string - Optional<br/>Default: http://localhost:5341/ |
| -lsk--log-seq-key                               | Sets the seq api key.<br/>string - Optional<br/>Default: null |
| -laik--log-app-insights-key                     | Sets the application insights instrumentation key.<br/>string - Optional |
| -laid--log-app-insights-disable                 | Gets or sets the application insights telemetry.<br/>bool - Optional<br/>Default: False |
| -laitt--log-app-insights-telemetry-type         | Sets the application insights telemetry type.<br/>    Traces    - Represents printf style trace statements that are text-searched.<br/>    Event     - Represent an event that occurred in your application.<br/>Default: Traces |
| -ct--cache-type                                 | Gets or sets the type of caching used for distributed caching in app.<br/>    Memory       - Use the app memory to cache values.<br/>    SqlServer    - Use the Sql Server to cache values.<br/>    Redis        - Use the redis to cache values.<br/>Default: Memory |
| -csc--cache-sql-connectionstring                | Sets the sqlserver connection string.<br/>string - Optional  |
| -css--cache-sql-schema                          | Sets the sqlserver schema name.<br/>string - Optional<br/>Default: dbo |
| -cst--cache-sql-table                           | Sets the sqlserver table name.<br/>string - Optional<br/>Default: Caching |
| -crc--cache-redis-connection                    | Sets the redis configuration.<br/>string - Optional<br/>Default: localhost:6379 |
| -cri--cache-redis-instancename                  | Sets the redis instance name.<br/>string - Optional<br/>Default: cache- |
| -ceis--convert-enum-in-string                   | Enable enum to be converted in string.<br/>bool - Optional<br/>Default: False |
| -jds--json-default-serializer                   | Sets the type of serialization who manipulates the json.<br/>    Newtonsoft    - Newtonsoft library<br/>    Standard      - Standard System.Text.Json<br/>Default: Newtonsoft |
| -sst--swagger-security-type                     | Sets swagger security type.<br/>    None     - No authentication is required<br/>    Jwt      - Json Web Token<br/>    Basic    - Basic user and password<br/>Default: None |
| -wcs--webapi-configuration-source               | Sets where the app will read the configuration.<br/>    AppSettings              - App settings file.<br/>    AzureAppConfiguration    - Azure App Configuration.<br/>Default: AppSettings |
| -ehc--enable-health-checks                      | Enable expose routes /readyz, /livez and /hc-ui<br/>bool - Optional<br/>Default: True |
| -efm--enable-feature-management                 | Enable feature toggles use. It will dependend on the configuration source.<br/>bool - Optional<br/>Default: True |
| -aace--azure-app-configuration-endpoint         | Sets the azure app configuration endpoint.<br/>string - Optional |
| -uk--use-keyvault                               | Sets whether the application will use KeyVault for sensitive data.<br/>bool - Optional<br/>Default: False |
| -ku--keyvault-url                               | Sets the azure key vault uri.<br/>string - Optional          |
| -kc--keyvault-clientid                          | Sets the azure key vault client id.<br/>string - Optional    |
| -kec--keyvault-clientsecret                     | Sets the azure key vault client secret.<br/>string - Optional |
| -em--enable-metrics                             | Sets whether the application will work with metrics.<br/>bool - Optional<br/>Default: False |
| -emo--enable-metrics-opentelemetry              | Enable open telemetry output.<br/>bool - Optional<br/>Default: False |
| -moe--metrics-opentelemetry-exporter            | Sets the azure key vault client id.<br/>    Console    - Console output as default.<br/>    Zipkins    - Zipkins distributed tracing.<br/>Default: Console |
| -mzh--metrics-zipkins-hostname                  | Sets kipkins hostname.<br/>string - Optional<br/>Default: localhost |
| -emp--enable-metrics-prometheus                 | Enable create route /metris used by prometheus.<br/>bool - Optional<br/>Default: False |
| -emai--enable-metrics-app-insights              | Enable send metrics to application insights.<br/>bool - Optional<br/>Default: True |
| -maik--metrics-app-insights-key                 | Sets the instrumantation key to send metrics to application insights.<br/>string - Optional |
| -emeka--enable-metrics-enricher-k8s-appinsights | Sets the enricher logges for k8s contexts properties in application insights.<br/>bool - Optional<br/>Default: False |
| -ae--adapter-example                            | Sets which adapter will be used as an example.<br/>    ServiceNow    - Adapter to integrate with service now api.<br/>    MongoDb       - Adapter to integrate with mongodb database.<br/>    SqlServer       - Adapter to integrate with sql server database.<br/>Default: ServiceNow |

### JSON Appsettings Config File

Below are all the available configurations (Cache, swagger, JSON serializer, app configuration, metrics, etc) used for the application to suit the proposed scenario.

```json
{
    "Serilog": {
        "MinimumLevel": {
            "Default": "Warning",
            "Override": {
                //In this example, all log emmitting namespaces present in Macgyver.WebApi with at least Debug level will be logged.
                "Macgyver.WebApi": "Debug", //Debug, Information, Warning, Trace, Error
                "Microsoft": "Warning",
                "Microsoft.Hosting.Lifetime": "Information",
                "System": "Warning"
            }
        }
    },
    "WebApiSettings": {
        "ConfigurationSource": "Possible values: AppSettings | AzureAppConfiguration",
        "EnableHealthChecks": "Possible values: True, False",
        "EnableFeatureManagement": "Possible values: True, False",
        //This property is used only when ConfigurationSource = 'AzureAppConfiguration'
        "AzureAppConfigurationEndpoint": "Azure Endpoint of AppConfiguration"
    },
    "UseKeyVault": "Possible values: True, False",

    //This property is used only when UseKeyVault = 'True'
    "AzureKeyVaultSettings": {
        "VaultUri": "Azure Keyvault Uri",
        "ClientId": "Azure Keyvault ClientId",
        "ClientSecret": "Azure Keyvault Secret"
    },

    //All properties above are used only when ConfigurationSource == 'AppSettings'

    //Configure web api logging
    "LoggingSettings": {
        "LoggingType": "Possible values: Stdout, File, Seq, ApplicationInsights, MongoDb",

        //This property is used only when LogType = 'MongoDb'
        "LoggingMongoDbDatabaseUrl": "Mongodb database url",
        "LoggingMongoDbDatabaseName": "Mongodb database name",
        "LoggingMongoDbCollectionName": "Mongodb database collection name",
        "LoggingMongoDbServerSelectionTimeoutInSeconds": "Mongodb database timeout to wait for connection",

        //This property is used only when LogType = 'Seq'
        "LoggingSeqServerUrl": "Seq url",
        "LoggingSeqApiKey": "Seq api key (Optional)",

        //This property is used only when LogType = 'ApplicationInsights'
        "LoggingAppInsightsInstrumentationKey": "Azure App Insights Instrumentation key",
        "LoggingAppInsightsDisableTelemetry": "Possible values: True, False",
        "LoggingAppInsightsTelemetryConverterType": "Possible values: Traces, Events"
    },
   
    //Exception handler settings
    "ExceptionHandlerSettings": {
        "EnableSophieErrorBaseRespose": "Possible values: True, False"
    },
    
    //Web api cache settings configurations
    "DistributedCacheSettings": {
        "CacheStorageType": "Possible values: SqlServer, Redis, Memory",

        //This property is used only when CacheStorageType == 'SqlServer'
        "CacheSqlConnectionString": "Sql server connection string",
        "CacheSqlSchemaName": "Sql server schema name",
        "CacheSqlTableName": "Sql server table name",

        //This property is used only when CacheStorageType == 'Redis'
        "CacheRedisConfiguration": "Redis connection configuration",
        "CacheRedisInstanceName": "Redis instance name"
    },

    //Json serializer settings configurations
    "JsonSettings": {
        "EnableStringEnumConverter": "Possible values: True, False",
        "DefaultJsonSerializer": "Possible values: Standard, Newtonsoft"
    },

    //Web Api Swagger options configurations
    "SwaggerSettings": {
        "SecurityType": "Possible values: None, Jwt, Basic"
    },

    //This property is used only when UseMetrics = 'True'
    //Web Api Metrics configurations
    "MetricsSettings": {
        "MetricsEnableOpenTelemetry": "Possible values: True, False",
        "MetricsOpenTelemetryExporter": "Possible values: Console, Zipkins",
        "MetricsZipkinHostName": "Zipkins hostname",
        "MetricsEnablePrometheus": "Possible values: True, False",
        "MetricsEnableAppInsights": "Possible values: True, False",
        "MetricsAppInsightsInstrumentationKey": "Azure App Insights Instrumantation key",
        "MetricsEnableAppInsightsK8sEnricher": "Possible values: True, False"
    },

    //ServiceNow Adapter Configuration
    "ServiceNowAdapterConfiguration": {
        "UrlBase": "https://www.service-now.com/api/",
        "User": "fakeuser",
        "Password": "fakepassword",
        "UseProxy": "false",
        "WebProxy": "http://172.17.16.129:8080",
        "CredentialType": "Network"
    },

    //Tmdb Adapter Configuration
    "TmdbAdapterConfiguration": {
        "TmdbApiUrlBase": "https://api.themoviedb.org/3",
        "TmdbApiKey": "1f54bd990f1cdfb230adb312546d765d",
        "TimeCacheInSeconds": 30,
        "Language": "pt-BR"
    },

    //MongoDb Adapter Configuration
    "MongoAdapterConfiguration": {
        "DatabaseUrl": "mongodb://localhost:27017",
        "DatabaseName": "local",
        "CollectionName": "tmdb",
        "Proxy": ""
    },

    //SqlServer Adapter Configuration
    "SqlServerAdapterConfiguration": {
        "SqlConnectionString": "Sql server connection string",
        "TimeCacheInSeconds": "Integer cache timeout in seconds"
    },

    //Web Api Features Toggle Configurations
    //All features should be unique or it should represent a toggle option
    "FeatureManagement": {
        "FeatureA": true,
        "FeatureB": false,
        "FeatureC": true,
        "NewFeatureEnabled": false,
        "RefreshableFeature": false,
        "StrongTypedResponse": true
    },

    //Jwt Configuration for webapi authorization
    "JwtSettings": {
        "Enabled": false,
        "Audience": "Macgyver.WebApi",
        "Issuer": "Macgyver.WebApi",
        "SecretKey": "963D9AB0-0B19-4227-BB5E-936DBAB2281D"
    }
}
```

### Uninstall MacGyver template

Run the following command:

```bash
dotnet new -u Macgyver.WebApi
```

### **Building and running your first project**

#### Local

Building locally can be done using the command `dotnet build` from the `src` folder.
To run the project, run the command `dotnet run` for web api project. The API can be accessed on port `80` for HTTP. Example: `dotnet run -p Cliente.WebApi/Cliente.WebApi.csproj`

> **Note**: Don't forget the configuration used to create the web api project, review the `appsettings.json`.

#### Docker

At the `src` folder, build the image by running the command `docker build -f Cliente.WebApi/Dockerfile -t clientewebapi:v1 .`.
To Run the container on default port `80` run the command `docker run -it -p 80:80 clientewebapi:v1`.

> **Note**:
>
> 1. Remember the configured settings when the app was created.
> 2. The docker name must be lower case for it is case sensitive.
> 3. The default port is 80, make sure the port is available for use;

#### Docker-compose

At the `src` folder, run the command `docker-compose up`.

> **Note**:
>
> 1. There is a *.env* file that handles the IMAGE_TAG and IMAGE_REPOSITORY variables, responsible for tagging and the docker's image repository source/path respectively, where the dockercompose will check whether the file exists and use it.
> 2. For local versioning of the container image, adjust the IMAGE_TAG property.

#### Easy choice to build and run

At the root folder, the file:

* `build.sh` will build, publish, check the docker compose config file, and generate a new image (check the name of image and tag version inside `.env` file in `src` folder).
* `run.sh` will do the same as the previous command and will execute the container at the link `http://localhost:80/`.

## **Solution Structure**

### Folder structure

```text
├───Macgyver.Application                           # Layer that defines the jobs the software is supposed to do and directs the expressive domain objects to work out problems.
|   |                                              # The tasks this layer is responsible for, are meaningful to the business or necessary for interaction with the application layers of other systems.
│   └───Microsoft.Extensions.DependencyInjection   # Contains the file responsible for the application services dependency injection and layer configuration.
|
├───Macgyver.Domain                                # Layer responsible for representing concepts of the business, information about the business situation, and business rules. State that reflects the business
|   |                                              # situation is controlled and used here, even though the technical details of storing it are delegated to the infrastructure. This layer is the heart of
|   |                                              # business software.
│   ├───Adapters                                   # Folder that contains the adapters interfaces mapped under an optic oriented to the adapter's purpose and its performed actions.
│   ├───Exceptions                                 # Folder that contains all exceptions and errors recognized by the business.
│   ├───Models                                     # Folder that contains all business domain model representations.
│   └───Services                                   # Folder that contains all service interfaces mapped under operations/context to handle business rules.
|
├───Macgyver.MongoAdapter                          # Secondary adapter layer responsible for communicating with external mongo database.
│   └───Microsoft.Extensions.DependencyInjection   # Contains the file responsible for adapter services dependency injection and layer configuration.
|
├───Macgyver.ServiceNowAdapter                     # An example of a secondary adapter layer, responsible for the external ServiceNow API communication using Refit.
│   ├───Clients                                    # Folder that contains all interfaces and input and output contracts, mapped according to the external API documentation.
│   ├───Extensions                                 # Folder that contains all extension methods that aids the application in handling ServiceNow data.
│   └───Microsoft.Extensions.DependencyInjection   # Contains the file responsible for adapter services dependency injection and layer configuration.
|
├───Macgyver.TmdbAdapter                           # An example of a secondary adapter layer, responsible for the external Tmdb API communication using Refit.
│   ├───Clients                                    # Folder that contains all interfaces and input and output contracts, mapped according to the external API documentation.
│   └───Microsoft.Extensions.DependencyInjection   # Contains the file responsible for adapter services dependency injection and layer configuration.
|
├───Macgyver.SqlServerAdapter                      # An example of a secondary adapter layer, responsible for SqlServer database communication.
│   └───Microsoft.Extensions.DependencyInjection   # Contains the file responsible for adapter services dependency injection and layer configuration.
|
├───Macgyver.WebApi                                # An example of a primary adapter layer, responsible for converting the incoming information, into information recognized by the application, and returning the data |                                                  # into information recognized by the external world.
│   ├───Controllers                                # Contains all controllers with routes preestablished under a business context to receive external world data.
│   ├───Dtos
│   │   ├───Incident                               # Contains the input and output contracts from the incident controller.
│   │   └───Movie                                  # Contains all input and output contracts from the movie controller.
│   └───Extensions                                 # Folder that contains all extension methods that aids the WebApi with application configurations and service collections handling.
|
└───tests
    ├───Macgyver.WebApi.IntegrationTests           # Web Api integration test layer.
    │   ├───Adapters                               # Cotnains adapters mock.
    │   └───TestResults                            # Contains the results of the tests.
    │
    ├───Macgyver.Application.UnitTests             # Application unit test layer.
    │   └───TestResults                            # Contains the results of the tests.
    │
    └───Macgyver.WebApi.UnitTests                  # Web Api unit test layer.
        └───TestResults                            # Contains the results of the tests.
```

### References structure

```mermaid
graph LR;
    WebApi-->Application;
    WebApi-->Adapter;
    Application-->Domain
    Application-->Adapter
    Adapter-->Domain
```

### Endpoints structure

#### 1. Feature Toggles Controller

```mermaid
graph LR
    Macgyver:::someclass --> /featuretoggles
    /featuretoggles --> GET
    classDef someclass fill:#f96;
```

#### 2. Movies Controller

```mermaid
graph LR
    Macgyver:::someclass --> /movies
    /movies --> POST
    /movies -- id --> PUT
    /movies -- id --> DELETE
    /movies -- id --> GET
    /movies --> GET
    classDef someclass fill:#f96;
```

#### 3. Incidents Controller

```mermaid
graph LR
    Macgyver:::someclass --> /incidents
    /incidents --> GET
    /incidents -- id --> GET
    /incidents --> POST
    classDef someclass fill:#f96;
```

#### 4. Movies Search from Tmdb Source

   ```mermaid
   graph LR
       Macgyver:::someclass --> /movies/source
       /movies/source --/tmdb --> GET
       classDef someclass fill:#f96;
   ```

#### 5. People Controller

```mermaid
graph LR
    Macgyver:::someclass --> /people
    /people --> POST
    /people -- id --> PUT
    /people -- id --> DELETE
    /people -- id --> GET
    /people --> GET
    classDef someclass fill:#f96;
```

### Movie search request sequence diagram

Below is an example of a systemic call where the intent is to search for the Avengers movie.

```mermaid
sequenceDiagram
ExternalCall->>WebApi: Search for Avengers movie
WebApi ->> Application:  Converts the dto <br> into domain entity
alt The movie is in cache
   TmdbAdapter->>Application: Get list of movies from cache
else Else
   TmdbAdapter-->>ExternalApi: Search in TMDb movie
   ExternalApi-->>TmdbAdapter: Returns
   TmdbAdapter->>Application: Return list of movies
end
Application->>WebApi: Builds contract <br> returning the movies
WebApi->> ExternalCall: Return movies
```

## **FAQ**

### How can I adapt the response my webapi to sophie base response?

We have a solution in WebApiBoot which will use a attribute who manipulate and adapt the response of endpoint to base response where the sophie can understand. Just use mark the controller OR a endpoint with `[DefaultSophieSuccessResponseFilter]` and the result action response will adapt automatically to json { type, data, total}.

Code Example:

```c#
[FeatureGate(FeatureFlags.StrongTypedResponse)]
[HttpGet]
[DefaultSophieSuccessResponseFilter] //this is the attribute filter !!!
public async Task<IActionResult> GetAll()
{
    var features = new FeatureToggleGetResponse
    {
        FeatureA = await _featureManager.IsEnabledAsync(nameof(FeatureFlags.FeatureA)),
        FeatureB = await _featureManager.IsEnabledAsync(nameof(FeatureFlags.FeatureB)),
        FeatureC = await _featureManager.IsEnabledAsync(nameof(FeatureFlags.FeatureC)),
        NewFeatureEnabled = await _featureManager.IsEnabledAsync(nameof(FeatureFlags.NewFeatureEnabled)),
        RefreshableFeature = await _featureManager.IsEnabledAsync(nameof(FeatureFlags.RefreshableFeature)),
    };

    return Ok(features);
}
```

> **NOTE**: This solution was made because sophie can't work (yet) with full REST integrations and its unable to understand and work http status response.

### I tried to install the MacGyver web api template but something went wrong

* Check the source of your nuget using command `nuget source` or `dotnet nuget list source`. You should see the link with [Enabled]
* Open the NuGet.Config (check the [location](https://docs.microsoft.com/en-us/nuget/consume-packages/configuring-nuget-behavior#config-file-locations-and-uses)) and verify if the credential were there, and if not, remover the link of "https://git.parli.com.br/api/v4/projects/541/packages/nuget/index.json" and follow the step [Creating your first project](#creating-your-first-project) again.
* For .NET CLI template generation, it is recommended to use the template's short name `macgyverwebapi` without special characters. There is a different betweem using the template nuget name `Macgyver.WebApi` and the short name `macgyverwebapi` of template model

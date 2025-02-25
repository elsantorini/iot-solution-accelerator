# Microsoft Azure Cosmos DB IoT solution accelerator - step-by-step quickstart guide

<details>
<summary><strong><em>Table of Contents</em></strong></summary>
<!-- TOC -->

- [Microsoft Azure Cosmos DB IoT solution accelerator - step-by-step quickstart guide](#microsoft-azure-cosmos-db-iot-solution-accelerator---step-by-step-quickstart-guide)
  - [Overview](#overview)
    - [Adapting the sample scenario to your own](#adapting-the-sample-scenario-to-your-own)
  - [Solution architecture](#solution-architecture)
    - [Architecture components](#architecture-components)
  - [Requirements](#requirements)
    - [Task 0: Download the starter files](#task-0-download-the-starter-files)
  - [Section 1: Configure environment](#section-1-configure-environment)
    - [Deployment and setup time](#deployment-and-setup-time)
    - [Task 1: Run deployment scripts](#task-1-run-deployment-scripts)
      - [Deployment information: Azure Cosmos DB](#deployment-information-azure-cosmos-db)
      - [About Azure Cosmos DB throughput](#about-azure-cosmos-db-throughput)
      - [About Azure Cosmos DB partitioning](#about-azure-cosmos-db-partitioning)
      - [About the Azure Cosmos DB indexing policies](#about-the-azure-cosmos-db-indexing-policies)
    - [Task 2: Authenticate the Office 365 API Connection for sending email alerts](#task-2-authenticate-the-office-365-api-connection-for-sending-email-alerts)
      - [About the Logic App](#about-the-logic-app)
    - [Task 3: Add Stream Analytics Event Hubs input](#task-3-add-stream-analytics-event-hubs-input)
    - [Task 4: Add Stream Analytics outputs](#task-4-add-stream-analytics-outputs)
    - [Task 5: Create Stream Analytics query](#task-5-create-stream-analytics-query)
    - [Task 6: Run Stream Analytics job](#task-6-run-stream-analytics-job)
  - [Section 2: Deploying Function Apps and Web App](#section-2-deploying-function-apps-and-web-app)
    - [Task 1: Open solution](#task-1-open-solution)
    - [Task 1: Deploy Azure Cosmos DB Processing Function App](#task-1-deploy-azure-cosmos-db-processing-function-app)
      - [Azure Cosmos DB Processing Function App code walk-through](#azure-cosmos-db-processing-function-app-code-walk-through)
    - [Task 2: Deploy Stream Processing Function App](#task-2-deploy-stream-processing-function-app)
      - [Stream Processing Function App code walk-through](#stream-processing-function-app-code-walk-through)
    - [Task 3: Configure Azure Active Directory application for the Web App](#task-3-configure-azure-active-directory-application-for-the-web-app)
      - [(Optionally) Install AzureAD PowerShell modules](#optionally-install-azuread-powershell-modules)
      - [Open PowerShell and navigate to the scripts directory](#open-powershell-and-navigate-to-the-scripts-directory)
      - [Option 1 (interactive)](#option-1-interactive)
      - [Option 2 (interactive with specified tenant)](#option-2-interactive-with-specified-tenant)
      - [Option 3 (manual steps)](#option-3-manual-steps)
        - [Choose the Azure AD tenant where you want to create your applications](#choose-the-azure-ad-tenant-where-you-want-to-create-your-applications)
        - [Register the webApp app (IoTSolutionAcceleratorWebApp)](#register-the-webapp-app-iotsolutionacceleratorwebapp)
    - [Task 4: Deploy Web App](#task-4-deploy-web-app)
    - [Task 5: Add new redirect URIs to the Azure AD application](#task-5-add-new-redirect-uris-to-the-azure-ad-application)
    - [Task 6: Update your notification settings in the Web App](#task-6-update-your-notification-settings-in-the-web-app)
      - [Web App code walk-through](#web-app-code-walk-through)
  - [Section 3: Configuring Azure Databricks](#section-3-configuring-azure-databricks)
    - [Task 1: Create Azure Databricks cluster](#task-1-create-azure-databricks-cluster)
    - [Task 2: Configure Key Vault-backed Databricks secret store](#task-2-configure-key-vault-backed-databricks-secret-store)
  - [Section 4: Explore and execute the data generator](#section-4-explore-and-execute-the-data-generator)
    - [How to provision your own devices](#how-to-provision-your-own-devices)
    - [Task 1: View the Azure Cosmos DB processing Function App in the portal and copy the Health Check URL](#task-1-view-the-azure-cosmos-db-processing-function-app-in-the-portal-and-copy-the-health-check-url)
    - [Task 2: View stream processing Function App in the portal and copy the Health Check URL](#task-2-view-stream-processing-function-app-in-the-portal-and-copy-the-health-check-url)
    - [Task 3: Open the data generator project](#task-3-open-the-data-generator-project)
      - [Code walk-through](#code-walk-through)
    - [Task 4: Update application configuration](#task-4-update-application-configuration)
    - [Task 5: Run generator](#task-5-run-generator)
    - [Task 6: View devices in IoT Hub](#task-6-view-devices-in-iot-hub)
  - [Section 5: Observe Change Feed using Azure Functions and App Insights](#section-5-observe-change-feed-using-azure-functions-and-app-insights)
    - [Task 1: Open App Insights Live Metrics Stream](#task-1-open-app-insights-live-metrics-stream)
  - [Section 6: Observe data using the Azure Cosmos DB Data Explorer and Web App](#section-6-observe-data-using-the-azure-cosmos-db-data-explorer-and-web-app)
    - [Task 1: View data in Azure Cosmos DB Data Explorer](#task-1-view-data-in-azure-cosmos-db-data-explorer)
    - [Task 2: Search and view data in Web App](#task-2-search-and-view-data-in-web-app)
  - [Section 7: Perform CRUD operations using the Web App](#section-7-perform-crud-operations-using-the-web-app)
    - [Task 1: Create a new vehicle](#task-1-create-a-new-vehicle)
    - [Task 2: View and edit the vehicle](#task-2-view-and-edit-the-vehicle)
    - [Task 3: Delete the vehicle](#task-3-delete-the-vehicle)
  - [Section 8: Create the Fleet status real-time dashboard in Power BI](#section-8-create-the-fleet-status-real-time-dashboard-in-power-bi)
    - [Task 1: Launch Power BI online and create the dashboard](#task-1-launch-power-bi-online-and-create-the-dashboard)
  - [Section 9: Create the Trip/Consignment Status reports in Power BI](#section-9-create-the-tripconsignment-status-reports-in-power-bi)
    - [Task 1: Import report in Power BI Desktop](#task-1-import-report-in-power-bi-desktop)
    - [Task 2: Update report data sources](#task-2-update-report-data-sources)
    - [Task 3: Explore report](#task-3-explore-report)
  - [Section 10: Run the predictive maintenance batch scoring](#section-10-run-the-predictive-maintenance-batch-scoring)
    - [About Azure Machine Learning](#about-azure-machine-learning)
    - [Task 1: Import lab notebooks into Azure Databricks](#task-1-import-lab-notebooks-into-azure-databricks)
    - [Task 2: Run batch scoring notebook](#task-2-run-batch-scoring-notebook)
  - [Section 11: Deploy the predictive maintenance web service](#section-11-deploy-the-predictive-maintenance-web-service)
    - [Task 1: Run deployment notebook](#task-1-run-deployment-notebook)
    - [Task 2: Call the deployed scoring web service from the Web App](#task-2-call-the-deployed-scoring-web-service-from-the-web-app)
    - [About Azure Machine Learning workspace and model deployments](#about-azure-machine-learning-workspace-and-model-deployments)
      - [High-level model workflow](#high-level-model-workflow)
        - [1 - Train](#1---train)
        - [2 - Package](#2---package)
        - [3 - Validate](#3---validate)
        - [4 - Deploy](#4---deploy)
        - [5 - Monitor](#5---monitor)
  - [Section 12: Refresh the Power BI report and view maintenance data](#section-12-refresh-the-power-bi-report-and-view-maintenance-data)
    - [Task 1: Open and refresh the report in Power BI Desktop](#task-1-open-and-refresh-the-report-in-power-bi-desktop)
  - [Environment clean-up](#environment-clean-up)
    - [Task 1: Delete the resource group](#task-1-delete-the-resource-group)

<!-- /TOC -->
</details>

## Overview

### Adapting the sample scenario to your own

The sample devices and data provided in this solution accelerator are based on fleets of vehicles containing sensors used to track vehicle and refrigeration unit telemetry. Feel free to adapt this to your own scenario, whether you work with oil field pumps, temperature sensors, or any of the thousands of possibilities in the IoT space.

> We refer to vehicles and oil field pumps throughout the guide to help you adapt the sample scenario to your own.

Contoso Auto is a high value cargo logistics organization that is collecting vehicle and package telemetry data and wants to use Azure Cosmos DB to rapidly ingest and store this data in its raw form, do some processing in near real-time to generate insights to support several business objectives and surface these to the most appropriate user communities within the organization. It is a fast growing organization and wants to be able to scale and manage the associated cost of its chosen technology to enable it to cope with its explosive growth and the inherent seasonality of the logistics business. This scenario includes applicability to both the vehicle telemetry and logistics use cases by focusing on trucking and inclusion of cargo sensing data. This additionally allows for many representative customer analytics scenarios.

From a technology perspective Contoso would like to leverage Azure Cosmos DB as the core repository for its hot data path and leverage the Azure Cosmos DB Change Feed as a means to drive a solid and robust event sourcing architecture that would allowing Contoso developers to quickly enhance the solution. This achieved using a robust and agile serverless approach by leveraging events published by the Change Feed that reflect the state changes within the application (database).

Ultimately Contoso would surface the raw and derived insights data to its users in one of three roles:

- **Logistic Operations personnel** who are interested in the current state of the vehicles and cargo logistics and who would use a web app to quickly understand the status of any single vehicle or piece of cargo, be notified of alerts as well as load vehicle and cargo meta data into the system. What they would like to see on the dashboard are various visualizations of detected anomalies, like engines overheating, abnormal oil pressure, and aggressive driving.

- **Management and Customer Reporting personnel** who would like to be in a position to see the current state of the vehicle fleet and customer consignment level information presented in on a Power BI report that automatically updates with new data as it flows in after being processed. What they would like to see are reports on bad driving behavior by driver and using visual components such as a map to show anomalies related to cities or areas, as well as various charts and graphs depicting aggregate fleet and consignment information in a clear way.

In this experience, you will use Azure Cosmos DB to ingest streaming vehicle telemetry data as the entry point to a near real-time analytics pipeline built on Azure Cosmos DB, Azure Functions, Event Hubs, Azure Databricks, Azure Storage, Azure Stream Analytics, Power BI, Azure Web Apps, and Logic Apps.

## Solution architecture

Below is a diagram of the solution architecture you will build in this guide. Please study this carefully, so you understand the whole of the solution as you are working on the various components.

![A diagram showing the components of the solution is displayed.](media/solution-architecture.png 'Solution Architecture')

### Architecture components

- Data ingest, event processing, and storage:

  The solution for the IoT scenario centers around **Azure Cosmos DB**, which acts as the globally-available, highly scalable data storage for streaming event data, fleet, consignment, package, and trip metadata, and aggregate data for reporting. Vehicle telemetry (you may not have vehicles, but oil field pumps) data flows in from the data generator, through registered IoT devices in **IoT Hub**, where an **Azure function** processes the event data and inserts it into a telemetry container in Azure Cosmos DB.

- Trip processing with Azure Functions:

  The Azure Cosmos DB change feed triggers three separate Azure functions, with each managing their own checkpoints so they can process the same incoming data without conflicting with one another. One function serializes the event data and stores it into time-sliced folders in **Azure Storage** for long-term cold storage of raw data. Another function processes the vehicle (or pump) telemetry, aggregating the batch data and updating the trip and consignment status in the metadata container, based on odometer readings and whether the trip is running on schedule. This function also triggers a **Logic App** to send email alerts when trip milestones are reached. A third function sends the event data to **Event Hubs**, which in turn triggers **Stream Analytics** to execute time window aggregate queries.

- Stream processing, dashboards, and reports:

  The Stream Analytics queries output vehicle-specific aggregates to the Azure Cosmos DB metadata container, and overall vehicle aggregates to **Power BI** to populate its real-time dashboard of vehicle status information. A Power BI Desktop report displays detailed vehicle, trip, and consignment information pulled directly from the Azure Cosmos DB metadata container. It also displays batch battery failure predictions, pulled from the maintenance container.

- Advanced analytics and ML model training:

  **Azure Databricks** is used to train a machine learning model to predict vehicle battery failure, based on historical information. It saves a trained model locally for batch predictions, and deploys a model and scoring web service to **Azure Kubernetes Service (AKS)** or **Azure Container Instances (ACI)** for real-time predictions. Azure Databricks also uses the **Spark Cosmos DB connector** to pull down each day's trip information to make batch predictions on battery failure and store the predictions in the maintenance container.

  > We use vehicle battery data in this sample scenario to provide a concrete example of how Apache Spark, through an Azure Databricks workspace, can directly connect to Azure Cosmos DB and use it as a source for advanced analytics and machine learning. The data, or the machine learning model, are not important. What we highlight is the Spark connector for Azure Cosmos DB and the Azure Key Vault-backed secret store to securely access secrets, like the Azure Cosmos DB connection string. You may choose to adapt the supplied notebooks to your scenario or skip the ML pieces altogether.

- Fleet management web app, security, and monitoring:

  A **Web App** allows Contoso Auto to manage vehicles and view consignment, package, and trip information that is stored in Azure Cosmos DB. The Web App is also used to make real-time battery failure predictions while viewing vehicle information. **Azure Key Vault** is used to securely store centralized application secrets, such as connection strings and access keys, and is used by the Function Apps, Web App, and Azure Databricks. Finally, **Application Insights** provides real-time monitoring, metrics, and logging information for the Function Apps and Web App.

## Requirements

1. Microsoft Azure subscription must be pay-as-you-go or MSDN.
   - Trial subscriptions will not work.
   - **IMPORTANT**: To complete the OAuth 2.0 access components of this hands-on lab you must have permissions within your Azure subscription to create an App Registration and service principal within Azure Active Directory.
2. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/)
3. [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest) - version 2.0.68 or later
4. Install [Visual Studio 2019 Community](https://visualstudio.microsoft.com/vs/) (v16.4) or greater
5. Install [.NET Core SDK 2.2](https://dotnet.microsoft.com/download/dotnet-core/2.2) and [.NET Core SDK 3.1](https://dotnet.microsoft.com/download/dotnet-core/3.1) or greater
6. Optional: [Windows PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/install/installing-windows-powershell) (PowerShell Core will not work with the Azure AD scripts at this time)

### Task 0: Download the starter files

Download a starter project that includes a vehicle simulator, Azure Function App projects, a Web App project, Azure Databricks notebooks, and data files used in the lab.

1. From your lab computer, download the starter files by downloading a .zip copy of the Azure Cosmos DB scenario-based labs GitHub repo.

2. In a web browser, navigate to the [Azure Cosmos DB IoT solution accelerator repo](https://github.com/AzureCosmosDB/solution-accelerator).

3. On the repo page, select **Clone or download**, then select **Download ZIP**.

   ![Download .zip containing the repository](media/github-download-repo.png 'Download ZIP')

4. Unzip the contents to your root hard drive (i.e. `C:\`). This will create a folder on your root drive named `solution-accelerator-master`.

5. Navigate to the [.NET Core 2.2 download page](https://dotnet.microsoft.com/download/dotnet-core/2.2), then download the SDK for your environment, such as Windows .NET Core Installer x64.

6. Navigate to the [.NET Core 3.1 download page](https://dotnet.microsoft.com/download/dotnet-core/3.1), then download the SDK for your environment, such as Windows .NET Core Installer x64.

## Section 1: Configure environment

You must provision a few resources in Azure before you start developing the solution. Ensure all resources use the same resource group for easier cleanup.

In this section, you will configure your environment so you can start sending and processing generated vehicle, consignment, package, and trip data. You will begin by creating an Azure Cosmos DB database and containers, then you will create a new Logic App and create a workflow for sending email notifications, create an Application Insights service for real-time monitoring of your solution, then retrieve secrets used in the solution's application settings (such as connection strings) and securely store them in Azure Key Vault, and finally configure your Azure Databricks environment.

### Deployment and setup time

Most of the deployment is automated, but there is some manual configuration you must complete.

We base the time estimates that follow on an experienced Azure user completing the setup steps in this Quickstart guide, bypassing code and application walkthroughs, as well as the learning materials located throughout the guide.

- Automated deployment from the ARM template: **< 15 minutes**.
- Manual configuration of core components: **1 hour**.
- (Optional) Power BI dashboard creation: **15 minutes**.
- (Optional) Power BI desktop report configuration: **5-10 minutes**.
- (Optional) Azure Databricks configuration, batch processing, and model deployment: **~30 minutes**.

> **Before you begin**: See [detailed monthly pricing](Pricing.md) of the deployed resources.

### Task 1: Run deployment scripts

1. Select the **Deploy to Azure** button below to get started. When prompted, sign in to the Azure portal with your account.

   <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzureCosmosDB%2Fsolution-accelerator%2Fmaster%2Fdeploy%2FdemoDeploy.json" target="_blank">
   <img src="http://azuredeploy.net/deploybutton.png"/>
   </a>

2. Enter the following values:

   - **Subscription**: select the Azure subscription you are using for this lab.
   - **Resource group**: _if you are using a hosted environment, select the existing `iot` resource group provided for you_; Otherwise, create a new resource group like `cosmos-db-iot`.
   - **Location**: select the location closest to you. This value sets the Resource Group location.
   - **Recipient Email**: Enter an email address to receive notifications from the Logic App.
   - **Location**: select the location closest to you. This value sets the location for all deployed services. _The options in this list are limited to those locations commonly available to all services in this solution_.

3. Check the **I agree to the terms and conditions stated above** box.

    ![The template form is displayed with the previously described values.](media/portal-deploy-template-form.png "Custom Template")

4. Select **Purchase**

> The template deployment will take a few minutes to complete. Continue with the guide once it completes.

#### Deployment information: Azure Cosmos DB

Among the Azure resources the deployment script created, is an Azure Cosmos DB database and four SQL-based containers:

- **telemetry**: Used for ingesting hot vehicle telemetry data with a 90-day lifespan (TTL).
- **metadata**: Stores vehicle, consignment, package, trip, and aggregate event data.
- **maintenance**: The batch battery failure predictions are stored here for reporting purposes.
- **alerts**: Stores alert settings that control the types of alerts and frequency in which they are sent. Also stores a history document that keeps track of when summary alerts are sent.

These containers are used for the demo solution used as a reference for this accelerator. In this document, as well as the [companion accelerator guide](Guide_Azure_Cosmos_DB_IoT_Solution_Accelerator.docx), we provide detailed information about design decisions and database configuration that you can use to adapt the solution to your scenario.

To view the Azure Cosmos DB containers, perform the following steps:

1. Using a new tab or instance of your browser, navigate to the Azure portal, <https://portal.azure.com>.

2. Select **Resource groups** from the left-hand menu, then search for your resource group by typing in `cosmos-db-iot`. Select your resource group that you are using for this lab.

   ![Resource groups is selected and the cosmos-db-iot resource group is displayed in the search results.](media/resource-group.png 'cosmos-db-iot resource group')

3. Select your Azure Cosmos DB account. The name starts with `cosmos-db-iot`.

   ![The Azure Cosmos DB account is highlighted in the resource group.](media/resource-group-cosmos-db.png 'Azure Cosmos DB in the Resource Group')

4. Select **Data Explorer** in the left-hand menu, then expand the **ContosoAuto** database.

   ![Data Explorer is selected and the ContosoAuto database is expanded.](media/cosmos-containers.png "Data Explorer")

5. Expand the **alerts** container in the Azure Cosmos DB Data Explorer, then select **Scale & Settings**.

    ![The Scale & Settings blade for the maintenance container is displayed.](media/cosmos-scale-settings-maintenance.png "Scale & Settings")

    The **Throughput** value for this container is set to **400** RU/s. This is the lowest setting for a container, which is sufficient for the throughput requirements for alert management-related data due to low read and write usage.

    The **Partition Key** is set to **/id**. Having the partition key and ID share the same value allows us to perform rapid, low-cost point lookups of data, when coupled with the `ReadItemAsync` method on the `Container` object when using the [Azure Cosmos DB SDK](https://github.com/Azure/azure-cosmos-dotnet-v3).

    The **Indexing Policy** is set to the default value, which automatically indexes all fields for each document stored in the container. This is because all paths are included (remember, since we are storing JSON documents, we use paths to identify the property since they can exist within child collections in the document) by setting the value of `includedPaths` to `"path": "/*"`, and the only excluded path is the internal `_etag` property, which is used for versioning the documents. The default Indexing Policy is:

    ```json
    {
        "indexingMode": "consistent",
        "automatic": true,
        "includedPaths": [
            {
                "path": "/*"
            }
        ],
        "excludedPaths": [
            {
                "path": "/\"_etag\"/?"
            }
        ]
    }
    ```

6. Expand the **maintenance** container in the Azure Cosmos DB Data Explorer, then select **Scale & Settings**.

    The **Throughput** value for this container is set to **400** RU/s, which is sufficient for the throughput requirements for maintenance data due to low read and write usage.

    The **Partition Key** is set to **/vin** (VIN means *vehicle identification number*) so we can group maintenance data by vehicle, and because the `vin` field is used in most queries.

    The **Indexing Policy** is set to the default value.

7. Expand the **metadata** container in the Azure Cosmos DB Data Explorer, then select **Scale & Settings**.

    The **Throughput** value for this container is set to **50000** RU/s. We are initially setting the throughput on this container to this high number of RU/s because the data generator will perform a bulk insert of metadata the first time it runs. After inserting the data, it will programmatically reduce the throughput to **15000**.

    The **Partition Key** is set to **/partitionKey**. This is because we store several different types of documents (records) in this container. As such, the fields vary between document types. Each document has a `partitionKey` field added, and an `entityType` field to indicate the type of document, such as "Vehicle", "Package", or "Trip". The `partitionKey` field is set to a field property value appropriate to the document type, such as `vin` for Vehicle documents. Trip documents also use `vin` as the partition key since trip data is retrieved by the related vehicle's VIN, and is often retrieved along with vehicle data. The `entityType` field can be used to filter by type of document within a given partition key.

    The **Indexing Policy** is set to the default value.

8. Expand the **telemetry** container in the Azure Cosmos DB Data Explorer, then select **Scale & Settings**.

    The **Throughput** value for this container is set to **15000** RU/s, which is optimal for handling the rate of vehicle telemetry data written to this container.

    The **Partition Key** is set to **/partitionKey**. The partitionKey property represents a synthetic composite partition key for the Azure Cosmos DB container, consisting of the VIN + current year/month. Using a composite key instead of simply the VIN provides us with the following benefits:

    1. Distributing the write workload at any given point in time over a high cardinality of partition keys.
    2. Ensuring efficient routing on queries on a given VIN - you can spread these across time, e.g. `SELECT * FROM c WHERE c.partitionKey IN (“VIN123-2019-01”, “VIN123-2019-02”, …)`.
    3. Scale beyond the 10GB quota for a single partition key value.

    Notice that the **Time to Live** setting is set to **On (no default)**. This was turned off for the other containers. Time to Live (TTL) tells Azure Cosmos DB when to expire, or delete, the document(s) automatically. This setting can help save in storage costs by removing what you no longer need. Typically, this is used on hot data, or data that must be expired after a period of time due to regulatory requirements. Turning the Time to Live setting on with no default allows us to define the TTL individually for each document, giving us more flexibility in deciding which documents should expire after a set period of time. To do this, we have a `ttl` field on the document that is saved to this container that specifies the TTL in seconds.

    Now view the **Indexing Policy**, which is different from the default policy the other containers use. This custom policy is optimized for write-heavy workloads by excluding all paths and only including the paths used when we query the container (`vin`, `state`, and `partitionKey`):

    ```json
    {
        "indexingMode": "consistent",
        "automatic": true,
        "includedPaths": [
        {
            "path": "/vin/?"
        },
        {
            "path": "/state/?"
        },
        {
            "path": "/partitionKey/?"
        }
        ],
        "excludedPaths": [
        {
            "path": "/*"
        },
        {
            "path": "/\"_etag\"/?"
        }
        ]
    }
    ```

#### About Azure Cosmos DB throughput

You will notice that we have intentionally set the **throughput** in RU/s for each container, based on our anticipated event processing and reporting workloads. In Azure Cosmos DB, provisioned throughput is represented as request units/second (RUs). RUs measure the cost of both read and write operations against your Azure Cosmos DB container. Because Azure Cosmos DB is designed with transparent horizontal scaling (e.g., scale out) and multi-master replication, you can very quickly and easily increase or decrease the number of RUs to handle thousands to hundreds of millions of requests per second around the globe with a single API call.

Azure Cosmos DB allows you to increment/decrement the RUs in small increments of 100 at the database level, or at the container level. It is recommended that you configure throughput at the container granularity for guaranteed performance for the container all the time, backed by SLAs. Other guarantees that Azure Cosmos DB delivers are 99.999% read and write availability all around the world, with those reads and writes being served in less than 10 milliseconds at the 99th percentile.

When you set a number of RUs for a container, Azure Cosmos DB ensures that those RUs are available in all regions associated with your Azure Cosmos DB account. When you scale out the number of regions by adding a new one, Cosmos will automatically provision the same quantity of RUs in the newly added region. You cannot selectively assign different RUs to a specific region. These RUs are provisioned for a container (or database) for all associated regions.

#### About Azure Cosmos DB partitioning

When you created each container, you were required to define a **partition key**. As you will see later in the lab when you review the solution source code, each document stored within a collection contains a `partitionKey` property. One of the most important decisions one must make when creating a new container is to select an appropriate partition key for the data. A partition key should provide even distribution of storage and throughput (measured in requests per second) at any given time to avoid storage and performance bottlenecks. For instance, vehicle metadata stores the VIN, which is a unique value for each vehicle, in the `partitionKey` field. Trip metadata also uses the VIN for the `partitionKey` field, since trips are most often queried by VIN, and trip documents are stored in the same logical partition as vehicle metadata since they are likely to be queried together, preventing fan-out, or cross-partition queries. Package metadata, on the other hand, use the Consignment ID value for the `partitionKey` field for the same purposes. The partition key should be present in the bulk of queries for read-heavy scenarios to avoid excessive fan-out across numerous partitions. This is because each document with a specific partition key value belongs to the same logical partition, and is also stored in and served from the same physical partition. Each physical partition is replicated across geographical regions, resulting in global distribution.

Choosing an appropriate partition key for Azure Cosmos DB is a critical step for ensuring balanced reads and writes, scaling, and, in the case of this solution, in-order change feed processing per partition. While there are no limits, per se, on the number of logical partitions, a single logical partition is allowed an upper limit of 10 GB of storage. Logical partitions cannot be split across physical partitions. For the same reason, if the partition key chosen is of bad cardinality, you could potentially have skewed storage distribution. For instance, if one logical partition becomes larger faster than the others and hits the maximum limit of 10 GB, while the others are nearly empty, the physical partition housing the maxed out logical partition cannot split and could cause an application downtime.

#### About the Azure Cosmos DB indexing policies

The default indexing policy for newly created containers indexes every property of every item, enforcing range indexes for any string or number, and spatial indexes for any GeoJSON object of type Point. This allows you to get high query performance without having to think about indexing and index management upfront. Since the `alerts`, `metadata`, and `maintenance` containers have more read-heavy workloads than `telemetry`, it makes sense to use the default indexing policy where query performance is optimized. Since we need faster writes for `telemetry`, we exclude unused paths. The use of indexing paths can offer improved write performance and lower index storage for scenarios in which the query patterns are known beforehand, as indexing costs are directly correlated to the number of unique paths indexed.

The indexing mode for all three containers is set to **Consistent**. This means the index is updated synchronously as items are added, updated, or deleted, enforcing the consistency level configured for the account for read queries. The other indexing mode one could choose is None, which disables indexing on the container. Usually this mode is used when your container acts as a pure key-value store, and you do not need indexes for any of the other properties. It is possible to dynamically change the consistency mode prior to executing bulk operations, then changing the mode back to Consistent afterwards, if the potential performance increase warrants the temporary change.

### Task 2: Authenticate the Office 365 API Connection for sending email alerts

In this task, you will open the deployed Logic App workflow and configure it to send email alerts through its HTTP trigger. This trigger will be called by one of your Azure functions that gets triggered by the Azure Cosmos DB change feed, any time a notification event occurs, such as completing a trip. You will need to have an Office 365 or Outlook.com account to send the emails.

1. In the [Azure portal](https://portal.azure.com), navigate to your resource group for this demo and open the **Logic App**.

2. Select **API connections** in the left-hand menu, then select the **office365** API connection.

    ![API connections lists the office365 connection in its blade.](media/logic-app-connections.png "API connections")

3. Select **Edit API connection** in the left-hand menu. Enter your email in the **Display Name** field, then select **Authorize** and authenticate your Office 365 account.

    ![Edit API connection](media/logic-app-office365-api-connection-edit.png 'Edit API connection')

4. Select **Save**.

#### About the Logic App

The Azure Logic Apps service works as a powerful workflow orchestrator that natively [integrates with hundreds](https://docs.microsoft.com/azure/connectors/apis-list) of Azure and 3rd-party services. Users usually build logic apps with the Logic Apps Designer, which provides a simple web-based, drag-and-drop interface. Alternately, logic apps can be built using JavaScript Object Notation (JSON) for scripting, Azure PowerShell commands, and Azure Resource Manager (ARM) templates.

The logic app that is deployed in the solution accelerator sends email notifications to recipients when certain event milestones occur, such as when a package delivery is running behind schedule, or when an oil pump encounters an anomaly.

To view the logic app, select **Logic app designer** in the left-hand menu. This will display the current workflow in the visual designer. There are currently four activities:

1. **HTTP trigger**: This is the entry point for the logic app. When you post a request to the URL provided by this activity, the logic app is triggered, and it receives a payload of data from the request body in JSON format. This is the shape of the JSON document that the Azure Function sends to the logic app through this HTTP trigger:

    ```json
    {
        "properties": {
            "consignmentId": {
                "type": "string"
            },
            "customer": {
                "type": "string"
            },
            "delayedVINs": {
                "type": "string"
            },
            "deliveryDueDate": {
                "type": "string"
            },
            "distanceDriven": {
                "type": "number"
            },
            "hasHighValuePackages": {
                "type": "boolean"
            },
            "id": {
                "type": "string"
            },
            "isSummary": {
                "type": "boolean"
            },
            "lastRefrigerationUnitTemperatureReading": {
                "type": "integer"
            },
            "location": {
                "type": "string"
            },
            "lowestPackageStorageTemperature": {
                "type": "integer"
            },
            "odometerBegin": {
                "type": "integer"
            },
            "odometerEnd": {
                "type": "number"
            },
            "plannedTripDistance": {
                "type": "number"
            },
            "recipientEmail": {
                "type": "string"
            },
            "status": {
                "type": "string"
            },
            "temperatureSetting": {
                "type": "integer"
            },
            "tripEnded": {
                "type": "string"
            },
            "tripStarted": {
                "type": "string"
            },
            "tripsCompleted": {
                "type": "integer"
            },
            "tripsDelayed": {
                "type": "integer"
            },
            "tripsStarted": {
                "type": "integer"
            },
            "vin": {
                "type": "string"
            }
        },
        "type": "object"
    }
    ```

    Defining this payload allows subsequent activities to reference the fields to dynamically add the values, as you can see below.

2. **Condition**: The Condition evaluates the `isSummary` value, which indicates whether the passed in alert is for a summary email (summary of alerts sent every x minutes) or an individual alert message. There are two paths, based on the value: **If true**, which contains an activity that sends the summary email, and **If false**, which contains an activity that sends the individual alert email.

    ![The Condition within the logic app's designer is displayed.](media/logic-app-condition.png "Logic app condition")

3. **Send an alert summary email**: This activity uses Office 365 to send an email to the defined email recipient (`recipientEmail` field). Office 365 is only one of many connections for sending emails. You can use Outlook, Gmail, SendGrid, and other email services. You can also use one of the [hundreds of service connectors](https://docs.microsoft.com/azure/connectors/apis-list) to send notifications or create multi-step workflows. Notice in the screenshot below that we are using dynamic field references in the email activity from the payload sent to the HTTP trigger:

    ![The email activity within the logic app's designer is displayed.](media/logic-app-summary-email-activity.png "Logic app summary email activity")

    You can use a dialog within the designer to add the dynamic fields from a list, or you can use a special dynamic field reference syntax (`@{source()?['field']}`) instead. When you paste the following into the email body, for instance, the dynamic fields will appear in the same way as in the screenshot above:

    ```text
    Here is a summary of the status of your trips:

    Number of trips that started: @{triggerBody()?['tripsStarted']}
    Number of trips that ended: @{triggerBody()?['tripsCompleted']}
    Delayed trips: @{triggerBody()?['tripsDelayed']}
    Delayed vehicles (VINs): @{triggerBody()?['delayedVINs']}

    Regards,
    Contoso Auto Bot
    ```

4. **Send an individual alert email**: This activity also uses Office 365 to send an email to the defined email recipient (`recipientEmail` field).

    ![The email activity within the logic app's designer is displayed.](media/logic-app-email-activity.png "Logic app email activity")

    The email body is as follows:

    ```text
    Here are the details of the trip and consignment:

    CONSIGNMENT INFORMATION:

    Customer: @{triggerBody()?['customer']}
    Delivery Due Date: @{triggerBody()?['deliveryDueDate']}
    Location: @{triggerBody()?['location']}
    Status: @{triggerBody()?['status']}

    TRIP INFORMATION:

    Trip Start Time: @{triggerBody()?['tripStarted']}
    Trip End Time: @{triggerBody()?['tripEnded']}
    Vehicle (VIN): @{triggerBody()?['vin']}
    Planned Trip Distance: @{triggerBody()?['plannedTripDistance']}
    Distance Driven: @{triggerBody()?['distanceDriven']}
    Start Odometer Reading: @{triggerBody()?['odometerBegin']}
    End Odometer Reading: @{triggerBody()?['odometerEnd']}

    PACKAGE INFORMATION:

    Has High Value Packages: @{triggerBody()?['hasHighValuePackages']}
    Lowest Package Storage Temp (F): @{triggerBody()?['lowestPackageStorageTemperature']}
    Trip Temp Setting (F): @{triggerBody()?['temperatureSetting']}
    Last Refrigeration Unit Temp Reading (F): @{triggerBody()?['lastRefrigerationUnitTemperatureReading']}

    REFERENCE INFORMATION:

    Trip ID: @{triggerBody()?['id']}
    Consignment ID: @{triggerBody()?['consignmentId']}
    Vehicle VIN: @{triggerBody()?['vin']}

    Regards,
    Contoso Auto Bot
    ```

### Task 3: Add Stream Analytics Event Hubs input

In this task, you will configure the [Azure Stream Analytics](https://docs.microsoft.com/azure/stream-analytics/stream-analytics-introduction) service that is deployed as part of the solution accelerator. This service provides real-time analytics through its event-processing engine that can work with high volumes of fast streaming data from multiple sources in parallel. Stream Analytics connects to inputs, such as IoT Hub and Event Hubs, and several outputs it can use as data sinks, including Azure Cosmos DB, Power BI, and several other Azure services. It provides a SQL-like query language used to query over the incoming data, where you can easily adjust the event ordering options and duration of time windows when performing aggregation operations through simple language constructs or configurations. We use Stream Analytics in this solution accelerator to aggregate data over time windows of varying sizes. We use these aggregates to populate materialized views in Azure Cosmos DB and to send small aggregates of data directly to Power BI to update a near real-time dashboard.

If you examine the right-hand side of the solution architecture diagram, you will see a flow of event data that feeds into Event Hubs from an Azure Cosmos DB change feed-triggered function. Stream Analytics uses the event hub as an input source for a set of time window queries that create aggregates for individual vehicle telemetry, and overall vehicle telemetry that flows through the architecture from the vehicle IoT devices. Stream Analytics has two output data sinks:

1. Azure Cosmos DB: Individual vehicle telemetry (grouped by VIN) is aggregated over a 30-second `TumblingWindow` and saved to the `metadata` container. This information is used in a Power BI report you will create in Power BI Desktop in a later task to display individual vehicle and multiple vehicle statistics.
2. Power BI: All vehicle telemetry is aggregated over a 10-second `TumblingWindow` and output to a Power BI data set. This near real-time data is displayed in a live Power BI dashboard to show in 10 second snapshots how many events were processed, whether there are engine temperature, oil, or refrigeration unit warnings, whether aggressive driving was detected during the period, and the average speed, engine temperature, and refrigeration unit readings.

![The stream processing components of the solution architecture are displayed.](media/solution-architecture-stream-processing.png 'Solution Architecture - Stream Processing')

1. In the [Azure portal](https://portal.azure.com), open your lab resource group, then open your **Stream Analytics job**.

   ![The Stream Analytics job is highlighted in the resource group.](media/resource-group-stream-analytics.png 'Resource Group')

2. Select **Inputs** in the left-hand menu. In the Inputs blade, select **+ Add stream input**, then select **Event Hub** from the list.

   ![The Event Hub input is selected in the Add Stream Input menu.](media/stream-analytics-inputs-add-event-hub.png 'Inputs')

3. In the **New input** form, specify the following configuration options:

   1. **Input alias**: Enter **events**.
   2. Select the **Select Event Hub from your subscriptions** option beneath.
   3. **Subscription**: Choose your Azure subscription for this lab.
   4. **Event Hub namespace**: Find and select your Event Hub namespace (eg. `iot-namespace`).
   5. **Event Hub name**: Select **Use existing**, then **reporting**.
   6. **Event Hub policy name**: Choose the default `RootManageSharedAccessKey` policy.

   ![The New Input form is displayed with the previously described values.](media/stream-analytics-new-input.png 'New input')

4. Select **Save**.

You should now see your Event Hubs input listed.

![The Event Hubs input is listed.](media/stream-analytics-inputs.png 'Inputs')

### Task 4: Add Stream Analytics outputs

1. **If you have never signed in to Power BI with this account**, open a new browser tab and navigate to <https://powerbi.com> and sign in. Confirm any messages if they appear and continue to the next step after the home page appears. This will help the connection authorization step from Stream Analytics succeed and find the group workspace.

2. Select **Outputs** in the left-hand menu, select **+ Add**, then select **Power BI** from the list.

   ![The Power BI output is selected in the Add menu.](media/stream-analytics-outputs-add-power-bi.png 'Outputs')

3. In the **New output** form, look toward the bottom to find the **Authorize connection** section, then select **Authorize** to sign in to your Power BI account. If you do not have a Power BI account, select the _Sign up_ option first.

   ![The Authorize connection section is displayed.](media/stream-analytics-authorize-power-bi.png 'Authorize connection')

4. After authorizing the connection to Power BI, specify the following configuration options in the form:
   1. **Output alias**: Enter **powerbi**.
   2. **Group workspace**: Select **My workspace**.
   3. **Dataset name**: Enter **Contoso Auto IoT Events**.
   4. **Table name**: Enter **FleetEvents**.
   5. **Authentication mode**: Select **User token**.

   ![The New Output form is displayed with the previously described values.](media/stream-analytics-new-output-power-bi.png 'New output')

5. Select **Save**.

You should now have two outputs listed.

![The two added outputs are listed.](media/stream-analytics-outputs.png 'Outputs')

### Task 5: Create Stream Analytics query

The Query is Stream Analytics' work horse. This is where we process streaming inputs and write data to our outputs. The Stream Analytics query language is SQL-like, allowing you to use familiar syntax to explore and transform the streaming data, create aggregates, and create materialized views that can be used to help shape your data structure before writing to the output sinks. Stream Analytics jobs can only have one Query, but you can write to multiple outputs in a single Query, as you will do in the steps that follow.

Please take a moment to analyze the query below. Notice how we are using the `events` input name for the Event Hubs input you created, and the `powerbi` and `cosmosDB` outputs, respectively. Also see where we use the `TumblingWindow` in durations of 30 seconds for `VehicleData`, and 10 seconds for `VehicleDataAll`. The `TumblingWindow` helps us evaluate events that occurred during the past X seconds and, in our case, create averages over those time periods for reporting.

1. Select **Query** in the left-hand menu. Replace the contents of the query window with the script below:

    ```sql
    WITH
    VehicleData AS (
        select
            vin,
            AVG(engineTemperature) AS engineTemperature,
            AVG(speed) AS speed,
            AVG(refrigerationUnitKw) AS refrigerationUnitKw,
            AVG(refrigerationUnitTemp) AS refrigerationUnitTemp,
            (case when AVG(engineTemperature) >= 400 OR AVG(engineTemperature) <= 15 then 1 else 0 end) as engineTempAnomaly,
            (case when AVG(engineoil) <= 18 then 1 else 0 end) as oilAnomaly,
            (case when AVG(transmission_gear_position) <= 3.5 AND
                AVG(accelerator_pedal_position) >= 50 AND
                AVG(speed) >= 55 then 1 else 0 end) as aggressiveDriving,
            (case when AVG(refrigerationUnitTemp) >= 30 then 1 else 0 end) as refrigerationTempAnomaly,
            System.TimeStamp() as snapshot
        from events TIMESTAMP BY [timestamp]
        GROUP BY
            vin,
            TumblingWindow(Duration(second, 30))
    ),
    VehicleDataAll AS (
        select
            AVG(engineTemperature) AS engineTemperature,
            AVG(speed) AS speed,
            AVG(refrigerationUnitKw) AS refrigerationUnitKw,
            AVG(refrigerationUnitTemp) AS refrigerationUnitTemp,
            COUNT(*) AS eventCount,
            (case when AVG(engineTemperature) >= 318 OR AVG(engineTemperature) <= 15 then 1 else 0 end) as engineTempAnomaly,
            (case when AVG(engineoil) <= 20 then 1 else 0 end) as oilAnomaly,
            (case when AVG(transmission_gear_position) <= 4 AND
                AVG(accelerator_pedal_position) >= 50 AND
                AVG(speed) >= 55 then 1 else 0 end) as aggressiveDriving,
            (case when AVG(refrigerationUnitTemp) >= 22.5 then 1 else 0 end) as refrigerationTempAnomaly,
            System.TimeStamp() as snapshot
        from events t TIMESTAMP BY [timestamp]
        GROUP BY
            TumblingWindow(Duration(second, 10))
    )
    -- INSERT INTO POWER BI
    SELECT
        *
    INTO
        powerbi
    FROM
        VehicleDataAll
    -- INSERT INTO COSMOS DB
    SELECT
        *,
        entityType = 'VehicleAverage',
        partitionKey = vin
    INTO
        cosmosdb
    FROM
        VehicleData
    ```

   ![The Stream Analytics job Query is displayed.](media/stream-analytics-query.png 'Query')

2. Select **Save query**.

### Task 6: Run Stream Analytics job

1. In the [Azure portal](https://portal.azure.com), open your lab resource group, then open your **Stream Analytics job**.

   ![The Stream Analytics job is highlighted in the resource group.](media/resource-group-stream-analytics.png 'Resource Group')

2. Select **Overview**.

3. In the Overview blade, select **Start** and select **Now** for the job output start time.

4. Select **Start** to beginning running the Stream Analytics job.

   ![The steps to start the job as described are displayed.](media/stream-analytics-start-job.png 'Start job')

## Section 2: Deploying Function Apps and Web App

In the architecture for this scenario, Azure functions play a major role in event processing. These functions execute within an Azure Function App, Microsoft's serverless solution for easily running small pieces of code, or "functions," in the cloud. You can write just the code you need for the problem at hand, without worrying about a whole application or the infrastructure to run it. Functions can make development even more productive, and you can use your development language of choice, such as C#, F#, Node.js, Java, or PHP.

Before we dive into this section, let's go over how the functions and Web App fit into our architecture.

There are three Function Apps and one Web App in the solution. The Function Apps handle event processing within two stages of the data pipeline, and the Web App is used to perform CRUD operations against data stored in Azure Cosmos DB.

![The two Function Apps and Web App are highlighted.](media/solution-diagram-function-apps-web-app.png 'Solution diagram')

You may wonder, if a Function App contains several functions within, _why do we need two Function Apps instead of one_? The primary reason for using two Function Apps is due to how functions scale to meet demand. When you use the Azure Functions consumption plan, you only pay for the time your code runs. More importantly, Azure automatically handles scaling your functions to meet demand. It scales using an internal scale controller that evaluates the type of trigger the functions are using, and applies heuristics to determine when to scale out to multiple instances. The important thing to know is that functions scale at the Function App level. Meaning, if you have one very busy function and the rest are mostly idle, that one busy function causes the entire Function App to scale. Think about this when designing your solution. It is a good idea to **divide extremely high-load functions into separate Function Apps**.

Now let's introduce the Function Apps and Web App and how they contribute to the architecture.

- **IoT-StreamProcessing Function App**: This is the Stream Processing Function App, and it contains a two functions:

  - **IoTHubTrigger**: This function is automatically triggered by the IoT Hub's Event Hub endpoint as vehicle telemetry is sent by the data generator. The function performs some light processing to the data by defining the partition key value, the document's TTL, adds a timestamp value, then saves the information to Azure Cosmos DB.
  - **HealthCheck**: This function has an Http trigger that enables users to verify that the Function App is up and running, and that each configuration setting exists and has a value. More thorough checks would validate each value against an expected format or by connecting to each service as required. The function will return an HTTP status of `200` (OK) if all values contain non-zero strings. If any are null or empty, the function will return an error (`400`), indicating which values are missing. The data generator calls this function before running.

  ![The Event Processing function is shown.](media/solution-architecture-function1.png 'Solution architecture')

- **IoT-CosmosDBProcessing Function App**: This is the Trip Processing Function App. It contains three functions that are triggered by the Azure Cosmos DB Change Feed on the `telemetry` container. Because the Azure Cosmos DB Change Feed supports multiple consumers, these three functions can run in parallel, processing the same information simultaneously without conflicting with one another. When we define the `CosmosDBTrigger` for each of these functions, we configure the trigger settings to connect to an Azure Cosmos DB collection named `leases` to keep track of which change feed events they have processed. We also set the `LeaseCollectionPrefix` value for each function with a unique prefix so one function does not attempt to retrieve or update the lease information for another. The following functions are in this Function App:

  - **TripProcessor**: This function groups vehicle telemetry data by VIN, retrieves the associated Trip record from the `metadata` container, updates the Trip record with a trip start timestamp, an end timestamp if completed, and a status showing whether the trip has started, is delayed, or has completed. It also updates the associated Consignment record with the status, and triggers the Logic App with the trip information if an alert needs to be emailed to the recipient defined in the Function App's app settings (`RecipientEmail`).
  - **ColdStorage**: This function connects to the Azure Storage account (`ColdStorageAccount`) and writes the raw vehicle telemetry data for cold storage in the following time-sliced path format: `telemetry/custom/scenario1/yyyy/MM/dd/HH/mm/ss-fffffff.json`.
  - **SendToEventHubsForReporting**: This function simply sends the vehicle telemetry data straight to Event Hubs, allowing Stream Analytics to apply windowed aggregates and save those aggregates in batches to Power BI and to the Azure Cosmos DB `metadata` container.
  - **HealthCheck**: As with the function of the same name within the Stream Processing Function App, this function has an Http trigger that enables users to verify that the Function App is up and running, and that each configuration setting exists and has a value. The data generator calls this function before running.
  - **SendQueuedAlerts**: This function executes on a regular 5-minute interval via its `TimerTrigger`. It uses the `TripHelper` to determine whether to send a summary alert, based on the user settings and the number of alerts in the Azure Storage queue, if applicable.

  ![The Trip Processing function is shown.](media/solution-architecture-function2.png 'Solution architecture')

- **IoTWebApp**: The Web App provides a Fleet Management portal, allowing users to perform CRUD operations on vehicle data, make real-time battery failure predictions for a vehicle against the deployed machine learning model, and view consignments, packages, and trips. It connects to the Azure Cosmos DB `metadata` container, using the [.NET SDK for Azure Cosmos DB v3](https://github.com/Azure/azure-cosmos-dotnet-v3/).

  ![The Web App is shown.](media/solution-architecture-webapp.png 'Solution architecture')

### Task 1: Open solution

In this task, you will open the Visual Studio solution for this lab. It contains projects for both Function Apps, the Web App, and the data generator.

1. Open Windows Explorer and navigate to the location you extracted the solution ZIP file, as instructed at the beginning of this Quickstart guide. If you extracted the ZIP file directly to `C:\`, you need to open the following folder: `C:\solution-accelerator-master\Solution`. Open the Visual Studio solution file: **CosmosDbIoTScenario.sln**.

    > If Visual Studio prompts you to sign in when it first launches, use the account provided to you for this lab (if applicable), or an existing Microsoft account.

2. After opening the solution, observe the included projects in the **Solution Explorer**:

    1. **Functions.CosmosDB**: Project for the **IoT-CosmosDBProcessing** Function App.
    2. **Functions.StreamProcessing**: Project for the **IoT-StreamProcessing** Function App.
    3. **CosmosDbIoTScenario.Common**: Contains entity models, extensions, and helpers used by the other projects.
    4. **FleetDataGenerator**: The data generator seeds the Azure Cosmos DB `metadata` container with data and simulates vehicles, connects them to IoT Hub, then sends generated telemetry data.
    5. **FleetManagementWebApp**: Project for the **IoTWebApp** Web App.
    6. **Microsoft.Identity.Web**: Helper library that simplifies working with Microsoft Identity within the ASP.NET MVC Core web app (`IoTWebApp`).

    ![The Visual Studio Solution Explorer is displayed.](media/vs-solution-explorer.png "Solution Explorer")

3. Right-click on the `CosmosDbIoTScenario` solution in Solution Explorer, then select **Restore NuGet Packages**. The packages may have already been restored upon opening the solution.

### Task 1: Deploy Azure Cosmos DB Processing Function App

1. Open the Visual Studio solution file **CosmosDbIoTScenario.sln** within the `C:\solution-accelerator-master\Solution` folder.

2. In the Visual Studio Solution Explorer, right-click on the **Functions.CosmosDB** project, then select **Publish...**.

    ![The context menu is displayed and the Publish menu item is highlighted.](media/vs-publish.png "Publish")

3. In the publish dialog, select the **Azure Functions Consumption Plan** publish target. Next, select the **Select Existing** radio and make sure **Run from package file (recommended)** is checked. Select **Publish** on the bottom of the form.

    ![The publish dialog is displayed.](media/vs-publish-target-functions.png "Pick a publish target")

4. In the App Service pane, select your Azure Subscription you are using for this lab, and make sure View is set to **Resource group**. Find and expand your Resource Group in the results below. The name should start with **cosmos-db-iot**. Select the Function App whose name starts with **IoT-CosmosDBProcessing**, then select **OK**.

    ![The App Service blade of the publish dialog is displayed.](media/vs-publish-app-service-function-cosmos.png "App Service")

5. Click **Publish** to begin.

    After the publish completes, you should see the following in the Output window: `========== Publish: 1 succeeded, 0 failed, 0 skipped ==========` to indicate a successful publish.

#### Azure Cosmos DB Processing Function App code walk-through

This Function App contains a group of Azure Functions that are triggered by the Azure Cosmos DB Change Feed on the `telemetry` container. The Function App is written in C# and uses the version 2.0 function runtime on the .NET Core platform. The following are some highlights within the source code, which are areas you can adapt for your solution.

1. Open **Startup.cs** within the **Functions.CosmosDB** project and locate the following block of code:

    ```csharp
    builder.Services.AddSingleton((s) => {
        var connectionString = configuration["CosmosDBConnection"];
        var cosmosDbConnectionString = new CosmosDbConnectionString(connectionString);

        if (string.IsNullOrEmpty(connectionString))
        {
            throw new ArgumentNullException("Please specify a value for CosmosDBConnection in the local.settings.json file or your Azure Functions Settings.");
        }

        CosmosClientBuilder configurationBuilder = new CosmosClientBuilder(cosmosDbConnectionString.ServiceEndpoint.OriginalString, cosmosDbConnectionString.AuthKey);
        return configurationBuilder
            .Build();
    });
    ```

    Since we are using the [.NET SDK for Azure Cosmos DB v3](https://github.com/Azure/azure-cosmos-dotnet-v3/), and dependency injection is supported starting with Function Apps v2, we are using a [singleton Azure Cosmos DB client for the lifetime of the application](https://docs.microsoft.com/azure/cosmos-db/performance-tips#sdk-usage). This is injected into the `Functions` class through its constructor, as you will see in the next code block.

2. Open **Functions.cs** within the **Functions.CosmosDB** project and locate the following block of code for the constructor at the top of the file:

    ```csharp
    public Functions(IHttpClientFactory httpClientFactory, CosmosClient cosmosClient)
    {
        _httpClientFactory = httpClientFactory;
        _cosmosClient = cosmosClient;
    }
    ```

    This code allows the `HttpClientFactory` and the `CosmosClient` to be injected into the function code, which allows these services to manage their own connections and lifecycle to improve performance and prevent thread starvation and other issues caused by incorrectly creating too many instances of expensive objects. The `HttpClientFactory` is configured in `Startup.cs`, above the code block we detailed previously. It is used to send alerts to the Logic App endpoint, and uses [Polly](https://github.com/App-vNext/Polly) to employ a gradual back-off wait and retry policy in case the Logic App is overloaded or has other issues causing calls to the HTTP endpoint to fail.

3. Look at the first function code below the constructor:

    ```csharp
    [FunctionName("TripProcessor")]
    public async Task TripProcessor([CosmosDBTrigger(
        databaseName: "ContosoAuto",
        collectionName: "telemetry",
        ConnectionStringSetting = "CosmosDBConnection",
        LeaseCollectionName = "leases",
        LeaseCollectionPrefix = "trips",
        CreateLeaseCollectionIfNotExists = true,
        StartFromBeginning = true)]IReadOnlyList<Document> vehicleEvents,
        ILogger log)
    {
    ```

    The `FunctionName` attribute defines how the function name appears within the Function App, and can be different from the C# method name. This `TripProcessor` function uses the `CosmosDBTrigger` to fire on every Azure Cosmos DB change feed event. The events arrive in batches, whose size depends on factors such as how many Insert, Update, or Delete events there are for the container. The `databaseName` and `collectionName` properties define which container's change feed triggers the function. The `ConnectionStringSetting` indicates the name of the Function App's application setting from which to pull the Azure Cosmos DB connection string. In our case, the connection string value will draw from the Key Vault secret you created. The `LeaseCollection` properties define the name of the lease container and the prefix applied to lease data for this function, and whether to create the lease container if it does not exist. `StartFromBeginning` is set to `true`, ensuring that all events since the function last run are processed. The function outputs the change feed documents into an `IReadOnlyList` collection.

4. Scroll down a little further in the function to view the following code block:

    ```csharp
    var vin = group.Key;
    var odometerHigh = group.Max(item => item.GetPropertyValue<double>("odometer"));
    var averageRefrigerationUnitTemp =
        group.Average(item => item.GetPropertyValue<double>("refrigerationUnitTemp"));
    ```

    We have grouped the events by vehicle VIN, so we assign a local `vin` variable to hold the group key (VIN). Next, we use the `group.Max` aggregate function to calculate the max odometer value, and use the `group.Average` function to calculate the average refrigeration unit temperature. We will use the `odometerHigh` value to calculate the trip distance and determine whether the trip is completed, based on the planned trip distance from the `Trip` record in the Azure Cosmos DB `metadata` container. The `averageRefrigerationUnitTemp` is added in the alert that gets sent to the Logic App, if needed.

5. Review the code that is just below this code block:

    ```csharp
    // First, retrieve the metadata Azure Cosmos DB container reference:
    var container = _cosmosClient.GetContainer(database, metadataContainer);

    // Create a query, defining the partition key so we don't execute a fan-out query (saving RUs), where the entity type is a Trip and the status is not Completed, Canceled, or Inactive.
    var query = container.GetItemLinqQueryable<Trip>(requestOptions: new QueryRequestOptions { PartitionKey = new Microsoft.Azure.Cosmos.PartitionKey(vin) })
        .Where(p => p.status != WellKnown.Status.Completed
                    && p.status != WellKnown.Status.Canceled
                    && p.status != WellKnown.Status.Inactive
                    && p.entityType == WellKnown.EntityTypes.Trip)
        .ToFeedIterator();

    if (query.HasMoreResults)
    {
        // Only retrieve the first result.
        var trip = (await query.ReadNextAsync()).FirstOrDefault();

        if (trip != null)
        {
            var tripHelper = new TripHelper(trip, container, _httpClientFactory);

            var sendTripAlert = await tripHelper.UpdateTripProgress(odometerHigh);
    ```

    Here we are using the [.NET SDK for Azure Cosmos DB v3](https://github.com/Azure/azure-cosmos-dotnet-v3/) by retrieving an Azure Cosmos DB container reference with the CosmosClient (`_cosmosClient`) that was injected into the class. We use the container's `GetItemLinqQueryable` with the `Trip` class type to query the container using LINQ syntax and binding the results to a new collection of type `Trip`. Note how we are passing the **partition key**, in this case the VIN, to prevent executing a cross-partion, fan-out query, saving RU/s. We also define the type of document we want to retrieve by setting the `entityType` document property in the query to Trip, since other entity types can also have the same partition key, such as the Vehicle type.

    Once we have retrieved the trip (`var trip = (await query.ReadNextAsync()).FirstOrDefault();`), we instantiate a new instance of the `TripHelper` class, passing in the trip, container reference, and `HTTPClientFactory` instance that was injected into the constructor. We pass the `odometerHigh` value into the `UpdateTripProgress` method of the `TripHelper` class to determine whether we need to send an alert.

6. Expand the `Helpers` folder, then open the **TripHelper.cs** file. Review the following code block for the `UpdateTripProgress` method:

    ```csharp
    /// <summary>
    /// Uses a Trip record and the aggregate odometer reading (<see cref="odometerHigh"/>)
    /// to retrieve a Consignment record from Azure Cosmos DB and calculate the vehicle's trip
    /// progress, based on miles driven compared to the planned trip distance. If the number
    /// of miles driven are greater than or equal to the planned distance, the trip and
    /// consignment records are marked as complete. Otherwise, if the trip has not been
    /// completed and we are past the delivery due date, the trip and consignment are marked
    /// as delayed. Finally, if the trip record's start date (tripStarted) is null, the
    /// date/time is set to now and the trip and consignment records are marked as started.
    ///
    /// The trip and consignment records in the Azure Cosmos DB container are updated as needed,
    /// and if any of the three conditions are met (completed, delayed, or started), a
    /// boolean value of true is returned, indicating a trip alert should be sent.
    /// </summary>
    /// <param name="odometerHigh">The max aggregate odometer reading in the telemetry
    /// batch.</param>
    /// <returns>True if an alert needs to be sent.</returns>
    public async Task<bool> UpdateTripProgress(double odometerHigh)
    {
        var sendTripAlert = false;

        // Retrieve the Consignment record.
        var document = await _container.ReadItemAsync<Consignment>(_trip.consignmentId,
            new PartitionKey(_trip.consignmentId));
        var consignment = document.Resource;
    ```

    Since we have the Consignment ID, we can use the `ReadItemAsync` method to retrieve a single Consignment record. Here we also pass the partition key to minimize fan-out. Within an Azure Cosmos DB container, a document's unique ID is a combination of the `id` field and the partition key value.

7. Scroll down a little further in the same method to find the following code block:

    ```csharp
    if (updateTrip)
    {
        await container.ReplaceItemAsync(trip, trip.id, new Microsoft.Azure.Cosmos.PartitionKey(trip.partitionKey));
    }

    if (updateConsignment)
    {
        await container.ReplaceItemAsync(consignment, consignment.id, new Microsoft.Azure.Cosmos.PartitionKey(consignment.partitionKey));
    }
    ```

    The `ReplaceItemAsync` method updates the Azure Cosmos DB document with the passed in object with the associated `id` and partition key value.

8. Scroll down to the `SendTripAlert` method to find the following code block at the bottom of the file:

    ```csharp
    await httpClient.PostAsync(Environment.GetEnvironmentVariable("LogicAppUrl"), new StringContent(postBody, Encoding.UTF8, "application/json"));
    ```

    Here we are using the `HttpClient` created by the injected `HttpClientFactory` to post the serialized `LogicAppAlert` object to the Logic App. The `Environment.GetEnvironmentVariable("LogicAppUrl")` method extracts the Logic App URL from the Function App's application settings and, using the special Key Vault access string the deployment script added to the app setting, extracts the encrypted value from the Key Vault secret.

9. Return to the **Functions.cs** file and find the following **SendToEventHubsForReporting** function:

    ```csharp
    [FunctionName("SendToEventHubsForReporting")]
    public async Task SendToEventHubsForReporting([CosmosDBTrigger(
        databaseName: "ContosoAuto",
        collectionName: "telemetry",
        ConnectionStringSetting = "CosmosDBConnection",
        LeaseCollectionName = "leases",
        LeaseCollectionPrefix = "reporting",
        CreateLeaseCollectionIfNotExists = true,
        StartFromBeginning = true)]IReadOnlyList<Document> vehicleEvents,
        [EventHub("reporting", Connection = "EventHubsConnection")] IAsyncCollector<EventData> vehicleEventsOut,
        ILogger log)
    {
        log.LogInformation($"Sending {vehicleEvents.Count} Azure Cosmos DB records to Event Hubs for reporting.");

        if (vehicleEvents.Count > 0)
        {
            foreach (var vehicleEvent in vehicleEvents)
            {
                // Convert to a VehicleEvent class.
                var vehicleEventOut = await vehicleEvent.ReadAsAsync<VehicleEvent>();
                // Add to the Event Hub output collection.
                await vehicleEventsOut.AddAsync(new EventData(
                    Encoding.UTF8.GetBytes(JsonConvert.SerializeObject(vehicleEventOut))));
            }
        }
    }
    ``` 

    Notice that this function is also triggered by the Azure Cosmos DB Change Feed. We use a different `LeaseCollectionPrefix` value so this function keeps track of its own checkpointing when processing events from the Change Feed. This prefix allows functions to work from the Change Feed on the same container without conflicting with one another.

    The `ReadAsAsync` method is an extension method located in `CosmosDbIoTScenario.Common.ExtensionMethods` that converts an Azure Cosmos DB Document to a class; in this case, a `VehicleEvent` class. Currently, the `CosmosDBTrigger` on a function only supports returning an `IReadOnlyList` of `Documents`, requiring a conversion to another class if you want to work with your customer classes instead of a Document for now. This extension method automates the process.

    The `AddAsync` method asynchronously adds to the `IAsyncCollector<EventData>` collection defined in the function attributes, which takes care of sending the collection items to the defined Event Hub endpoint.

### Task 2: Deploy Stream Processing Function App

1. In the Visual Studio Solution Explorer, right-click on the **Functions.StreamProcessing** project, then select **Publish...**.

    ![The context menu is displayed and the Publish menu item is highlighted.](media/vs-publish.png "Publish")

2. In the publish dialog, select the **Azure Functions Consumption Plan** publish target. Next, select the **Select Existing** radio and make sure **Run from package file (recommended)** is checked. Select **Publish** on the bottom of the form.

    ![The publish dialog is displayed.](media/vs-publish-target-functions.png "Pick a publish target")

3. In the App Service pane, select your Azure Subscription you are using for this lab, and make sure View is set to **Resource group**. Find and expand your Resource Group in the results below. The name should start with **cosmos-db-iot**. Select the Function App whose name starts with **IoT-StreamProcessing**, then select **OK**.

    ![The App Service blade of the publish dialog is displayed.](media/vs-publish-app-service-function-stream.png "App Service")

4. Click **Publish** to begin.

    After the publish completes, you should see the following in the Output window: `========== Publish: 1 succeeded, 0 failed, 0 skipped ==========` to indicate a successful publish.

#### Stream Processing Function App code walk-through

This Function App provides initial stream processing from the IoT Hub instance and saves the processed data to the Azure Cosmos DB `telemetry` container.

1. Open **Functions.cs** within the **Functions.StreamProcessing** project. Let us first review the function parameters:

    ```csharp
    [FunctionName("IoTHubTrigger")]
    public static async Task IoTHubTrigger([IoTHubTrigger("messages/events", Connection = "IoTHubConnection")] EventData[] vehicleEventData,
        [CosmosDB(
            databaseName: "ContosoAuto",
            collectionName: "telemetry",
            ConnectionStringSetting = "CosmosDBConnection")]
        IAsyncCollector<VehicleEvent> vehicleTelemetryOut,
        ILogger log)
    {
    ```

    This function is defined with the `IoTHubTrigger`. Each time the IoT devices send data to IoT Hub, this function gets triggered and sent the event data in batches (`EventData[] vehicleEventData`). The `CosmosDB` attribute is an output attribute, simplifying writing Azure Cosmos DB documents to the defined database and container; in our case, the `ContosoAuto` database and `telemetry` container, respectively.

2. Scroll down in the function code to find the following code block:

    ```csharp
    vehicleEvent.partitionKey = $"{vehicleEvent.vin}-{DateTime.UtcNow:yyyy-MM}";
    // Set the TTL to expire the document after 60 days.
    vehicleEvent.ttl = 60 * 60 * 24 * 60;
    vehicleEvent.timestamp = DateTime.UtcNow;

    await vehicleTelemetryOut.AddAsync(vehicleEvent);
    ```

    The `partitionKey` property represents a synthetic composite partition key for the Azure Cosmos DB container, consisting of the VIN + current year/month. Using a composite key instead of simply the VIN provides us with the following benefits:

    1. Distributing the write workload at any given point in time over a high cardinality of partition keys.
    2. Ensuring efficient routing on queries on a given VIN - you can spread these across time, e.g. `SELECT * FROM c WHERE c.partitionKey IN ("VIN123-2019-01", "VIN123-2019-02", …)`
    3. Scale beyond the 10GB quota for a single partition key value.

    The `ttl` property sets the time-to-live for the document to 60 days, after which Azure Cosmos DB will delete the document, since the `telemetry` container is our hot path storage.

    When we asynchronously add the class to the `vehicleTelemetryOut` collection, the Azure Cosmos DB output binding on the function automatically handles writing the data to the defined Azure Cosmos DB database and container, managing the implementation details for us.

### Task 3: Configure Azure Active Directory application for the Web App

The web app uses Azure Active Directory (Azure AD) for user authentication. Before deploying the web app, we need to register a new app in Azure AD and add the domain, tenant, and app's client ID to the web app's settings. There are two options to do this. If you have Windows PowerShell (only available on Windows machines), you can run a script to automate these steps. Otherwise, you can follow the manual configuration steps.

#### (Optionally) Install AzureAD PowerShell modules

The scripts install the required PowerShell module (AzureAD) for the current user if needed. However, if you want to install if for all users on the machine, you can follow the following steps:

1. If you have not done so already, in the PowerShell window, install the AzureAD PowerShell modules. For this:

   1. Open PowerShell as an admin (On Windows, Search Powershell in the search bar, right click on it and select Run as administrator).
   2. Type:

      ```PowerShell
      Install-Module AzureAD
      ```

      Or if you cannot be an administrator on your machine, run:

      ```PowerShell
      Install-Module AzureAD -Scope CurrentUser
      ```

2. Close the PowerShell window. You will need to re-open it to gain access to the new modules.

#### Open PowerShell and navigate to the scripts directory

1. Open PowerShell (On Windows, press  `Windows-R` and type `PowerShell` in the search window)

2. Navigate to the location you extracted the solution ZIP file, as instructed at the beginning of this Quickstart guide. You need to navigate to the **AppCreationScripts** sub-folder of the **FleetManagementWebApp** directory within the `Solution` folder. If you extracted the ZIP file directly to `C:\`, you need to open the following folder: `C:\solution-accelerator-master\Solution\FleetManagementWebApp\AppCreationScripts`.

3. Until you change it, the default [Execution Policy](https:/go.microsoft.com/fwlink/?LinkID=135170) for scripts is usually `Restricted`. In order to run the PowerShell script you need to set the Execution Policy to `RemoteSigned`. You can set this just for the current PowerShell process by running the command:

    ```PowerShell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
    ```

    When prompted, enter **A** (`[A] Yes to All`) to change the execution policy.

#### Option 1 (interactive)

- Just run `. .\Configure.ps1`, and you will be prompted to sign-in (email address, password, and if needed MFA).
- The script will be run as the signed-in user and will use the tenant in which the user is defined.

> Note that the script will choose the tenant in which to create the applications, based on the user. Also to run the `Cleanup.ps1` script, you will need to re-sign-in.

#### Option 2 (interactive with specified tenant)

If you have more than one Azure tenant associated with your account, perform the following steps to define the tenant prior to running the scripts:

- Open the [Azure portal](https://portal.azure.com).
- Select the Azure Active Directory you are interested in (in the combo-box below your name on the top right of the browser window).
- Find the "Azure Active Directory" object in this tenant, found in the portal's left-hand menu.
- Go to **Properties** and copy the content of the **Directory Id** property.
- Then use the full syntax to run the scripts:

```PowerShell
$tenantId = "yourTenantIdGuid"
. .\Cleanup.ps1 -TenantId $tenantId
. .\Configure.ps1 -TenantId $tenantId
```

The `Configure.ps1` script will create the Azure AD application and update the web app's `appsettings.json` file with the details of the new application. You will be prompted to log in twice, once for each script.

#### Option 3 (manual steps)

If you cannot run the PowerShell scripts, complete the following steps to manually configure Azure AD:

<details>
    <summary>Expand to see the manual steps</summary>

##### Choose the Azure AD tenant where you want to create your applications

As a first step you'll need to:

1. Sign in to the [Azure portal](https://portal.azure.com) using either a work or school account or a personal Microsoft account.
1. If your account is present in more than one Azure AD tenant, select your profile at the top right corner in the menu on top of the page, and then **switch directory**.
Change your portal session to the desired Azure AD tenant.

##### Register the webApp app (IoTSolutionAcceleratorWebApp)

1. Navigate to the Microsoft identity platform for developers [App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page.

2. Select **New registration**.

3. When the **Register an application page** appears, enter your application's registration information:

   - In the **Name** section, enter a meaningful application name that will be displayed to users of the app, for example `IoTSolutionAcceleratorWebApp`.
   - In the **Supported account types** section, select **Accounts in this organizational directory only ({tenant name})**.

    ![Register an application](media/aad-register-app.png "Register an application")

    > Note that there are more than one redirect URIs. You'll need to add them from the **Authentication** tab later after the app has been created successfully.

4. Select **Register** to create the application.

5. On the app **Overview** page, find the **Application (client) ID** value and record it for later. You'll need it to configure the Visual Studio configuration file for this project.

    ![Overview blade](media/aad-application-overview.png "Overview blade")

6. In the list of pages for the app, select **Authentication**.

   - In the Redirect URIs section, select **Web** in the combo-box and enter the following redirect URIs.
       - `https://localhost:44321/`
       - `https://localhost:44321/signin-oidc`
   - In the **Advanced settings** section set **Logout URL** to `https://localhost:44321/signout-oidc`
   - In the **Advanced settings** | **Implicit grant** section, check **ID tokens** as this sample requires
       the [Implicit grant flow](https://docs.microsoft.com/azure/active-directory/develop/v2-oauth2-implicit-grant-flow) to be enabled to
       sign-in the user.

    ![Authentication blade](media/aad-authentication-initial.png "Authentication blade")

7. Select **Save**.

    > Note that unless the Web App calls a Web API, no certificate or secret is needed.

8. Open the **FleetManagementWebApp** project in Visual Studio and update the **appsettings.json** file:

   - Replace the `ClientID` value with the *Application ID* from the application you registered in Application Registration portal in *Step 5*.
   - Replace the `TenantId` value with the *Tenant ID* where you registered your Application in *Step 5*.
   - Replace the `Domain` value with the *Azure AD domain name*,  e.g. contoso.onmicrosoft.com where you registered your Application in *Step 5*.

</details>

### Task 4: Deploy Web App

1. In the Visual Studio Solution Explorer, right-click on the **FleetManagementWebApp** project, then select **Publish...**.

    ![The context menu is displayed and the Publish menu item is highlighted.](media/vs-publish.png "Publish")

2. In the publish dialog, select the **App Service** publish target. Next, select the **Select Existing** radio, then select **Publish** on the bottom of the form.

    ![The publish dialog is displayed.](media/vs-publish-target-webapp.png "Pick a publish target")

3. In the App Service pane, select your Azure Subscription you are using for this lab, and make sure View is set to **Resource group**. Find and expand your Resource Group in the results below. The name should start with **cosmos-db-iot**. Select the Web App whose name starts with **IoTWebApp**, then select **OK**.

    ![The App Service blade of the publish dialog is displayed.](media/vs-publish-app-service-webapp.png "App Service")

4. Click **Publish** to begin.

    After the publish completes, you should see the following in the Output window: `========== Publish: 1 succeeded, 0 failed, 0 skipped ==========` to indicate a successful publish. Also, the web app should open in a new browser window.

    You will be prompted to approve the application to allow it to access your Azure Active Directory profile information. Accept the request.

    You should now see a notification that states: **Sorry, but we're having trouble signing you in.**. This is expected. We will add the required redirect URIs to the Azure Active Directory application in the next task.

    ![Sorry, but we're having trouble signing you in.](media/web-app-sign-in-error.png "Sign in error dialog")

    If the web app does not automatically open, you can copy its URL on the publish dialog:

    ![The site URL value is highlighted on the publish dialog.](media/vs-publish-site-url.png "Publish dialog")

> **NOTE:** If the web application displays an error, then go into the Azure Portal for the **IoTWebApp** and click **Restart**. When the Azure Web App is created from the ARM Template and configured for .NET Core, it may need to be restarted for the .NET Core configuration to be fully installed and ready for the application to run. Once restarted, the web application will run as expected.
> ![App Service blade with Restart button highlighted](media/IoTWebApp-App-Service-Restart-Button.png "App Service blade with Restart button highlighted")

> **Further troubleshooting:** If, after restarting the web application more than once, you still encounter a _500_ error, there may be a problem with the system identity for the web app (**please note**, after restarting, you may see a _503_ error for a while, as the web application initializes). To check if this is the issue, open the web application's Configuration and view its Application Settings. Open the **CosmosDBConnection** setting and look at the **Key Vault Reference Details** underneath the setting. You should see an output similar to the following, which displays the secret details and indicates that it is using the _System assigned managed identity_:

![The application setting shows the Key Vault reference details underneath.](media/webapp-app-setting-key-vault-reference.png "Key Vault reference details")

> If you see an error in the Key Vault Reference Details, go to Key Vault and delete the access policy for the web app's system identity. Then go back to the web app, turn off the System Identity, turn it back on (which creates a new one), then re-add it to Key Vault's access policies.

### Task 5: Add new redirect URIs to the Azure AD application

Now that you have deployed the web app, we need to add the redirect URIs in the Azure AD application's Authentication settings. This will allow the web application to successfully incorporate user authentication.

1. Copy the web app's URL you obtained in the previous task. If you cannot find this value, navigate to the web app in the Azure portal, located within the resource group, then copy the URL on the Overview blade.

    ![The URL is highlighted on the Overview blade.](media/web-app-overview-url.png "Overview")

2. Navigate to Azure Active Directory in the Azure portal, then select **App registrations** on the left-hand menu.

    ![The app registrations link is highlighted.](media/aad-app-registrations-link.png "App registrations")

3. Locate and select the **IoTSolutionAcceleratorWebApp** app registration.

    ![The app registration is highlighted.](media/aad-app-registrations.png "App registrations")

4. Select **Authentication** in the left-hand menu. Add two new redirect URIs, using the published web app URL you copied (replace `[YOUR URL]` with the web app's URL):

   - `[YOUR URL]`
   - `[YOUR URL]/signin-oidc`
   - In the **Advanced settings** section set **Logout URL** to `[YOUR URL]/signout-oidc`

    ![The Authentication form is displayed.](media/aad-app-registration-authentication.png "Authentication")

5. Select **Save** to apply your changes.

### Task 6: Update your notification settings in the Web App

When you run the data generator in a later section, the device telemetry flows through the solution, starting with IoT devices sending telemetry to IoT Hub, an Azure Function processing those messages and saving them to Azure Cosmos DB, then the Azure Cosmos DB change feed triggering other Azure Functions for further processing. Inside one of these change feed-triggered functions, the processing logic keeps track of vehicle trip progress, optionally sending an alert notification through the Logic App.

In this task, you sign in to the deployed web app and configure your notification settings.

1. Launch the deployed web app. If you cannot find the URL, navigate to the web app in the Azure portal, located within the resource group, then copy the URL on the Overview blade.

    ![The URL is highlighted on the Overview blade.](media/web-app-overview-url.png "Overview")

2. When prompted, sign in with your Azure account.

    If you try to navigate through the site, you will notice there is no data. We will seed the Azure Cosmos DB `metadata` container with data in the next section.

    ![The Fleet Management web app home page is displayed.](media/webapp-home-page.png "Fleet Management home page")

3. Select **Settings** in the left-hand menu.

4. Enter the email address that you want to receive alerts within the **Recipient Email Address** field. Check which types of alerts you wish to receive, then select a **Send Alert Interval** value. The default value is `Send every alert individually`. This instructs the Function App to send every alert as they occur to the Logic App for email notifications. This type of email contains very detailed information about the trip events, but can quickly flood your inbox. ALternately, select one of the summary email options. These summary emails contain counts of the number of events (trips started, completed, or delayed), as well as any vehicle VINs affected by delays. You can choose whether to receive a summary every 5, 10, 30, or 60 minutes.

    ![The Settings form is displayed in the web app.](media/web-app-settings.png "Settings")

#### Web App code walk-through

The Web App provides a web-based management interface for vehicle, package, trip, and consignment operational data for the sample scenario. You can adapt this web application as you deem necessary for your own scenario. This ASP.NET MVC Core web app demonstrates how to use the Azure Cosmos DB SDK v3.0 to directly communicate with Azure Cosmos DB, highlighting capabilities such as injecting the Azure Cosmos DB client into controllers, performing CRUD operations against the database, and implementing paging of large data sets.

1. Open **Startup.cs** within the **FleetManagementWebApp** project. Scroll down to the bottom of the file to find the following code:

    ```csharp
    CosmosClientBuilder clientBuilder = new CosmosClientBuilder(cosmosDbConnectionString.ServiceEndpoint.OriginalString, cosmosDbConnectionString.AuthKey);
    CosmosClient client = clientBuilder
        .WithConnectionModeDirect()
        .Build();
    CosmosDbService cosmosDbService = new CosmosDbService(client, databaseName, containerName);
    ```

    This code uses the [.NET SDK for Azure Cosmos DB v3](https://github.com/Azure/azure-cosmos-dotnet-v3/) to initialize the `CosmosClient` instance that is added to the `IServiceCollection` as a singleton for dependency injection and object lifetime management.

2. Open **CosmosDBService.cs** under the **Services** folder of the **FleetManagementWebApp** project to find the following code block:

    ```csharp
    var setIterator = query.Where(predicate).Skip(itemIndex).Take(pageSize).ToFeedIterator();
    ```

    Here we are using the newly added `Skip` and `Take` methods on the `IOrderedQueryable` object (`query`) to retrieve just the records for the requested page. The `predicate` represents the LINQ expression passed in to the `GetItemsWithPagingAsync` method to apply filtering.

3. Scroll down a little further to the following code:

    ```csharp
    var count = this._container.GetItemLinqQueryable<T>(allowSynchronousQueryExecution: true, requestOptions: !string.IsNullOrWhiteSpace(partitionKey) ? new QueryRequestOptions { PartitionKey = new PartitionKey(partitionKey) } : null)
        .Where(predicate).Count();
    ```

    In order to know how many pages we need to navigate, we must know the total item count with the current filter applied. To do this, we retrieve a new `IOrderedQueryable` results from the `Container`, pass the filter predicate to the `Where` method, and return the `Count` to the `count` variable. For this to work, you must set `allowSynchronousQueryExecution` to true, which we do with our first parameter to the `GetItemLinqQueryable` method.

4. Open **VehiclesController.cs** under the **Controllers** folder of the **FleetManagementWebApp** project to review the following code:

    ```csharp
    private readonly ICosmosDbService _cosmosDbService;
    private readonly IHttpClientFactory _clientFactory;
    private readonly IConfiguration _configuration;
    private readonly Random _random = new Random();

    public VehiclesController(ICosmosDbService cosmosDbService, IHttpClientFactory clientFactory, IConfiguration configuration)
    {
        _cosmosDbService = cosmosDbService;
        _clientFactory = clientFactory;
        _configuration = configuration;
    }

    public async Task<IActionResult> Index(int page = 1, string search = "")
    {
        if (search == null) search = "";
        //var query = new QueryDefinition("SELECT TOP @limit * FROM c WHERE c.entityType = @entityType")
        //    .WithParameter("@limit", 100)
        //    .WithParameter("@entityType", WellKnown.EntityTypes.Vehicle);
        // await _cosmosDbService.GetItemsAsync<Vehicle>(query);

        var vm = new VehicleIndexViewModel
        {
            Search = search,
            Vehicles = await _cosmosDbService.GetItemsWithPagingAsync<Vehicle>(
                x => x.entityType == WellKnown.EntityTypes.Vehicle &&
                      (string.IsNullOrWhiteSpace(search) ||
                      (x.vin.ToLower().Contains(search.ToLower()) || x.stateVehicleRegistered.ToLower() == search.ToLower())), page, 10)
        };

        return View(vm);
    }
    ```

    We are using dependency injection with this controller, just as we did with one of our Function Apps earlier. The `ICosmosDbService`, `IHttpClientFactory`, and `IConfiguration` services are injected into the controller through the controller's constructor. The `CosmosDbService` is the class whose code you reviewed in the previous step. The `CosmosClient` is injected into it through its constructor.

    The `Index` controller action method uses paging, which it implements by calling the `ICosmosDbService.GetItemsWithPagingAsync` method you updated in the previous step. Using this service in the controller helps abstract the Azure Cosmos DB query implementation details and business rules from the code in the action methods, keeping the controller lightweight and the code in the service reusable across all the controllers.

    Notice that the paging query does not include a partition key, making the Azure Cosmos DB query cross-partition, which is needed to be able to query across all the documents. If this query ends up being used a lot with the passed in `search` value, causing a higher than desired RU usage on the container per execution, then you might want to consider alternate strategies for the partition key, such as a combination of `vin` and `stateVehicleRegistered`. However, since most of our access patterns for vehicles in this container use the VIN, we are using it as the partition key right now. You will see code further down in the method that explicitly pass the partition key value.

5. Scroll down in the `VehiclesController.cs` file to find the following code:

    ```csharp
    await _cosmosDbService.DeleteItemAsync<Vehicle>(item.id, item.partitionKey);
    ```

    Here we are doing a hard delete by completely removing the item. In a real-world scenario, we would most likely perform a soft delete, which means updating the document with a `deleted` property and ensuring all filters exclude items with this property. Plus, we'd soft delete related records, such as trips. Soft deletions make it much easier to recover a deleted item if needed in the future. This is an enhancement you should consider adding to your solution.

## Section 3: Configuring Azure Databricks

> **Please note**: This is an optional component. If you do not need advanced analytics and machine learning in your solution, you may skip this section.

[Azure Databricks](https://azure.microsoft.com/services/databricks/) is a fully-managed, cloud-based Big Data and Machine Learning platform, which empowers developers to accelerate AI and innovation by simplifying the process of building enterprise-grade production data applications. Built as a joint effort by the team that started Apache Spark and Microsoft, Azure Databricks provides data science and engineering teams with a single platform for Big Data processing and Machine Learning.

By combining the power of Databricks, an end-to-end, managed Apache Spark platform optimized for the cloud, with the enterprise scale and security of Microsoft's Azure platform, Azure Databricks makes it simple to run large-scale Spark workloads.

### Task 1: Create Azure Databricks cluster

Contoso Auto wants to use the valuable data they are collecting from their vehicles to make predictions about the health of their fleet to reduce downtime due to maintenance-related issues. One of the predictions they would like to make is whether a vehicle's battery is likely to fail within the next 30 days, based on historical data. They would like to run a nightly batch process to identify vehicles that should be serviced, based on these predictions. They also want to have a way to make a prediction in real time when viewing a vehicle on their fleet management website.

To support this requirement, you will use Apache Spark on Azure Databricks, a fully managed Apache Spark platform optimized to run on Azure. Spark is a unified big data and advanced analytics platform that enables data scientists and data engineers to explore and prepare large amounts of structured and unstructured data, then use that data to train, use, and deploy machine learning models at scale. We will read and write to Azure Cosmos DB, using the `azure-cosmosdb-spark` connector (<https://github.com/Azure/azure-cosmosdb-spark>).

In this task, you will create a new cluster on which data exploration and model deployment tasks will be executed in later sections.

1. In the [Azure portal](https://portal.azure.com), open your lab resource group, then open your **Azure Databricks Service**. The name should start with `iot-databricks`.

   ![The Azure Databricks Service is highlighted in the resource group.](media/resource-group-databricks.png 'Resource Group')

2. Select **Launch Workspace**. Azure Databricks will automatically sign you in through its Azure Active Directory integration.

   ![Launch Workspace](media/databricks-launch-workspace.png 'Launch Workspace')

3. Once in the workspace, select **Clusters** in the left-hand menu, then select **+ Create Cluster**.

   ![Create Cluster is highlighted.](media/databricks-clusters.png 'Clusters')

4. In the **New Cluster** form, specify the following configuration options:

   1. **Cluster Name**: Enter **lab**.
   2. **Cluster Mode**: Select **Standard**.
   3. **Pool**: Select **None**.
   4. **Databricks Runtime Version**: Select **Runtime 6.1 (Scala 2.11, Spark 2.4.4)**.
   5. **Autopilot Options**: Uncheck **Enable autoscaling** and **Terminate after...**, with a value of **120** minutes.
   6. **Worker Type**: Select **Standard_DS3_v2**.
   7. **Driver Type**: Select **Same as worker**.
   8. **Workers**: Enter **1**.

   ![The New Cluster form is displayed with the previously described values.](media/databricks-new-cluster.png 'New Cluster')
   
   **Note** If you failed to create a cluster, try to change the worker type from Standard_DS3_v2 to other VM sizes.

5. Select **Create Cluster**.

6. Before continuing to the next step, verify that your new cluster is running. Wait for the state to change from **Pending** to **Running**

7. Select the **lab** cluster, then select **Libraries**.

8. Select **Install New**.

    ![Navigate to the libraries tab and select `Install New`.](media/databricks-new-library.png 'Adding a new library')

9. In the Install Library dialog, select **Maven** for the Library Source.

10. In the Coordinates field type:

    ```text
    com.microsoft.azure:azure-cosmosdb-spark_2.4.0_2.11:1.4.1
    ```

11. Select **Install**

    ![Populated library dialog for Maven.](media/databricks-install-library-cosmos.png 'Add the Maven library')

12. **Wait** until the library's status shows as **Installed** before continuing.

### Task 2: Configure Key Vault-backed Databricks secret store

Azure Key Vault is used to Securely store and tightly control access to tokens, passwords, certificates, API keys, and other secrets. In addition, secrets that are stored in Azure Key Vault are centralized, giving the added benefits of only needing to update secrets in one place, such as an application key value after recycling the key for security purposes.

When you executed the deployment template at the beginning of this Quickstart guide, a new Azure Key Vault was provisioned. The template went on to store application secrets in Azure Key Vault, then configured the Function Apps and Web App to securely connect to Azure Key Vault by performing the following steps:

- Add secrets to the provisioned Key Vault.
- Create a system-assigned managed identity for each Azure Function App and the Web App to read from the vault.
- Create an access policy in Key Vault with the "Get" secret permission, assigned to each of these application identities.

In this task, you will configure the Key Vault-backed Databricks secret store to securely access these secrets.

Azure Databricks has two types of secret scopes: Key Vault-backed and Databricks-backed. These secret scopes allow you to store secrets, such as database connection strings, securely. If someone tries to output a secret to a notebook, it is replaced by `[REDACTED]`. This helps prevent someone from viewing the secret or accidentally leaking it when displaying or sharing the notebook.

1. Return to the [Azure portal](https://portal.azure.com), which should still be open in another browser tab, then navigate to your Key Vault account and select **Properties** on the left-hand menu.

2. Copy the **DNS Name** and **Resource ID** property values and paste them to Notepad or some other text application that you can reference in a moment.

   ![Properties is selected on the left-hand menu, and DNS Name and Resource ID are highlighted to show where to copy the values from.](media/key-vault-properties.png 'Key Vault properties')

3. Navigate back to the Azure Databricks workspace.

4. In your browser's URL bar, append **#secrets/createScope** to your Azure Databricks base URL (for example, <https://eastus.azuredatabricks.net#secrets/createScope>).

5. Enter `key-vault-secrets` for the name of the secret scope.

6. Select **Creator** within the Manage Principal drop-down to specify only the creator (which is you) of the secret scope has the MANAGE permission.

   > MANAGE permission allows users to read and write to this secret scope, and, in the case of accounts on the Azure Databricks Premium Plan, to change permissions for the scope.

   > Your account must have the Azure Databricks Premium Plan for you to be able to select Creator. This is the recommended approach: grant MANAGE permission to the Creator when you create the secret scope, and then assign more granular access permissions after you have tested the scope.

7. Enter the **DNS Name** (for example, <https://iot-vault.vault.azure.net/>) and **Resource ID** you copied in step 2 above, for example: `/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/cosmos-db-iot/providers/Microsoft.KeyVault/vaults/iot-vault`.

   ![Create Secret Scope form](media/create-secret-scope.png 'Create Secret Scope')

8. Select **Create**.

After a moment, you will see a dialog verifying that the secret scope has been created.

## Section 4: Explore and execute the data generator

In this section, we will explore the data generator project, **FleetDataGenerator**, update the application configuration, and run it in order to seed the metadata database with data and simulate vehicles.

There are several tasks that the data generator performs, depending on the state of your environment. The first task is that the generator will create the Azure Cosmos DB database and containers with the optimal configuration for this lab if these elements do not exist in your Azure Cosmos DB account. When you run the generator in a few moments, this step will be skipped because you already created them at the beginning of the lab. The second task the generator performs is to seed your Azure Cosmos DB `metadata` container with data if no data exists. This includes vehicle, consignment, package, and trip data. Before seeding the container with data, the generator temporarily increases the requested RU/s for the container to 50,000 for optimal data ingestion speed. After the seeding process completes, the RU/s are scaled back down to 15,000.

After the generator ensures the metadata exists, it begins simulating the specified number of vehicles. You are prompted to enter a number between 1 and 5, simulating 1, 10, 50, 100, or the number of vehicles specified in your configuration settings, respectively. For each simulated vehicle, the following tasks take place:

1. An IoT device is registered for the vehicle, using the IoT Hub connection string and setting the device ID to the vehicle's VIN. This returns a generated device key.
2. A new simulated vehicle instance (`SimulatedVehicle`) is added to a collection of simulated vehicles, each acting as an AMQP device and assigned a Trip record to simulate the delivery of packages for a consignment. These vehicles are randomly selected to have their refrigeration units fail and, out of those, some will randomly fail immediately while the others fail gradually.
3. The simulated vehicle creates its own AMQP device instance, connecting to IoT Hub with its unique device ID (VIN) and generated device key.
4. The simulated vehicle asynchronously sends vehicle telemetry information through its connection to IoT Hub continuously until it either completes the trip by reaching the distance in miles established by the Trip record, or receiving a cancellation token.

### How to provision your own devices

Within the data generator, we use the [Azure IoT Hub SDK for .NET](https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/) to directly register and manage devices in Azure IoT Hub. There are also [SDKs available](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks#azure-iot-hub-device-sdks) for C, Java, Node.js, Python, and iOS.

The **DeviceManager.cs** file within the data generator project shows how to use the `Microsoft.Azure.Devices.RegistryManager` to perform create, remove, update, and delete operations on devices. First, we instantiate a new instance of `RegistryManager` from the IoT Hub connection string:

```csharp
// Create an instance of the RegistryManager from the IoT Hub connection string.
registryManager = RegistryManager.CreateFromConnectionString(connectionString);
```

The `RegisterDevicesAsync` method in the `DeviceManager` helper class demonstrates how to register a single device with IoT Hub. First, it creates a new device and sets its state to `Enabled`. Then, it attempts to register the new device. If an exception is returned that a device already exists, we retrieve the registered device, set the status to `Enabled`, and update the device state in IoT Hub with the status change:

```csharp
/// <summary>
/// Register a single device with IoT Hub.
/// </summary>
/// <param name="connectionString"></param>
/// <param name="deviceId"></param>
/// <returns></returns>
public static async Task<string> RegisterDevicesAsync(string connectionString, string deviceId)
{
    //Make sure we're connected
    if (registryManager == null)
        IotHubConnect(connectionString);

    // Create a new device.
    var device = new Device(deviceId) {Status = DeviceStatus.Enabled};

    try
    {
        // Register the new device.
        device = await registryManager.AddDeviceAsync(device);
    }
    catch (Exception ex)
    {
        if (ex is DeviceAlreadyExistsException ||
            ex.Message.Contains("DeviceAlreadyExists"))
        {
            // Device already exists, get the registered device.
            device = await registryManager.GetDeviceAsync(deviceId);

            // Ensure the device is activated.
            device.Status = DeviceStatus.Enabled;

            // Update IoT Hub with the device status change.
            await registryManager.UpdateDeviceAsync(device);
        }
        else
        {
            Program.WriteLineInColor($"An error occurred while registering IoT device '{deviceId}':\r\n{ex.Message}", ConsoleColor.Red);
        }
    }

    // Return the device key.
    return device.Authentication.SymmetricKey.PrimaryKey;
}
```

The `RegisterDevicesAsync` method returns a symmetric key that the registered device uses to authenticate when connecting to IoT Hub. The `deviceId` value is the vehicle's VIN in this case. You can use whatever string value you want for your devices, as long as the values are unique. The `RegisterDevicesAsync` method is called from the `SetupVehicleTelemetryRunTasks` method in the data generator:

```csharp
// Register vehicle IoT device, using its VIN as the device ID, then return the device key.
var deviceKey = await DeviceManager.RegisterDevicesAsync(iotHubConnectionString, trip.vin);
```

Each vehicle IoT device is simulated by the data generator. The simulated device is represented by the `SimulatedVehicle` class (**SimulatedVehicle.cs**). When a new simulated device is instantiated, the device ID (the vehicle's VIN) and the device's symmetric key are passed into the constructor and used when creating a new `MIcrosoft.Azure.Devices.Client.DeviceClient` instance:

```csharp
public SimulatedVehicle(Trip trip, bool causeRefrigerationUnitFailure,
    bool immediateRefrigerationUnitFailure, int vehicleNumber,
    string iotHubUri, string deviceId, string deviceKey)
{
    _vehicleNumber = vehicleNumber;
    _trip = trip;
    _tripId = trip.id;
    _distanceRemaining = trip.plannedTripDistance + 3; // Pad a little bit extra distance to ensure all events captured.
    _causeRefrigerationUnitFailure = causeRefrigerationUnitFailure;
    _immediateRefrigerationUnitFailure = immediateRefrigerationUnitFailure;
    _IotHubUri = iotHubUri;
    DeviceId = deviceId;
    DeviceKey = deviceKey;
    _DeviceClient = DeviceClient.Create(_IotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey(DeviceId, DeviceKey));
}
```

You can update this code to simulate your own IoT devices. When you are ready to **use physical devices**, follow the [tutorials found in the IoT Hub documentation](https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-get-started-physical).

The best way to provision multiple IoT devices in a secure and scalable manner is to use the [Azure IoT Hub Device Provisioning Service](https://docs.microsoft.com/azure/iot-dps/about-iot-dps) (DPS). Use the [Microsoft Azure Provisioning SDKs](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-sdks#microsoft-azure-provisioning-sdks) for the best experience with using DPS.

### Task 1: View the Azure Cosmos DB processing Function App in the portal and copy the Health Check URL

1. In the Azure portal (<https://portal.azure.com>), open the Azure Function App whose name begins with **IoT-CosmosDBProcessing**.

2. Expand the **Functions** list in the left-hand menu, then select **TripProcessor**.

    ![The TripProcessor function is displayed.](media/portal-tripprocessor-function.png "TripProcessor")

3. View the **function.json** file to the right. This file was generated when you published the Function App in Visual Studio. The bindings are the same as you saw in the project code for the function. When new instances of the Function App are created, the generated `function.json` file and a ZIP file containing the compiled application are copied to these instances, and these instances run in parallel to share the load as data flows through the architecture. The `function.json` file instructs each instance how to bind attributes to the functions, where to find application settings, and information about the compiled application (`scriptFile` and `entryPoint`).

4. Select the **HealthCheck** function. This function has an Http trigger that enables users to verify that the Function App is up and running, and that each configuration setting exists and has a value. The data generator calls this function before running.

5. Select **Get function URL**.

    ![The HealthCheck function is selected and the Get function URL link is highlighted.](media/portal-cosmos-function-healthcheck.png "HealthCheck function")

6. **Copy the URL** and save it to Notepad or similar text editor for the section that follows.

    ![The HealthCheck URL is highlighted.](media/portal-cosmos-function-healthcheck-url.png "Get function URL")

### Task 2: View stream processing Function App in the portal and copy the Health Check URL

1. In the Azure portal (<https://portal.azure.com>), open the Azure Function App whose name begins with **IoT-StreamProcessing**.

2. Expand the **Functions** list in the left-hand menu, then select the **HealthCheck** function. Next, select **Get function URL**.

    ![The HealthCheck function is selected and the Get function URL link is highlighted.](media/portal-stream-function-healthcheck.png "HealthCheck")

3. **Copy the URL** and save it to Notepad or similar text editor for the section that follows.

    ![The HealthCheck URL is highlighted.](media/portal-stream-function-healthcheck-url.png "Get function URL")

> **Hint**: You can paste the Health Check URLs into a web browser to check the status at any time. The data generator programmatically accesses these URLs each time it runs, then reports whether the Function Apps are in a failed state or missing important application settings.

### Task 3: Open the data generator project

1. If the Visual Studio solution is not already open, navigate to `C:\solution-accelerator-master\Solution` and open the Visual Studio solution file: **CosmosDbIoTScenario.sln**.

2. Expand the **FleetDataGenerator** project and open **Program.cs** in the Solution Explore

   ![The Program.cs file is highlighted in the Solution Explorer.](media/vs-data-generator-program.png 'Solution Explorer')

#### Code walk-through

There is a lot of code within the data generator project, so we'll just touch on the highlights. The code we do not cover is commented and should be easy to follow if you so desire.

1. Within the **Main** method of **Program.cs**, the core workflow of the data generator is executed by the following code block:

    ```csharp
    // Instantiate Azure Cosmos DB client and start sending messages:
    var trips = new List<Trip>();
    using (_cosmosDbClient = new CosmosClient(cosmosDbConnectionString.ServiceEndpoint.OriginalString,
        cosmosDbConnectionString.AuthKey, connectionPolicy))
    {
        await InitializeCosmosDb();

        // Find and output the container details, including # of RU/s.
        var container = _database.GetContainer(MetadataContainerName);

        var offer = await container.ReadThroughputAsync(cancellationToken);

        if (offer != null)
        {
            var currentCollectionThroughput = offer ?? 0;
            WriteLineInColor(
                $"Found collection `{MetadataContainerName}` with {currentCollectionThroughput} RU/s.",
                ConsoleColor.Green);
        }

        // Ensure the telemetry container throughput is set to 15,000 RU/s.
        var telemetryContainer = await GetContainerIfExists(TelemetryContainerName);
        await ChangeContainerPerformance(telemetryContainer, 15000);

        // Initially seed the Azure Cosmos DB database with metadata if empty or if the user wants to generate new trips.
        await SeedDatabase(cosmosDbConnectionString, generateNewTripsOnly, cancellationToken);
        if (!generateNewTripsOnly)
        {
            trips = await GetTripsFromDatabase(numberSimulatedTrucks, container);
        }
    }

    if (!generateNewTripsOnly)
    {
        try
        {
            // Start sending telemetry from simulated vehicles to Event Hubs:
            _runningVehicleTasks = await SetupVehicleTelemetryRunTasks(numberSimulatedTrucks,
                trips, arguments.IoTHubConnectionString);
            var tasks = _runningVehicleTasks.Select(t => t.Value).ToList();
            while (tasks.Count > 0)
            {
                try
                {
                    Task.WhenAll(tasks).Wait(cancellationToken);
                }
                catch (TaskCanceledException)
                {
                    //expected
                }

                tasks = _runningVehicleTasks.Where(t => !t.Value.IsCompleted).Select(t => t.Value).ToList();

            }
        }
        catch (OperationCanceledException)
        {
            Console.WriteLine("The vehicle telemetry operation was canceled.");
            // No need to throw, as this was expected.
        }
    }
    ```

    The top section of the code instantiates a new `CosmosClient`, using the connection string defined in either `appsettings.json` or the environment variables. The first call within the block is to `InitializeCosmosDb()`. We'll dig into this method in a moment, but it is responsible for creating the Azure Cosmos DB database and containers if they do not exist in the Azure Cosmos DB account. Next, we create a new `Container` instance, which the v3 version of the .NET Azure Cosmos DB SDK uses for operations against a container, such as CRUD and maintenance information. For example, we call `ReadThroughputAsync` on the container to retrieve the current throughput (RU/s), and we pass it to `GetTripsFromDatabase` to read Trip documents from the container, based on the number of vehicles we are simulating. In this method, we also call the `SeedDatabase` method, which checks whether data currently exists and, if not, calls methods in the `DataGenerator` class (`DataGenerator.cs` file) to generate vehicles, consignments, packages, and trips, then writes the data in bulk using the `BulkImporter` class (`BulkImporter.cs` file). This `SeedDatabase` method executes the following on the `Container` instance to adjust the throughput (RU/s) to 50,000 before the bulk import, and back to 15,000 after the data seeding is complete: `await container.ReplaceThroughputAsync(desiredThroughput);`. Also notice that we are passing `generateNewTripsOnly` to the `SeedDatabase` method. This value is set to true if the user selects option 6 when executing the generator. When `generateNewTripsOnly` is set to true, any existing trips and consignments that are in pending or active status are canceled and new trips and consignments are created for existing vehicles. If no data currently exists, the `SeedDatabase` method generates all new data, as usual.

    The `try/catch` block calls `SetupVehicleTelemetryRunTasks` to register IoT device instances for each simulated vehicle and load up the tasks from each `SimulatedVehicle` instance it creates. It uses `Task.WhenAll` to ensure all pending tasks (simulated vehicle trips) are complete, removing completed tasks from the `_runningvehicleTasks` list as they finish. The cancellation token is used to cancel all running tasks if you issue the cancel command (`Ctrl+C` or `Ctrl+Break`) in the console.

2. Scroll down the `Program.cs` file until you find the `InitializeCosmosDb()` method. Here is the code for your reference:

    ```csharp
    private static async Task InitializeCosmosDb()
    {
        _database = await _cosmosDbClient.CreateDatabaseIfNotExistsAsync(DatabaseName);

        #region Telemetry container
        // Define and create a new container using the builder pattern.
        await _database.DefineContainer(TelemetryContainerName, $"/{PartitionKey}")
            // Tune the indexing policy for write-heavy workloads by only including regularly queried paths.
            // Be careful when using an opt-in policy as we are below. Excluding all and only including certain paths removes
            // Azure Cosmos DB's ability to proactively add new properties to the index.
            .WithIndexingPolicy()
                .WithIndexingMode(IndexingMode.Consistent)
                .WithIncludedPaths()
                    .Path("/vin/?")
                    .Path("/state/?")
                    .Path("/partitionKey/?")
                    .Attach()
                .WithExcludedPaths()
                    .Path("/*")
                    .Attach()
                .Attach()
            .CreateIfNotExistsAsync(15000);
        #endregion

        #region Metadata container
        // Define a new container.
        var metadataContainerDefinition =
            new ContainerProperties(id: MetadataContainerName, partitionKeyPath: $"/{PartitionKey}")
            {
                // Set the indexing policy to consistent and use the default settings because we expect read-heavy workloads in this container (includes all paths (/*) with all range indexes).
                // Indexing all paths when you have write-heavy workloads may impact performance and cost more RU/s than desired.
                IndexingPolicy = { IndexingMode = IndexingMode.Consistent }
            };

        // Set initial performance to 50,000 RU/s for bulk import performance.
        await _database.CreateContainerIfNotExistsAsync(metadataContainerDefinition, throughput: 50000);
        #endregion

        #region Maintenance container
        // Define a new container.
        var maintenanceContainerDefinition =
            new ContainerProperties(id: MaintenanceContainerName, partitionKeyPath: $"/vin")
            {
                IndexingPolicy = { IndexingMode = IndexingMode.Consistent }
            };

        // Set initial performance to 400 RU/s due to light workloads.
        await _database.CreateContainerIfNotExistsAsync(maintenanceContainerDefinition, throughput: 400);
        #endregion

        #region Alerts container
        // Define a new container.
        var alertsContainerDefinition =
            new ContainerProperties(id: AlertsContainerName, partitionKeyPath: $"/id")
            {
                IndexingPolicy = { IndexingMode = IndexingMode.Consistent }
            };

        // Set initial performance to 400 RU/s due to light workloads.
        await _database.CreateContainerIfNotExistsAsync(alertsContainerDefinition, throughput: 400);
        #endregion
    }
    ```

    This method creates an Azure Cosmos DB database if it does not already exist, otherwise it retrieves a reference to it (`await _cosmosDbClient.CreateDatabaseIfNotExistsAsync(DatabaseName);`). Then it creates `ContainerProperties` for the `telemetry`, `metadata`, `maintenance`, and `alerts` containers. The `ContainerProperties` object lets us specify the container's indexing policy. We use the default indexing policy for `alerts`, `metadata`, and `maintenance` since they are read-heavy and benefit from a greater number of paths, but we exclude all paths in the `telemetry` index policy, and add paths only to those properties we need to query, due to the container's write-heavy workload. The `telemetry` container is assigned a throughput of 15,000 RU/s, 50,000 for `metadata` for the initial bulk import, then it is scaled down to 15,000, and 400 for `maintenance` and `alerts`.

### Task 4: Update application configuration

The data generator needs two connection strings before it can successfully run; the IoT Hub connection string, and the Azure Cosmos DB connection string. The IoT Hub connection string can be found by selecting **Shared access policies** in IoT Hub, selecting the **iothubowner** policy, then copying the **Connection string--primary key** value. This is different from the Event Hub-compatible endpoint connection string you copied earlier.

![The iothubowner shared access policy is displayed.](media/iot-hub-connection-string.png "IoT Hub shared access policy")

1. Open **appsettings.json** within the **FleetDataGenerator** project.

2. Paste the IoT Hub connection string value in quotes next to the **IOT_HUB_CONNECTION_STRING** key. Paste the Azure Cosmos DB connection string value in quotes next to the **COSMOS_DB_CONNECTION_STRING** key.

    If you do not have the Azure Cosmos DB connection string, you can find it by opening the Azure Cosmos DB account in the solution accelerator's resource group in the portal, then selecting **Keys** in the left-hand menu, then copy the **Primary Connection String** value.

    ![Azure Cosmos DB connection string is highlighted within the Keys blade.](media/cosmos-db-connection-string.png "Keys")

3. The data generator also requires the Health Check URLs you copied in the previous section for the `HealthCheck` functions located in both Function Apps. Paste the Azure Cosmos DB Processing Function App's `HealthCheck` function's URL in quotes next to the **COSMOS_PROCESSING_FUNCTION_HEALTHCHECK_URL** key. Paste the Stream Processing Function App's `HealthCheck` function's URL in quotes next to the **STREAM_PROCESSING_FUNCTION_HEALTHCHECK_URL** key.

    ![The appsettings.json file is highlighted in the Solution Explorer, and the connection strings and health check URLs are highlighted within the file.](media/vs-appsettings.png "appsettings.json")

    The NUMBER_SIMULATED_TRUCKS value is used when you select option 5 when you run the generator. This gives you the flexibility to simulate between 1 and 1,000 trucks at a time. SECONDS_TO_LEAD specifies how many seconds to wait until the generator starts generating simulated data. The default value is 0. SECONDS_TO_RUN forces the simulated trucks to stop sending generated data to IoT Hub. The default value is 14400. Otherwise, the generator stops sending tasks when all the trips complete or you cancel by entering `Ctrl+C` or `Ctrl+Break` in the console window.

3. **Save** the `appsettings.json` file.

> As an alternative, you may save these settings as environment variables on your machine, or through the FleetDataGenerator properties. Doing this will remove the risk of accidentally saving your secrets to source control.

### Task 5: Run generator

In this task, you will run the generator and have it generate events for 50 trucks. The reason we are generating events for so many vehicles is two-fold:

- In the next section, we will observe the function triggers and event activities with Application Insights.
- We need to have completed trips prior to performing batch predictions in a later section.

> **Warning**: You will receive a lot of emails when the generator starts sending vehicle telemetry. If you do not wish to receive emails, simply disable the Logic App you created.

1. Within Visual Studio, right-click on the **FleetDataGenerator** project in the Solution Explorer and select **Set as Startup Project**. This will automatically run the data generator each time you debug.

    ![Set as Startup Project is highlighted in the Solution Explorer.](media/vs-set-startup-project.png "Solution Explorer")

2. Select the Debug button at the top of the Visual Studio window or hit **F5** to run the data generator.

    ![The debug button is highlighted.](media/vs-debug.png "Debug")

3. When the console window appears, enter **3** to simulate 50 vehicles. The generator will perform the Function App health checks, resize the requested throughput for the `metadata` container, use the bulk importer to seed the container, and resize the throughput back to 15,000 RU/s.

    ![3 has been entered in the console window.](media/cmd-run.png "Generator")

4. After the seeding is completed the generator will retrieve 50 trips from the database, sorted by shortest trip distance first so we can have completed trip data appear faster. You will see a message output for every 50 events sent, per vehicle with their VIN, the message count, and the number of miles remaining for the trip. For example: `Vehicle 19: C1OVHZ8ILU8TGGPD8 Message count: 3650 -- 3.22 miles remaining`. **Let the generator run in the background and continue to the next section**.

    ![Vehicle simulation begins.](media/cmd-simulated-vehicles.png "Generator")

5. As the vehicles complete their trips, you will see a message such as `Vehicle 37 has completed its trip`.

    ![A completed messages is displayed in the generator console.](media/cmd-vehicle-completed.png "Generator")

6. When the generator completes, you will see a message to this effect.

    ![A generation complete message is displayed in the generator console.](media/cmd-generator-completed.png "Generator")

If the health checks fail for the Function Apps, the data generator will display a warning, oftentimes telling you which application settings are missing. The data generator will not run until the health checks pass.

![The failed health checks are highlighted.](media/cmd-healthchecks-failed.png "Generator")

### Task 6: View devices in IoT Hub

The data generator registered and activated each simulated vehicle in IoT Hub as a device. In this task, you will open IoT Hub and view these registered devices.

1. In the Azure portal (<https://portal.azure.com>), open the IoT Hub instance within your **cosmos-db-iot** resource group.

    ![The IoT Hub resource is displayed in the resource group.](media/portal-resource-group-iot-hub.png "IoT Hub")

2. Select **IoT devices** in the left-hand menu. You will see all 50 IoT devices listed in the IoT devices pane to the right, with the VIN specified as the device ID. When we simulate more vehicles, we will see additional IoT devices registered here.

    ![The IoT devices pane is displayed.](media/iot-hub-iot-devices.png "IoT devices")

## Section 5: Observe Change Feed using Azure Functions and App Insights

In this section, we use the Live Metrics Stream feature of Application Insights to view the incoming requests, outgoing requests, overall health, allocated server information, and sample telemetry in near-real-time. The Live Metrics Stream helps you observe how your functions scale under load and allow you to spot any potential bottlenecks or problematic components, through a single interactive interface.

[Application Insights](https://docs.microsoft.com/azure/azure-monitor/app/app-insights-overview), a feature of Azure Monitor, is an extensible Application Performance Management (APM) service for developers and DevOps professionals. Use it to monitor your live applications. It will automatically detect performance anomalies and includes powerful analytics tools to help you diagnose issues and to understand what users actually do with your app. It's designed to help you continuously improve performance and usability. It works for apps on a wide variety of platforms including .NET, Node.js and Java EE, hosted on-premises, hybrid, or any public cloud. It integrates with your DevOps process and has connection points to a variety of development tools. It can monitor and analyze telemetry from mobile apps by integrating with Visual Studio App Center.

### Task 1: Open App Insights Live Metrics Stream

1. In the Azure portal (<https://portal.azure.com>), open the Application Insights instance within your **cosmos-db-iot** resource group.

    ![The App Insights resource is displayed in the resource group.](media/portal-resource-group-app-insights.png "Application Insights")

2. Select **Live Metrics Stream** in the left-hand menu.

    ![The Live Metrics Stream link is displayed in the left-hand menu.](media/app-insights-live-metrics-stream-link.png "Application Insights")

3. Observe the metrics within the Live Metrics Stream as data flows through the system.

    ![The Live Metrics Stream page is displayed.](media/app-insights-live-metrics-stream.png "Live Metrics Stream")

    At the top of the page, you will see a server count. This shows how many instances of the Function Apps there are, and one server is allocated to the Web App. As the Function App server instances exceed computational, memory, or request duration thresholds, and as the IoT Hub and Change Feed queues grow and age, new instances are automatically allocated to scale out the Function Apps. You can view the server list at the bottom of the page. On the right-hand side, you will see sample telemetry, including messages sent to the logger within the functions. Here we highlighted a message stating that the Azure Cosmos DB Processing function is sending 100 Azure Cosmos DB records to Event Hubs.

    While observing the live stream, you may notice many dependency call failures (404). These can be safely ignored. They are caused by the Azure Storage binding used in the **ColdStorage** function within the Azure Cosmos DB Processing Function App. This binding checks if the file exists before writing to the specified container. Since we are writing new files, you will see a `404` message for every file that is written since it does not exist. Currently, the binding engine does not know the difference between "good" 404 messages such as these, and "bad" ones.

## Section 6: Observe data using the Azure Cosmos DB Data Explorer and Web App

The Azure Cosmos DB Data Explorer is a web-based interface that allows you to view and manage the data stored in Azure Cosmos DB. Alternately, you can use the [Azure Cosmos DB explorer](https://docs.microsoft.com/azure/cosmos-db/data-explorer) stand-alone interface to perform the same tasks.

### Task 1: View data in Azure Cosmos DB Data Explorer

1. In the Azure portal (<https://portal.azure.com>), open the Azure Cosmos DB instance within your **cosmos-db-iot** resource group.

2. Select **Data Explorer** in the left-hand menu.

3. Expand the **ContosoAuto** database, then expand the **metadata** container. Select **Items** to view a list of documents stored in the container. Select one of the items to view the data.

    ![The data explorer is displayed with a selected item in the metadata container's items list.](media/cosmos-data-explorer-metadata-items.png "Data Explorer")

4. Select the ellipses (...) to the right of the **metadata** container name, then select **New SQL Query**.

    ![The New SQL Query menu item is highlighted.](media/cosmos-data-explorer-metadata-new-sql-query.png "New SQL Query")

5. Replace the query with the following:

    ```sql
    SELECT * FROM c WHERE c.entityType = 'Vehicle'
    ```

6. Execute the query to view the first 100 vehicle records.

    ![The query editor is displayed with the vehicle results.](media/cosmos-vehicle-query.png "Vehicle query")

7. Update the query to find trip records where the trip is completed.

    ```sql
    SELECT * FROM c WHERE c.entityType = 'Trip' AND c.status = 'Completed'
    ```

    ![The query editor is displayed with the trip results.](media/cosmos-trip-completed-query.png "Trip query")

    Please note, you may not have any trips that have completed yet. Try querying where the `status` = **Active** instead. Active trips are those that are currently running.

    Here is an example completed trip record (several packages removed for brevity):

    ```json
    {
        "partitionKey": "DK6JW0RNF0G9PO2FJ",
        "id": "eb96c44e-4c1d-4f54-bdea-e7d2f927009c",
        "entityType": "Trip",
        "vin": "DK6JW0RNF0G9PO2FJ",
        "consignmentId": "e1da2e74-bf37-4773-a5bf-483fc08533ac",
        "plannedTripDistance": 18.33,
        "location": "AR",
        "odometerBegin": 106841,
        "odometerEnd": 106859.36,
        "temperatureSetting": 19,
        "tripStarted": "2019-09-20T14:39:24.1855725Z",
        "tripEnded": "2019-09-20T14:54:53.7558481Z",
        "status": "Completed",
        "timestamp": "0001-01-01T00:00:00",
        "packages": [
            {
                "packageId": "a5651f48-67d5-4c1b-b7d9-80d678aabe9b",
                "storageTemperature": 30,
                "highValue": false
            },
            {
                "packageId": "b2185628-eb0e-49b9-8b7d-685fcdcb5a36",
                "storageTemperature": 22,
                "highValue": false
            },
            {
                "packageId": "25ac4bd1-5aad-4030-91f7-9539cc15b441",
                "storageTemperature": 31,
                "highValue": true
            }
        ],
        "consignment": {
            "consignmentId": "e1da2e74-bf37-4773-a5bf-483fc08533ac",
            "customer": "Fabrikam, Inc.",
            "deliveryDueDate": "2019-09-20T17:50:40.3291024Z"
        },
        "_rid": "hM5HAOavCggb5QAAAAAAAA==",
        "_self": "dbs/hM5HAA==/colls/hM5HAOavCgg=/docs/hM5HAOavCggb5QAAAAAAAA==/",
        "_etag": "\"2d0364cc-0000-0700-0000-5d84e83d0000\"",
        "_attachments": "attachments/",
        "_ts": 1568991293
    }
    ```

    Portions of the package and consignment records are included since they are often used in trip queries and reports.

### Task 2: Search and view data in Web App

1. Navigate to your deployed Fleet Management web app. If you closed it earlier, you can find the deployment URL in the Overview blade of your Web App (**IoTWebApp**) in the portal.

    ![The web app's URL is highlighted.](media/webapp-url.png "Web App overview")

2. Select **Vehicles**. Here you will see the paging capabilities at work.

    ![The vehicles page is displayed.](media/webapp-vehicles.png "Vehicles")

3. Select one of the vehicles to view the details. On the right-hand side of the details page are the trips assigned to the vehicle. This view provides the customer name from the associated consignment record, aggregate information for the packages, and the trip details.

    ![The vehicle details are displayed.](media/webapp-vehicle-details.png "Vehicle details")

4. Go back to the vehicles list and enter a search term, such as **MT**. This will search both the state registered, and the VIN, including partial matches. Feel free to search for both states and VINs. In the screenshot below, we searched for `MT` and received results for Montana state registrations, and had a record where `MT` was included in the VIN.

    ![The search results are displayed.](media/webapp-vehicle-search.png "Vehicle search")

5. Select **Consignments** in the left-hand menu, then enter **alpine ski** in the search box and execute. You should see several consignments for the `Alpine Ski House` customer. You can also search by Consignment ID. In our results, one of the consignments has a status of Completed.

    ![The search results are displayed.](media/webapp-consignments-search.png "Consignments")

6. Select a consignment to view the details. The record shows the customer, delivery due date, status, and package details. The package statistics contains aggregates to calculate the total number of packages, the required storage temperature, based on the package with the lowest storage temperature setting, the total cubic feet and combined gross weight of the packages, and whether any of the packages are considered high value.

    ![The consignment details page is displayed.](media/webapp-consignment-details.png "Consignment details")

7. Select **Trips** in the left-hand menu. Use the filter at the top of the page to filter trips by status, such as Pending, Active, Delayed, and Completed. Trips are delayed if the status is not Completed prior to the delivery due date. You may not see any delayed at this point, but you may have some that become delayed when you re-run the data generator later. You can view the Vehicle or related Consignment record from this page.

    ![The search results are displayed.](media/webapp-trips-search.png "Trips")

## Section 7: Perform CRUD operations using the Web App

In this section, you will insert, update, and delete a vehicle record.

### Task 1: Create a new vehicle

1. In the web app, navigate to the **Vehicles** page, then select **Create New Vehicle**.

    ![The Create New Vehicle button is highlighted on the vehicles page.](media/webapp-vehicles-new-button.png "Vehicles")

2. Complete the Create Vehicle form with the following VIN: **ISO4MF7SLBXYY9OZ3**. When finished filling out the form, select **Create**.

    ![The Create Vehicle form is displayed.](media/webapp-create-vehicle.png "Create Vehicle")

### Task 2: View and edit the vehicle

1. Search for your new vehicle in the Vehicles page by pasting the VIN in the search box: **ISO4MF7SLBXYY9OZ3**.

    ![The VIN is pasted in the search box and the vehicle result is displayed.](media/webapp-vehicles-search-vin.png "Vehicles")

2. Select the vehicle in the search results. Select **Edit Vehicle** in the vehicle details page.

    ![Details for the new vehicle are displayed and the edit vehicle button is highlighted.](media/webapp-vehicles-details-new.png "Vehicle details")

3. Update the record by changing the state registered and any other field, then select **Update**.

    ![The Edit Vehicle form is displayed.](media/webapp-vehicles-edit.png "Edit Vehicle")

### Task 3: Delete the vehicle

1. Search for your new vehicle in the Vehicles page by pasting the VIN in the search box: **ISO4MF7SLBXYY9OZ3**. You should see the registered state any any other fields you updated have changed.

    ![The VIN is pasted in the search box and the vehicle result is displayed.](media/webapp-vehicles-search-vin-updated.png "Vehicles")

2. Select the vehicle in the search results. Select **Delete** in the vehicle details page.

    ![Details for the new vehicle are displayed and the delete button is highlighted.](media/webapp-vehiclde-details-updated.png "Vehicle details")

3. In the Delete Vehicle confirmation page, select **Delete** to confirm.

    ![The Delete Vehicle confirmation page is displayed.](media/webapp-vehicles-delete-confirmation.png "Delete Vehicle")

4. Search for your new vehicle in the Vehicles page by pasting the VIN in the search box: **ISO4MF7SLBXYY9OZ3**. You should see that no vehicles are found.

    ![The vehicle was not found.](media/webapp-vehicles-search-deleted.png "Vehicles")

## Section 8: Create the Fleet status real-time dashboard in Power BI

[Microsoft Power BI](https://powerbi.microsoft.com) is a business analytics service that provides interactive visualizations with self-service business intelligence capabilities, enabling end-users to create reports and dashboards by themselves without having to depend on information technology staff or database administrators.

> **Important**: If the data generator is no longer running or sending new telemetry, be sure to start it before continuing. Simulating 50 vehicles should suffice for this section.

### Task 1: Launch Power BI online and create the dashboard

1. Browse to <https://powerbi.microsoft.com> and sign in with the same account you used when you created the Power BI output in Stream Analytics.

2. Select **My workspace**, then select the **Datasets** tab. You should see the **Contoso Auto IoT Events** dataset. This is the dataset you defined in the Stream Analytics Power BI output.

   ![The Contoso Auto IoT dataset is displayed.](media/powerbi-datasets.png 'Power BI Datasets')

3. Select **+ Create** at the top of the page, then select **Dashboard**.

   ![The Create button is highlighted at the top of the page, and the Dashboard menu item is highlighted underneath.](media/powerbi-create-dashboard.png 'Create Dashboard')

4. Provide a name for the dashboard, such as `Contoso Auto IoT Live Dashboard`, then select **Create**.

   ![The create dashboard dialog is displayed.](media/powerbi-create-dashboard-dialog.png 'Create dashboard dialog')

5. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

   ![The add tile dialog is displayed.](media/power-bi-dashboard-add-tile.png 'Add tile')

6. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

   ![The Contoso Auto IoT Events dataset is selected.](media/power-bi-dashboard-add-tile-dataset.png 'Your datasets')

   > **Important**: If the **Contoso Auto IoT Events** data set does not appear, it is because there is a lag time of several minutes between when you first configure the Stream Analytics Power BI output and when data first appears in the streaming data set. Please ensure the data generator is running and that you have started the Stream Analytics query. Also, you may try restarting the Function App as well.

7. Select the **Card** Visualization Type. Under fields, select **+ Add value**, then select **oilAnomaly** from the dropdown. Select **Next**.

   ![The oilAnomaly field is added.](media/power-bi-dashboard-add-tile-oilanomaly.png 'Add a custom streaming data tile')

8. Leave the values at their defaults for the tile details form, then select **Apply**.

   ![The apply button is highlighted on the tile details form.](media/power-bi-dashboard-tile-details.png 'Tile details')

9. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

10. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

11. Select the **Card** Visualization Type. Under fields, select **+ Add value**, then select **engineTempAnomaly** from the dropdown. Select **Next**.

12. Leave the values at their defaults for the tile details form, then select **Apply**.

13. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

14. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

15. Select the **Card** Visualization Type. Under fields, select **+ Add value**, then select **aggressiveDriving** from the dropdown. Select **Next**.

16. Leave the values at their defaults for the tile details form, then select **Apply**.

17. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

18. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

19. Select the **Card** Visualization Type. Under fields, select **+ Add value**, then select **refrigerationTempAnomaly** from the dropdown. Select **Next**.

20. Leave the values at their defaults for the tile details form, then select **Apply**.

21. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

22. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

23. Select the **Card** Visualization Type. Under fields, select **+ Add value**, then select **eventCount** from the dropdown. Select **Next**.

24. Leave the values at their defaults for the tile details form, then select **Apply**.

25. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

26. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

27. Select the **Line chart** Visualization Type. Under Axis, select **+ Add value**, then select **snapshot** from the dropdown. Under Values, select **+Add value**, then select **engineTemperature**. Leave the time window to display at 1 minute. Select **Next**.

    ![The engineTemperature field is added.](media/power-bi-dashboard-add-tile-enginetemperature.png 'Add a custom streaming data tile')

28. Leave the values at their defaults for the tile details form, then select **Apply**.

29. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

30. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

31. Select the **Line chart** Visualization Type. Under Axis, select **+ Add value**, then select **snapshot** from the dropdown. Under Values, select **+Add value**, then select **refrigerationUnitTemp**. Leave the time window to display at 1 minute. Select **Next**.

32. Leave the values at their defaults for the tile details form, then select **Apply**.

33. Above the new dashboard, select **+ Add tile**, then select **Custom Streaming Data** in the dialog, then select **Next**.

34. Select your **Contoso Auto IoT Events** dataset, then select **Next**.

35. Select the **Line chart** Visualization Type. Under Axis, select **+ Add value**, then select **snapshot** from the dropdown. Under Values, select **+Add value**, then select **speed**. Leave the time window to display at 1 minute. Select **Next**.

36. Leave the values at their defaults for the tile details form, then select **Apply**.

37. When you are done, rearrange the tiles as shown:

    ![The tiles have been rearranged.](media/power-bi-dashboard-rearranged.png 'Power BI dashboard')

38. If the data generator is finished sending events, you may notice that tiles on the dashboard are empty. If so, start the data generator again, this time selecting **option 1** for one vehicle. If you do this, the refrigeration temperature anomaly is guaranteed, and you will see the refrigeration unit temperature gradually climb above the 22.5 degree Fahrenheit alert threshold. Alternatively, you may opt to simulate more vehicles and observe the high event count numbers.

    ![The live dashboard is shown with events.](media/power-bi-dashboard-live-results.png "Power BI dashboard")

    After the generator starts sending vehicle telemetry, the dashboard should start working after a few seconds. In this screenshot, we are simulating 50 vehicles with 2,486 events in the last 10 seconds. You may see a higher or lower value for the `eventCount`, depending on the speed of your computer on which you are running the generator, your network speed and latency, and other factors.

## Section 9: Create the Trip/Consignment Status reports in Power BI

In this section, you will import a Power BI report that has been created for you. After opening it, you will update the data source to point to your Power BI instance.

### Task 1: Import report in Power BI Desktop

1. Open **Power BI Desktop**, then select **Open other reports**.

    ![The Open other reports link is highlighted.](media/pbi-splash-screen.png "Power BI Desktop")

2. In the Open report dialog, browse to `C:\solution-accelerator-master\Reports`, then select **FleetReport.pbix**. Click **Open**.

    ![The FleetReport.pbix file is selected in the dialog.](media/pbi-open-report.png "Open report dialog")

### Task 2: Update report data sources

1. After the report opens, click on **Edit Queries** in the ribbon bar within the Home tab.

    ![The Edit Queries button is highlighted.](media/pbi-edit-queries-button.png "Edit Queries")

2. Select **Trips** in the Queries list on the left, then select **Source** under Applied Steps. Click the gear icon next to Source.

    ![The Trip query is selected and the source configuration icon is highlighted.](media/pbi-queries-trips-source.png "Edit Queries")

3. In the source dialog, update the Azure Cosmos DB **URL** value with your Azure Cosmos DB URI you copied earlier in the lab, then click **OK**. If you need to find this value, navigate to your Azure Cosmos DB account in the portal, select Keys in the left-hand menu, then copy the URI value.

    ![The Trips source dialog is displayed.](media/pbi-queries-trips-source-dialog.png "Trips source dialog")

    The Trips data source has a SQL statement defined that returns only the fields we need, and applies some aggregates:

    ```sql
    SELECT c.id, c.vin, c.consignmentId, c.plannedTripDistance,
    c.location, c.odometerBegin, c.odometerEnd, c.temperatureSetting,
    c.tripStarted, c.tripEnded, c.status,
    (
        SELECT VALUE Count(1) 
        FROM n IN c.packages
    ) AS numPackages,
    (
        SELECT VALUE MIN(n.storageTemperature) 
        FROM n IN c.packages
    ) AS packagesStorageTemp,
    (
        SELECT VALUE Count(1)
        FROM n IN c.packages
        WHERE n.highValue = true
    ) AS highValuePackages,
    c.consignment.customer,
    c.consignment.deliveryDueDate
    FROM c where c.entityType = 'Trip'
    and c.status in ('Active', 'Delayed', 'Completed')
    ```

4. When prompted, enter the Azure Cosmos DB **Account key** value, then click **Connect**. If you need to find this value, navigate to your Azure Cosmos DB account in the portal, select Keys in the left-hand menu, then copy the Primary Key value.

    ![The Azure Cosmos DB account key dialog is displayed.](media/pbi-queries-trips-source-dialog-account-key.png "Azure Cosmos DB account key dialog")

5. In a moment, you will see a table named **Document** that has several rows whose value is Record. This is because Power BI doesn't know how to display the JSON document. The document has to be expanded. After expanding the document, you want to change the data type of the numeric and date fields from the default string types, so you can perform aggregate functions in the report. These steps have already been applied for you. Select the **Changed Type** step under Applied Steps to see the columns and changed data types.

    ![The Trips table shows Record in each row.](media/pbi-queries-trips-updated.png "Queries")

    The screenshot below shows the Trips document columns with the data types applied:

    ![The Trips document columns are displayed with the changed data types.](media/pbi-queries-trips-changed-type.png "Trips with changed types")

6. Select **VehicleAverages** in the Queries list on the left, then select **Source** under Applied Steps. Click the gear icon next to Source.

    ![The VehicleAverages query is selected and the source configuration icon is highlighted.](media/pbi-queries-vehicleaverages-source.png "Edit Queries")

7. In the source dialog, update the Azure Cosmos DB **URL** value with your Azure Cosmos DB URI, then click **OK**.

    ![The VehicleAverages source dialog is displayed.](media/pbi-queries-vehicleaverages-source-dialog.png "Trips source dialog")

    The VehicleAverages data source has the following SQL statement defined:

    ```sql
    SELECT c.vin, c.engineTemperature, c.speed,
    c.refrigerationUnitKw, c.refrigerationUnitTemp,
    c.engineTempAnomaly, c.oilAnomaly, c.aggressiveDriving,
    c.refrigerationTempAnomaly, c.snapshot
    FROM c WHERE c.entityType = 'VehicleAverage'
    ```

8. If prompted, enter the Azure Cosmos DB **Account key** value, then click **Connect**. You may not be prompted since you entered the key in an earlier step.

    ![The Azure Cosmos DB account key dialog is displayed.](media/pbi-queries-trips-source-dialog-account-key.png "Azure Cosmos DB account key dialog")

9. Select **VehicleMaintenance** in the Queries list on the left, then select **Source** under Applied Steps. Click the gear icon next to Source.

    ![The VehicleMaintenance query is selected and the source configuration icon is highlighted.](media/pbi-queries-vehiclemaintenance-source.png "Edit Queries")

10. In the source dialog, update the Azure Cosmos DB **URL** value with your Azure Cosmos DB URI, then click **OK**.

    ![The VehicleMaintenance source dialog is displayed.](media/pbi-queries-vehiclemaintenance-source-dialog.png "Trips source dialog")

    The VehicleMaintenance data source has the following SQL statement defined, which is simpler than the other two since there are no other entity types in the `maintenance` container, and no aggregates are needed:

    ```sql
    SELECT c.vin, c.serviceRequired FROM c
    ```

11. If prompted, enter the Azure Cosmos DB **Account key** value, then click **Connect**. You may not be prompted since you entered the key in an earlier step.

    ![The Azure Cosmos DB account key dialog is displayed.](media/pbi-queries-trips-source-dialog-account-key.png "Azure Cosmos DB account key dialog")

12. If you are prompted, click **Close & Apply**.

    ![The Close & Apply button is highlighted.](media/pbi-close-apply.png "Close & Apply")

### Task 3: Explore report

1. The report will apply changes to the data sources and the cached data set will be updated in a few moments. Explore the report, using the slicers (status filter, customer filter, and VIN list) to filter the data for the visualizations. Also be sure to select the different tabs at the bottom of the report, such as Maintenance for more report pages.

    ![The report is displayed.](media/pbi-updated-report.png "Updated report")

2. Select a customer from the Customer Filter, which acts as a slicer. This means when you select an item, it applies a filter to the other items on the page and linked pages. After selecting a customer, you should see the map and graphs change. You will also see a filtered list of VINs and Status. Select the **Details** tab.

    ![A customer record is selected, and an arrow is pointed at the Details tab.](media/pbi-customer-slicer.png "Customer selected")

3. The Details page shows related records, filtered on the selected customer and/or VIN. Now select the **Trips** tab.

    ![The details page is displayed.](media/pbi-details-tab.png "Details")

4. The Trips page shows related trip information. Select **Maintenance**.

    ![The trips page is displayed.](media/pbi-trips-tab.png "Trips")

5. The Maintenance page should contain no data at this time. This page shows information from a batch scoring Machine Learning notebook that you can optionally execute in Databricks in the next section.

6. If at any time you have a number of filters set and you cannot see records, **Ctrl+Click** the **Clear Filters** button on the main report page (Trip/Consignments).

    ![The Clear Filters button is highlighted.](media/pbi-clear-filters.png "Clear Filters")

7. If your data generator is running while viewing the report, you can update the report with new data by clicking the **Refresh** button at any time.

    ![The refresh button is highlighted.](media/pbi-refresh.png "Refresh")

## Section 10: Run the predictive maintenance batch scoring

> **Please note**: This is an optional component. If you do not need advanced analytics and machine learning in your solution, you may skip this section.

In this section, you will import Databricks notebooks into your Azure Databricks workspace. A notebook is interactive and runs in any web browser, mixing markup (formatted text with instructions), executable code, and outputs from running the code.

Next, you will run the Batch Scoring notebook to make battery failure predictions on vehicles, using vehicle and trip data stored in Azure Cosmos DB.

### About Azure Machine Learning

Within the Databricks notebooks you are about to import and run, we use [Azure Machine Learning](https://docs.microsoft.com/azure/machine-learning/service/overview-what-is-azure-ml) to manage, train, and deploy a custom machine learning (ML) model. Azure Machine Learning is a fully managed cloud service used to train, deploy, and manage machine learning models at scale. Given the variety of services within Azure that you can choose from to create AI solutions, Azure Machine Learning is the one platform in Azure that "glues" together the entire custom AI/ML development story. When you couple the rich set of tools with the service, you have everything you need to get started with experimenting and creating AI solutions on the right-hand side of the AI spectrum.

Azure Machine Learning fully supports open-source technologies so that you can use tens of thousands of open-source Python packages such as TensorFlow, PyTorch, MXNet, and scikit-learn. All you need is a Python-enabled environment to get started with setting up and using Azure Machine Learning through its [Python SDK](https://docs.microsoft.com/python/api/overview/azure/ml/intro?view=azure-ml-py). Powerful tools are also available, such as [notebook VMs](https://docs.microsoft.com/azure/machine-learning/service/how-to-configure-environment#notebookvm), [Azure notebooks](https://notebooks.azure.com/), [Jupyter notebooks](http://jupyter.org), or the [Azure Machine Learning for Visual Studio Code](https://aka.ms/vscodetoolsforai) extension to make it easy to explore and transform data, and then train and deploy models. Azure Machine Learning includes features that automate model generation and tuning with ease, efficiency, and accuracy.

Use Azure Machine Learning to train, deploy, and manage machine learning models using Python and CLI at cloud scale. For a low-code or no-code option, use the interactive, [visual interface](https://docs.microsoft.com/azure/machine-learning/service/ui-quickstart-run-experiment) to easily and quickly build, test, and deploy models using pre-built machine learning algorithms.

### Task 1: Import lab notebooks into Azure Databricks

In this task, you will import the Databricks notebooks into your workspace.

1. In the [Azure portal](https://portal.azure.com), open your lab resource group, then open your **Azure Databricks Service**. The name should start with `iot-databricks`.

   ![The Azure Databricks Service is highlighted in the resource group.](media/resource-group-databricks.png 'Resource Group')

2. Select **Launch Workspace**. Azure Databricks will automatically sign you in through its Azure Active Directory integration.

   ![Launch Workspace](media/databricks-launch-workspace.png 'Launch Workspace')

3. Select **Workspace**, select **Users**, select the dropdown to the right of your username, then select **Import**.

   ![The Import link is highlighted in the Workspace.](media/databricks-import-link.png 'Workspace')

4. Select **URL** next to **Import from**, paste the following into the text box: `https://github.com/AzureCosmosDB/solution-accelerator/blob/master/Notebooks/01%20IoT.dbc`, then select **Import**.

   ![The URL has been entered in the import form.](media/databricks-import.png 'Import Notebooks')

5. After importing, select your username. You will see a new folder named `01 IoT`, which contains two notebooks, and a sub-folder named `Includes`, which contains one notebook.

    ![The imported notebooks are displayed.](media/databricks-notebooks.png 'Imported notebooks')

6. Open the **Shared-Configuration** notebook located in the `Includes` sub-folder and provide values for your Machine Learning workspace. You can find these values within the Overview blade of your Machine Learning workspace that is located in your lab resource group.

    The values highlighted in the screenshot below are for the following variables in the notebooks:

    1. `subscription_id`
    2. `resource_group`
    3. `workspace_name`
    4. `workspace_region`

    ![The required values are highlighted.](media/machine-learning-workspace-values.png "Machine Learning service workspace values")

### Task 2: Run batch scoring notebook

In this task, you will run the `Batch Scoring` notebook, using a pre-trained machine learning (ML) model to determine if the battery needs to be replaced on several vehicles within the next 30 days. The notebook performs the following actions:

1. Installs required Python libraries.
2. Connects to Azure Machine Learning (Azure ML).
3. Downloads a pre-trained ML model, saves it to Azure ML, then uses that model for batch scoring.
4. Uses the Azure Cosmos DB Spark connector to retrieve completed Trips and Vehicle metadata from the `metadata` Azure Cosmos DB container, prepares the data using SQL queries, then surfaces the data as temporary views.
5. Applies predictions against the data, using the pre-trained model.
6. Saves the prediction results in the Azure Cosmos DB `maintenance` container for reporting purposes.

To run this notebook, perform the following steps:

1. In Azure Databricks, select **Workspace**, select **Users**, then select your username.

2. Select the `01 IoT` folder, then select the **Batch Scoring** notebook to open it.

   ![The Batch Scoring notebook is highlighted.](media/databricks-batch-scoring-notebook.png 'Workspace')

3. Before you can execute the cells in this or the other notebooks for this lab, you must first attach your Databricks cluster. Expand the dropdown at the top of the notebook where you see **Detached**. Select your lab cluster to attach it to the notebook. If it is not currently running, you will see an option to start the cluster.

   ![The screenshot displays the lab cluster selected for attaching to the notebook.](media/databricks-notebook-attach-cluster.png 'Attach cluster')

4. You may use keyboard shortcuts to execute the cells, such as **Ctrl+Enter** to execute a single cell, or **Shift+Enter** to execute a cell and move to the next one below.

In both notebooks, you will be required to provide values for your Machine Learning workspace. You can find these values within the Overview blade of your Machine Learning workspace that is located in your lab resource group.

The values highlighted in the screenshot below are for the following variables in the notebooks:

1. `subscription_id`
2. `resource_group`
3. `workspace_name`
4. `workspace_region`

![The required values are highlighted.](media/machine-learning-workspace-values.png "Machine Learning service workspace values")

> If you wish to execute this notebook on a scheduled basis, such as every evening, you can use the Jobs feature in Azure Databricks to accomplish this.

## Section 11: Deploy the predictive maintenance web service

> **Please note**: This is an optional component. If you do not need advanced analytics and machine learning in your solution, you may skip this section.

In addition to batch scoring, Contoso Auto would like to predict battery failures on-demand in real time for any given vehicle. They want to be able to call the model from their Fleet Management website when looking at a vehicle to predict whether that vehicle's battery may fail in the next 30 days.

In the previous task, you executed a notebook that used a pre-trained ML model to predict battery failures for all vehicles with trip data in a batch process. But how do you take that same model and deploy it (in data science terms, this is called "operationalization") to a web service for this purpose?

In this task, you will run the `Model Deployment` notebook to deploy the pre-trained model to a web service hosted by Azure Container Instances (ACI), using your Azure ML workspace. While it is possible to deploy the model to a web service running in Azure Kubernetes Service (AKS), we are deploying to ACI instead since doing so saves 10-20 minutes. However, once deployed, the process used to call the web service is the same, as are most of the steps to do the deployment.

### Task 1: Run deployment notebook

To run this notebook, perform the following steps:

1. In Azure Databricks, select **Workspace**, select **Users**, then select your username.

2. Select the `01 IoT` folder, then select the **Model Deployment** notebook to open it.

   ![The Model Deployment notebook is highlighted.](media/databricks-model-deployment-notebook.png 'Workspace')

3. As with the Batch Scoring notebook, be sure to attach your lab cluster before executing cells.

4. **After you are finished running the notebook**, open the Azure Machine Learning service workspace in the portal, then select **Models** in the left-hand menu to view the pre-trained model.

   ![The models blade is displayed in the AML service workspace.](media/aml-models.png 'Models')

5. Select **Deployments** in the left-hand menu, then select the Azure Container Instances deployment that was created when you ran the notebook.

    ![The deployments blade is displayed in the AML service workspace.](media/aml-deployments.png "Deployments")

6. Copy the **Scoring URI** value. This will be used by the deployed web app to request predictions in real time.

    ![The deployment's scoring URI is highlighted.](media/aml-deployment-scoring-uri.png "Scoring URI")

### Task 2: Call the deployed scoring web service from the Web App

Now that the web service is deployed to ACI, we can call it to make predictions from the Fleet Management Web App. To enable this capability, we first need to update the Web App's application configuration settings with the scoring URI.

1. Make sure you have copied the Scoring URI of your deployed service, as instructed in the previous task.

2. Open the Web App (App Service) whose name begins with **IoTWebApp**.

3. Select **Configuration** in the left-hand menu.

4. Scroll to the **Application settings** section then select **+ New application setting**.

5. In the Add/Edit application setting form, enter `ScoringUrl` for the **Name**, and paste the web service URI you copied and paste it in the **Value** field. Select **OK** to add the setting.

    ![The form is filled in with the previously described values.](media/app-setting-scoringurl.png "Add/Edit application setting")

6. Select **Save** to save your new application setting.

7. Go back to the **Overview** blade for the Web App, then select **Restart**.

8. Navigate to the deployed Fleet Management web app and open a random Vehicle record. Select **Predict battery failure**, which calls your deployed scoring web service and makes a prediction for the vehicle.

    ![The prediction results show that the battery is not predicted to fail in the next 30 days.](media/web-prediction-no.png "Vehicle details with prediction")

    This vehicle has a low number of **Lifetime cycles used**, compared to the battery's rated 200 cycle lifespan. The model predicted that the battery will not fail within the next 30 days.

9. Look through the list of vehicles to find one whose **Lifetime cycles used** value is closer to 200, then make the prediction for the vehicle.

    ![The prediction results show that the battery is is predicted to fail in the next 30 days.](media/web-prediction-yes.png "Vehicle details with prediction")

    This vehicle has a high number of **Lifetime cycles used**, which is closer to the battery's rated 200 cycle lifespan. The model predicted that the battery will fail within the next 30 days.

### About Azure Machine Learning workspace and model deployments

The top-level component of the Azure Machine Learning (AML) is the [workspace](https://docs.microsoft.com/azure/machine-learning/service/concept-workspace). Your first step to using AML is to create a workspace within an Azure region and resource group (a logical grouping of Azure services). When you do this, the script creates all services alongside your workspace. When you deployed the environment for this solution accelerator at the beginning of the Quickstart guide, the AML workspace was created.

Beyond the workspace, there are a few related Azure resources that are used to manage, monitor, and secure the workspace components. These are created for you automatically when you create a new workspace. However, you can choose to use existing Azure services in place of creating new versions.

- [Azure Container Registry](https://azure.microsoft.com/services/container-registry/): Registers docker containers that you use during training and when you deploy a model. To minimize costs, ACR is lazy-loaded until deployment images are created. This means that the ACR service is provisioned when you first register a model in your workspace.
- [Azure Storage account](https://azure.microsoft.com/services/storage/): Is used as the default data store for the workspace. Jupyter notebooks that are used with your notebook VMs are stored here as well.
- [Azure Application Insights](https://azure.microsoft.com/services/application-insights/): Allows you to monitor your models and view metrics on their usage.
- [Azure Key Vault](https://azure.microsoft.com/services/key-vault/): Securely stores secrets and other sensitive information used by your workspace and any compute targets.

#### High-level model workflow

![The stages shown are Train, Package, Validate, Deploy, and Monitor. An arrow labeled Retrain goes back to Train from Monitor.](media/aml-model-workflow.png 'Azure Machine Learning model workflow')

##### 1 - Train

At the core of the modern data science process is training, evaluating, and selecting machine learning models. Leading up to this point, you have collected and prepared the data for training. The next step is to select an algorithm for your model then train it with data that has been evaluated and prepared with the transformations and features required for training. At a very high level, training a model with Azure Machine Learning service involves the following steps:

- Using your favorite Python environment, create a machine learning training script along with any associated files. Specify the directory that contains these files, as well as an experiment name. Alternately, use visual interface for a code-free experience.
- Create and configure a compute target for executing the training. During training, the complete directory copies to the compute target before the training script executes.
- Submit the training scripts to the configured compute target. Afterward, the script starts running within the environment and has access to read from and write to datastores. Each execution saves a record of the run within the workspace, grouped under experiments.

Use the automated machine learning feature to select the best model during training automatically. This feature automates experimenting with multiple combinations of parameter values, also referred to as hyperparameter tuning, to accelerate the model training process and keeps a record of the outcomes to help identify potential areas of improvement more quickly.

##### 2 - Package

After you have trained your model and have identified the best version, you package it along with all the components you need to use the model, into an image. The image can be either a Docker image or an FPGA image used to deploy your model to a field-programmable gate array. The image saves to the image registry in your workspace. The registry provides a centralized place to store your models so they can be easily copied to new deployment targets, as well as versioned.

##### 3 - Validate

Model validation is used to calculate the accuracy of a model. Validation happens during the training process to make sure your chosen algorithm is performing as expected. It is also conducted periodically to ensure your model is still performing well over time with new data. Azure Machine Learning service allows you to query your experiments for logged metrics from current and past runs. Use the metrics to determine whether the run had the desired outcome. If not, begin the retraining process by starting over at step one.

##### 4 - Deploy

When you want your model to be available for on-demand access over the web or on an IoT device, you use the Azure Machine Learning SDK to deploy it as a web service in Azure, an FPGA, or to an IoT Edge device. The image that you created when you packaged the model is used to copy instances of the model, scoring script, and any dependencies to your deployment target. Your options for deploying the model as a web service are Azure Container Instance (ACI) and Azure Kubernetes Service (AKS).

##### 5 - Monitor

Monitor for changes in the distribution of data between the training dataset and inference data of your deployed model. These changes are sometimes called [data drift](https://docs.microsoft.com/azure/machine-learning/service/concept-data-drift) and indicate degraded prediction performance over time due to how the input data changes during this period. When you detect degraded model performance, the next step is to retrain your model with new data, thus creating a new version of the model. If your model is deployed to a web service or IoT devices, then you would use the new version of the model to redeploy it to those endpoints. The Azure Machine Learning SDK provides tools you can use to redeploy with minimal interruption of these services and endpoints.

## Section 12: Refresh the Power BI report and view maintenance data

> **Please note**: This is an optional component. If you do not need advanced analytics and machine learning in your solution, you may skip this section.

### Task 1: Open and refresh the report in Power BI Desktop

1. Open **Power BI Desktop**, then re-open the report.

2. Select the tab at the bottom of the report to view the Maintenance page. This page shows results from the batch scoring notebook you executed in Databricks. If you do not see records here, then you need to run the entire batch scoring notebook after some trips have completed.

    ![The maintenance page is displayed.](media/pbi-maintenance-tab.png "Maintenance")

3. Update the report with new data by clicking the **Refresh** button. This will show the results of the batch scoring notebook if you had one or more completed trips prior to running the notebook.

    ![The refresh button is highlighted.](media/pbi-refresh.png "Refresh")

## Environment clean-up

In this section, you will delete any Azure resources that were created in support of the Quickstart. You should follow all steps provided after you finish evaluating the sample scenario to ensure your account does not continue to be charged for unused resources.

### Task 1: Delete the resource group

1. Using the [Azure portal](https://portal.azure.com), navigate to the Resource group you used throughout this Quickstart guide by selecting Resource groups in the left menu.

2. Search for the name of your resource group, and select it from the list.

3. Select Delete in the command bar, and confirm the deletion by re-typing the Resource group name, and selecting Delete.

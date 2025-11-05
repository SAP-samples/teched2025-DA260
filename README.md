# DA260 - Connect third-party systems in SAP Business Data Cloud and SAP Datasphere

## Description

The SAP Business Data Cloud (BDC) solution enables smooth integration of SAP and third-party data. In this hands-on session, you will explore different connectivity features in SAP Business Data Cloud (incl. SAP Datasphere & SAP Analytics Cloud), including setup, data acquisition, integration, and transformation—ideal for data engineers and architects.

This hands-on workshop will give you the opportunity to try out the different integration technologies that are part of the SAP Business Data Cloud offering. 

SAP Businees Data Cloud includes SAP Datasphere, a comprehensive data service acting as a business data fabric that enables every data professional to deliver seamless, and scalable access to mission-critical business data. SAP Datasphere enables access to authoritative data by accelerating time-to-value by automatically reusing the semantical definitions and associations from SAP applications. SAP Datasphere enriches all data projects by harmonizing heterogeneous data into a business semantic model of your diverse data landscape. On top, it helps to simplify the data landscape and accesses all your data across hybrid and cloud environments no matter where it resides.

Additionally, SAP Businees Data Cloud includes SAP Analytics Cloud (= SAC), which enables users to visualize data, create interactive dashboards, and perform real-time reporting while supporting collaborative planning and forecasting. Furthermore, it includes different capabilities to perform data integration & acquistion with a focus on self-service for business users to easily acquire data from various different sources including SAP as well as 3rd party data sources.

**Important Note:**
SAP Business Data Cloud also offers a zero-copy based sharing of data products with partners (e.g. Databricks) using the BDC Connect functionality. This is one of the fundamental & strategic way for SAP to be able to allow a seemles bi-directional access to data products, but this is out of scope for this hands-on exercise. You can find more information in the following session from [TechEd 2025](https://www.sap.com/events/teched/virtual/flow/sap/tev25/catalog-virtual/page/catalog/session/1751961499331001rRV1) as well as in the [BDC documentation](https://help.sap.com/docs/business-data-cloud/administering-sap-business-data-cloud/provision-sap-business-data-cloud-connector-for-supported-external-systems?locale=en-US).
You will also find more information for the different announcements being done during TechEd for extending the usage of zero-copy based sharing of data products for addtional partners that will be onboarded to BDC Connect.

## Overview

* Learning Goal: Learn how to use various integration capabilities in SAP Business Data Cloud for integrating data from 3rd party data sources leveraging SAP Datasphere and SAP Analytics Cloud.



* Estimated Time: 2-4 h

  **Important Note:**
  Performing all exercises will require more time than the actual workshop onsite. Therefore, please feel free to pick the exercises that sound most interesting for you! 

  For example exercise 1 offers some great content for SAP Analytics Cloud with a detailed step by step guide and is one of the larger exercises in this hands-on session.

## Disclaimer

* Your screenshots may look different than those in the exercises, as new releases might include additional features or enhancements.  
* Some user interface elements might differ from the screenshots used in the exercises. 


## Requirements

* Google Chrome
* [Access to GitHub Repository](https://github.com/SAP-samples/teched2025-DA260)

  **Important Note**: The landscape being used during SAP TechEd will be available until **November 19th**. Until November 19th, you can re-use your existing content in your user space and finalize the exercises in case you did not have sufficient time during the hands-on workshop. 
  
* [Access to SAP Datasphere tenant](https://trial-bdc-datasphere-3.eu10.hcs.cloud.sap/)
* [Access to SAP Analytics Cloud tenant](https://trial-bdc-sac-3.eu10.sapanalytics.cloud/)
  * User-Id: AC239489UXX + last 2 digits with XX are the number being handed over to you by the trainers onsite at TechEd.
  * Tenant access password: xxx

* Basic know-how about the usage and integration of data in SAP Business Data Cloud leveraging SAP Datasphere & SAP Analytics Cloud (SAC)
* General understanding of Enterprise Data Management and ETL (Extraction, Transformation, Load).

## Exercises

**Important Note:** Please feel free to choose the exercises that are most interesting for you! You will likely not be able to cover all exercises in the time during the workshop. The arrows in the illustration below describe dependencies between the exercises, e.g. you need to complete exercise 5, before performing exercises 6 and 7.

![Overview_Exercises](images/Overview_Exercises.jpg)

A more detailed overview including the links to different exercises is provided below:

### Inbound integration

Please find below an overview of the different exercises.

| Product             | Replication | Federation | Push |
|---------------------|-------------|------------|------------ |
| SAP Analytics Cloud | [Exercise 1](exercises/ex1/), [Exercise 8](exercises/ex8/) | [Exercise 2](exercises/ex2/) | |  |
| SAP Datasphere      | [Exercise 3](exercises/ex3/) | [Exercise 4](exercises/ex4/) | [Exercise 5](exercises/ex5/) | |


- [Exercise 1 - Replicate data into SAC ](exercises/ex1/)
- [Exercise 2 - Live connection in SAC](exercises/ex2/)
- [Exercise 3 - Replicate data into SAP Datasphere with Replication Flows](exercises/ex3/)
- [Exercise 4 - Federation in Datasphere with Remote Tables](exercises/ex4/) 
- [Exercise 5 - Push data into Datasphere with OpenSQL](exercises/ex5/) 
- [Exercise 8 - Loading Data into an existing SAC model](exercises/ex8/) 

### Outbound integration

| Product             | Pull | Push |
|---------------------|-------------|------------|
| SAP Datasphere      | [Exercise 6](exercises/ex6/) | [Exercise 7](exercises/ex7/) |

- [Exercise 6 - Outbound pull of data in SAP Datasphere with JDBC or oData](exercises/ex6/) 
- [Exercise 7 - Outbound push in SAP Datasphere with Replication FLows](exercises/ex7/)

Have fun!

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support
Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.

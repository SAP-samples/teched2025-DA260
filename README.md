# DA260 - Connect third-party systems in SAP Business Data Cloud and SAP Datasphere

## Description

The SAP Business Data Cloud solution enables smooth integration of SAP and third-party data. In this hands-on session, you will explore different connectivity features in SAP Business Data Cloud (incl. SAP Datasphere & SAP Analytics Cloud), including setup, data acquisition, integration, and transformation—ideal for data engineers and architects.

This hands-on workshop will give you the opportunity to try out the different integration technologies that is part of the SAP Business Data Cloud offering. 

SAP Businees Data Cloud inlcudes SAP Datasphere, a comprehensive data service acting as a business data fabric that enables every data professional to deliver seamless and scalable access to mission-critical business data. SAP Datasphere enables access to authoritative data by accelerating time-to-value by automatically reusing the semantical definitions and associations from SAP applications. SAP Datasphere enriches all data projects by harmonizing heterogeneous data into a business semantic model of your diverse data landscape. On top it helps to simplify the data landscape and accesses all your data across hybrid and cloud environments no matter where it resides.

Additionally, SAP Businees Data Cloud includes SAP Analytics Cloud, which includes various options to perform data integration & acquistion with a focus on self-service for business users to easily acquire data from various different sources.


## Overview

MyCompany sales bikes to customers. In the source the list price is stored in the product master data. The sales order items only contain the net sales and quantity. The list price, that was valid at the time of sales, is not stored. The goal of the exercise is, to create a data model that stores the historic list price. For that a two stage data model is used. The data will come in by a Replication Flow and be staged by a Transformation Flow. 

Question to answer: Was there a rebate in the net sales compared to the list price of the product master data?

* Learning Goal: Learn how to load data in delta with a replication flow and stage them with transformation flow.* 
* Time: 2-4 h
* Finished Product: A view that shows the potential rebate per sales order line item. 

## ToDo:
- [ ] Write Start page 1 -> all
- [ ] Proof read Start page -> Leona
- [ ] Write Exercise 1 -> David
- [ ] Proof read Exercise 1 -> Leona
- [ ] Test Exercise 1 -> Leona
- [ ] Write Exercise 2 -> David
- [ ] Proof read Exercise 2 -> Leona
- [ ] Test Exercise 2 -> Leona
- [x] Write Exercise 3 -> Leona
- [ ] Proof read Exercise 3 -> Daniel
- [ ] Test Exercise 3 -> Daniel
- [x] Write Exercise 4 -> Hannes
- [x] Proof read Exercise 4 -> Leona 
- [x] Test Exercise 4 -> Leona
- [x] Write Exercise 5 -> Hannes
- [x] Proof read Exercise 5 -> Leona
- [x] Test Exercise 5 -> Leona
- [ ] Write Exercise 6 -> David
- [ ] Proof read Exercise 6 -> Leona
- [ ] Test Exercise 6 -> Leona
- [ ] Write Exercise 7 -> David
- [ ] Proof read Exercise 7 -> Leona
- [ ] Test Exercise 7 -> Leona
- [x] Write Exercise 8 -> Hannes
- [ ] Proof read Exercise 8 -> Leona
- [ ] Test Exercise 8 -> Leona
- [x] Write Exercise 9 -> Leona
- [ ] Proof read Exercise 9 -> Daniel
- [ ] Test Exercise 9 -> Daniel


## Requirements

* Google Chrome
* Access to this GitHub repository

  **Important Note**: The Datasphere landscape being used during SAP TechEd will be available until **November 19th**. Until November 19th you can re-use your existing content in your user space and finalize the exercises in case you did not have sufficient time during the hands-on workshop at SAP TechEd. 
  
* [Access to SAP Datasphere tenant](https://trial-bdc-datasphere-3.eu10.hcs.cloud.sap/)
  * User-Id: xxx + last 2 digits that have been provided to you onsite at TechEd
  * Tenant access password: xxx

* Basic knowhow about the usage and integration of data in SAP Business Data Cloud 
* General understanding of Enterprise Data Management and ETL (Extraction, Transformation, Load)

## Exercises

### Inbound integration

| Product             | Replication | Federation | Push |
|---------------------|-------------|------------|------------ |
| SAP Analytics Cloud | [Exercise 1](exercises/ex1/) ToDo: David| [Exercise 2](exercises/ex2/) ToDo: David| |  |
| SAP Datasphere      | [Exercise 3](exercises/ex3/) ToDo: Daniel | [Exercise 4](exercises/ex4/) To Validate: Leona | [Exercise 5](exercises/ex5/) | |


- [Exercise 1 - Replicate data into SAC ](exercises/ex1/)
- [Exercise 2 - Live connection in SAC Replicate data into SAP Datasphere with Replication Flows](exercises/ex2/)
- [Exercise 3 - Replicate data into SAP Datasphere with Replication Flows](exercises/ex3/)
- [Exercise 4 - Federation in Datasphere with Remote Tables](exercises/ex4/) 
- [Exercise 5 - Push data into Datasphere with OpenSQL](exercises/ex5/) 

### Outbound integration

| Product             | Pull | Push |
|---------------------|-------------|------------|
| SAP Analytics Cloud | [Exercise 6](exercises/ex6/) ToDo: David| [Exercise 7](exercises/ex7/) ToDo: David|
| SAP Datasphere      | [Exercise 8](exercises/ex8/) To Validate: Leona| [Exercise 9](exercises/ex9/) ToDo: Daniel|

- [Exercise 6 - Outbound pull in SAC with oData](exercises/ex6/) 
- [Exercise 7 - Outbound push in SAC with oData](exercises/ex6/) 
- [Exercise 8 - Outbound pull of data in Datasphere with JDBC or oData](exercises/ex8/) 
- [Exercise 9 - Outbound push in Datasphere with Replication FLows](exercises/ex7/) 

**IMPORTANT**

Your repo must contain the .reuse and LICENSES folder and the License section below. DO NOT REMOVE the section or folders/files. Also, remove all unused template assets(images, folders, etc) from the exercises folder. 

## Contributing
Please read the [CONTRIBUTING.md](./CONTRIBUTING.md) to understand the contribution guidelines.

## Code of Conduct
Please read the [SAP Open Source Code of Conduct](https://github.com/SAP-samples/.github/blob/main/CODE_OF_CONDUCT.md).

## How to obtain support

Support for the content in this repository is available during the actual time of the online session for which this content has been designed. Otherwise, you may request support via the [Issues](../../issues) tab.

## License
Copyright (c) 2024 SAP SE or an SAP affiliate company. All rights reserved. This project is licensed under the Apache Software License, version 2.0 except as noted otherwise in the [LICENSE](LICENSES/Apache-2.0.txt) file.

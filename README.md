# DA260 - Connect third-party systems in SAP Business Data Cloud and SAP Datasphere

## Description

The SAP Business Data Cloud solution enables smooth integration of SAP and third-party data. In this hands-on session, explore connectivity features in the SAP Datasphere and SAP Business Data Cloud solutions, including setup, data acquisition, integration, and transformation—ideal for data engineers and architects.

This hands-on workshop will give you the opportunity to try out the different integration technologies that BDC has to offer. 

SAP Businees Data Cloud inlcuded SAP Datasphere, a comprehensive data service acting as a business data fabric that enables every data professional to deliver seamless and scalable access to mission-critical business data. SAP Datasphere enables access to authoritative data by accelerating time-to-value by automatically reusing the semantical definitions and associations from SAP applications. SAP Datasphere enriches all data projects by harmonizing heterogeneous data into a business semantic model of your diverse data landscape. On top it helps to simplify the data landscape and accesses all your data across hybrid and cloud environments no matter where it resides.

## Overview

MyCompany sales bikes to customers. In the source the list price is stored in the product master data. The sales order items only contain the net sales and quantity. The list price, that was valid at the time of sales, is not stored. The goal of the exercise is, to create a data model that stores the historic list price. For that a two stage data model is used. The data will come in by a Replication Flow and be staged by a Transformation Flow. 

Question to answer: Was there a rebate in the net sales compared to the list price of the product master data?

* Learning Goal: Learn how to load data in delta with a replication flow and stage them with transformation flow.* 
* Time: 2-4 h
* Finished Product: A view that shows the potential rebate per sales order line item. 

## Requirements

* Google Chrome
* Access to this GitHub repository

  **Important Note**: The Datasphere landscape being used during SAP TechEd will be available until **November 19th**. Until November 19th you can re-use your existing content in your user space and finalize the exercises in case you did not have sufficient time during the hands-on workshop at SAP TechEd. 
  
* [Session-1 on November 2nd] [Access to SAP Datasphere tenant](https://academy.eu10.hcs.cloud.sap/dwaas-ui/index.html#/home)
  * User-Id: xxx + last 2 digits that have been provided to you onsite at TechEd
  * Tenant access password: xxx

* [Session-2 on November 3rd] [Access to SAP Datasphere tenant](https://academy.eu10.hcs.cloud.sap/dwaas-ui/index.html#/home)
  * User-Id: xxx + last 2 digits that have been provided to you onsite at TechEd
  * Tenant access password: xxx

* Basic knowhow about the usage and integration of data from SAP S/4HANA
* General understanding of Enterprise Data Management and ETL (Extraction, Transformation, Load)

## Deep Dives

- [Deep Dive 0 - Introduction to the Enterprise Procurement Model (EPM) in SAP S/4HANA](exercises/dd0/)
- [Deep Dive 1 - ABAP CDS View based data extraction from SAP S/4HANA on-premise](exercises/dd1/)
- [Deep Dive 2 - Introduction to Replication Flows in SAP Datasphere](exercises/dd2/)

## Exercises

### Ingest

| Product             | Replication | Federation | Push |
|---------------------|-------------|------------|------------ |
| SAP Analytics Cloud | [Exercise 1](exercises/ex1/) | [Exercise 2](exercises/ex2/)| |  |
| SAP Datasphere      | [Exercise 3](exercises/ex3/)  | [Exercise 4](exercises/ex4/) | [Exercise 5](exercises/ex5/) | |


- [Exercise 1 - Replicate data into SAC ](exercises/ex1/)
- [Exercise 2 - Live connection in SAC Replicate data into SAP Datasphere with Replication Flows](exercises/ex2/)
- [Exercise 3 - Replicate data into SAP Datasphere with Replication Flows](exercises/ex3/)
- [Exercise 4 - Federation in Datasphere with Remote Tables](exercises/ex4/) 
- [Exercise 5 - Push data into Datasphere with OpenSQL](exercises/ex5/) 

### Egress

| Product             | Pull | Push |
|---------------------|-------------|------------|
| SAP Analytics Cloud | [Exercise 6](exercises/ex6/) | [Exercise 7](exercises/ex7/) |
| SAP Datasphere      | [Exercise 8](exercises/ex8/) | [Exercise 7](exercises/ex9/) |

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

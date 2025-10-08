# Deep Dive 1 - ABAP CDS View based data extraction from SAP S/4HANA on-premise

>**IMPORTANT NOTE**<br>
>The following ***Deep Dive 1 documentation*** is intended as a later guidance for you to reproduce the described steps in your own environments.
>Even though it contains step by step instructions, ***this part does not belong to the hands-on exercises!***
<br>
ABAP Development Tools (ADT), formerly known as "ABAP in Eclipse", is the integrated ABAP development environment built on top of the Eclipse platform. Its main objective is to support developers in today’s increasingly complex development environments by offering state-of the art ABAP development tools. You can find more information about ADT here: https://tools.hana.ondemand.com/#abap.<br>
<br>
CDS (Core Data Services) is an extension of the ABAP Dictionary that allows you to define semantically rich data models in the database and to use these data models in your ABAP programs. CDS is a central part of enabling code push-down in ABAP applications.<br>
You can find more information about CDS in the ABAP keyword documentation : https://help.sap.com/doc/abapdocu_751_index_htm/7.51/en-US/abencds.htm and the SAP Community: https://community.sap.com/topics/abap<br><br>
Starting with SAP S/4HANA Cloud 1905 and SAP S/4HANA 1909 FPS01 (on-premise), Change Data Capture (CDC) is supported for ABAP CDS Views. After an ABAP CDS View is enabled for this delta method, changes in tables belonging to this view are recorded by the CDC mechanism. From a technology perspective, this delta method makes use of real-time database triggers on table level based on SLT technology.<br> INSERT, UPDATE and DELETE operations can be recorded by the framework.<br>

Those who are interested in more information about Change Data Capture for ABAP CDS Views may like to read the following blog **[CDS based data extraction – Part II Delta Handling](https://blogs.sap.com/2019/12/16/cds-based-data-extraction-part-ii-delta-handling/)**.<br><br>

After having completed the steps in this Deep Dive section we will have created two new delta-enabled custom ABAP CDS Views on our SAP S/4HANA system. Our goal is to leverage these CDS Views later to access the Customer and Sales Order data of the Enterprise Procurement Model (our demo dataset) from Replication Flows in SAP Datasphere.<br><br>

## Deep Dive 1.1 - Create a simple ABAP CDS View in ADT

In this sub section you can track how to create a CDS (Core Data Services) View using ABAP Development Tools (ADT). In our specific case, it is demonstrated how to create a CDS View to access data of the EPM table SNWD_BPA, which contains the Business Partner record set.

1. Create a CDS View
In the context menu of your package choose ***New*** and then choose ***Other ABAP Repository Object***.<br><br>
![](/exercises/dd1/images/1-001a.jpeg)

2.	Select ***Data Definition***, then choose ***Next***.<br><br>
![](/exercises/dd1/images/1-002a.jpeg)

3. Enter the following values, then choose Next.
- Name, e.g. ```Z_CDS_EPM_BUPA```
- Description: **CDS View for EPM Business Partner Extraction**
- Referenced Object: **SNWD_BPA**<br><br>
![](/exercises/dd1/images/1-003a.JPG)

4.	Accept the default transport request (local) by simply choosing ***Next*** again.<br><br>
![](/exercises/dd1/images/1-004a.JPG)

5.	Select the entry ***Define View***, then choose ***Finish***.<br><br>
![](/exercises/dd1/images/1-005a.jpeg)

6.	The new view appears in an editor, with an error showing up because of the still missing SQL View name.<br>
In this editor, enter value for the SQL View name in the annotation **`@AbapCatalog.sqlViewName`**, e.g. **`Z_SQL_EPM_BUPA`**.<br>
The SQL view name is the internal/technical name of the view which will be created in the database.<br>
**`Z_CDS_EPM_BUPA`** is the name of the CDS view which provides enhanced view-building capabilities in ABAP. 
You should always use the CDS view name in your ABAP applications.<br><br>
The data source plus its fields have automatically been added to the view definition because of the reference to the data source object we gave in step 3.
If you haven't provided that value before, you can easily search for and add your data source using the keyboard shortcut ***CTRL+SPACE***.<br><br>
![](/exercises/dd1/images/1-006a.jpeg)

7.	Delete the not needed fields in the SELECT statement, add the annotation ```@ClientHandling.type: #CLIENT_DEPENDENT``` and beautify the view.<br><br>
   ![](/exercises/dd1/images/1-007a.jpeg)<br><br>
   The code may now look as follows:
     ```abap
     @AbapCatalog.sqlViewName: 'Z_SQL_EPM_BUPA'
     @AbapCatalog.compiler.compareFilter: true
     @AbapCatalog.preserveKey: true
     @ClientHandling.type: #CLIENT_DEPENDENT
     @AccessControl.authorizationCheck: #CHECK
     @EndUserText.label: 'CDS View for EPM Business Partner Extraction'
     
     define view Z_CDS_EPM_BUPA
         as select from SNWD_BPA
         
     {
         key node_key as NodeKey,
             bp_role as BpRole,
             email_address as EmailAddress,
             phone_number as PhoneNumber,
             fax_number as FaxNumber,
             web_address as WebAddress,
             address_guid as AddressGuid,
             bp_id as BpId,
             company_name as CompanyName,
             legal_form as LegalForm,
             created_at as CreatedAt,
             changed_at as ChangedAt,
             currency_code as CurrencyCode
     }
     ```

8.	***Save (CTRL+S or disk symbol in menu bar)*** and ***Activate (CTRL+F3 or magic wand symbol in menu bar)*** the CDS View.<br>
(first ![](/exercises/dd1/images/1-008a.jpeg) 
then ![](/exercises/dd1/images/1-008b.jpeg))<br><br>

9.	We are now able to verify the results in the ***Data Preview*** by choosing ***F8***. Our CDS View data preview should look like this:<br><br>
![](/exercises/dd1/images/1-009a.jpeg)<br><br>

We have now successfully created the first simple CDS View in SAP S/4HANA. In the next step we'll showing how we can enable it for delta processing based on CDC.


## Deep Dive 1.2 - Extraction and Delta enablement for simple ABAP CDS Views

The extraction and delta enablement for simple ABAP CDS Views is pretty easy! The only step to do is adding the `@Analytics` annotations to the view that sets the enabled flag and the change data capture approach.<br>

Let's continue with the simple ABAP CDS View that we have implemented in the previous section and introduce the CDC delta for **`Z_CDS_EPM_BUPA`**.<br><br>

1. In ADT's Project Explorer, we navigate to our package and then to ***Core Data Services --> Data Definitions*** and double-click on the ABAP CDS View `Z_CDS_EPM_BUPA`.<br><br>
![](/exercises/dd1/images/dd1-010a.JPG)<br><br>

2. Under the existing list of annotations, enter the following lines:
   ```abap
   @Analytics:{
       dataExtraction: {
           enabled: true,
           delta.changeDataCapture.automatic: true
       }
   }
   ```
   <br>![](/exercises/dd1/images/dd1-011a.jpeg)<br><br>

3. ***Save*** (CTRL+S or ![](/exercises/dd1/images/1-008a.JPG)) and ***Activate*** (CTRL+F3 or ![](/exercises/dd1/images/1-008b.JPG)) the CDS View.<br><br>

That's it! In this simple case, the framework can derive the relation between the fields of the ABAP CDS View and key fields of the underlying table itself. Whenever a record is inserted, updated or deleted in the underlying table, a record with the respective table key is stored in a generated logging table.<br><br>



## Deep Dive 1.3 - Create a more complex ABAP CDS View in ADT (joining multiple tables)

In this part of the Deep Dive you can learn how to create a more complex ABAP CDS View, again using the ABAP Development Tools (ADT). We will go through the implementation of an ABAP CDS View which will join the EPM tables `SNWD_SO`, `SNWD_SO_I`, `SNWD_PD`, and `SNWD_TEXTS` in order to fetch all Sales Order relevant data, including its positions, products, and product names.<br>

(As a reminder: The entity relationships of the tables can be found [here](../ex0#short-introduction-to-the-enterprise-procurement-model-epm-in-sap-s4hana).)<br><br>

In a later step, also this ABAP CDS View will be enabled for Change Data Capturing (CDC) for an tigger-based processing of Sales Order related deltas to the target storage in S3.<br><br>

1. Create a CDS View
In the context menu of your package choose ***New*** and then choose ***Other ABAP Repository Object***.<br><br>
![](/exercises/dd1/images/1-001a.jpeg)

2. Select ***Data Definition***, then choose ***Next***.<br><br>
![](/exercises/dd1/images/1-002a.jpeg)

3. Enter the following values, then choose Next.
- Name, e.g. ```Z_CDS_EPM_SO```
- Description: **CDS View for EPM Sales Order object extraction**
- Referenced Object: **SNWD_SO**<br><br>
![](/exercises/dd1/images/dd1-012a.JPG)

4. Accept the default transport request (local) by simply choosing ***Next*** again.<br><br>
![](/exercises/dd1/images/1-004a.JPG)

5. Select the entry ***Define View***, then choose ***Finish***.<br><br>
![](/exercises/dd1/images/1-005a.jpeg)

6. The new view appears in an editor, with an error showing up because of the still missing SQL View name.<br>
In this editor, enter value for the SQL View name in the annotation **`@AbapCatalog.sqlViewName`**, e.g. **`Z_SQL_EPM_SO`**.<br>
The SQL view name is the internal/technical name of the view which will be created in the database. 
**`Z_CDS_EPM_SO`** is the name of the CDS view which provides enhanced view-building capabilities in ABAP. 
You should always use the CDS view name in your ABAP applications.<br><br>
The pre-defined data source plus its fields have automatically been added to the view definition because of the reference to the data source object we gave in step 3.
If you haven't provided that value before, you can easily search for and add your data source using the keyboard shortcut ***CTRL+SPACE***.<br><br>
![](/exercises/dd1/images/dd1-013a.JPG)

7.	Delete the not needed fields in the SELECT statement, add the annotation ```@ClientHandling.type: #CLIENT_DEPENDENT``` and beautify the view a bit.<br><br>
![](/exercises/dd1/images/dd1-014a.JPG)<br><br>

8. For joining the EPM Sales Order Header table (`SNWD_SO`) with other related EPM tables (Sales Order Item: `SNWD_SO_I`, Product:`SNWD_PD`, Text (e.g. product names):`SNWD_TEXTS`), we can follow two different approaches.<br>
   - **JOINS**, according to classical SQL concepts and always fully executing this join condition whenever the CDS View is triggered.
     An example would be<br>```select from SNWD_SO as so left outer join SNWD_SO_I as item on so.node_key = item.parent_key```.
   - **ASSOCIATIONS**, which are a CDS View specific kind of joins. They can obtain data from the involved tables on Join conditions but the data is only fetched if required. For example, your CDS view has 4 Associations configured and user is fetching data for only 2 tables, the ASSOICATION on other 2 tables will not be triggered. This may save workload and may increase the query performance.<br> An example for a similar join condition with associations would be<br>```select from SNWD_SO as so association [0..1] to SNWD_SO_I as item	on so.node_key = item.parent_key```
   
   In our specific case, we always need to fetch data from all involved tables. Hence, we choose the classical JOIN for this example and include the following lines:<br>
   ...
   ```abap
   left outer join snwd_so_i as item on so.node_key = item.parent_key
   left outer join snwd_pd as prod on item.product_guid = prod.node_key
   left outer join snwd_texts as text on prod.name_guid = text.parent_key and text.language = 'E'
   ```
   ...<br><br>
   ![](/exercises/dd1/images/dd1-014b.jpeg)<br><br>

9.	Add the wanted fields from the other tables in the join condition (and don't forget to make all key fields of all involved tables elements of the ABAP CDS View).<br><br>
   ![](/exercises/dd1/images/dd1-015a.jpeg)<br><br>
   The ABAP CDS View may now look as follows:
     ```abap
     @AbapCatalog.sqlViewName: 'Z_SQL_EPM_SO'
     @AbapCatalog.compiler.compareFilter: true
     @AbapCatalog.preserveKey: true
     @ClientHandling.type: #CLIENT_DEPENDENT
     @AccessControl.authorizationCheck: #CHECK
     @EndUserText.label: 'CDS View for EPM Sales Order object extraction'
     
     define view Z_CDS_EPM_SO as select from snwd_so as so
         left outer join snwd_so_i as item on so.node_key = item.parent_key
         left outer join snwd_pd as prod on item.product_guid = prod.node_key
         left outer join snwd_texts as text on prod.name_guid = text.parent_key and text.language = 'E'
     {
         key item.node_key       as ItemGuid,
         so.node_key             as SalesOrderGuid,
         so.so_id                as SalesOrderId,
         so.created_at           as CreatedAt,
         so.changed_at           as ChangedAt,
         so.buyer_guid           as BuyerGuid,
         so.currency_code        as CurrencyCode,
         so.gross_amount         as GrossAmount,
         so.net_amount           as NetAmount,
         so.tax_amount           as TaxAmount,
         item.so_item_pos        as ItemPosition,
         prod.product_id         as ProductID,
         text.text               as ProductName,   
         prod.category           as ProductCategory,
         item.gross_amount       as ItemGrossAmount,
         item.net_amount         as ItemNetAmount,
         item.tax_amount         as ItemTaxAmount,
         prod.node_key           as ProductGuid,
         text.node_key           as TextGuid
     }
     ```

10. ***Save*** (CTRL+S or ![](/exercises/dd1/images/1-008a.jpeg)) and ***Activate*** (CTRL+F3 or ![](/exercises/dd1/images/1-008b.jpeg)) the CDS View.<br><br>

11. Verify the results in the ***Data Preview*** by pressing ***F8***. Our CDS View data preview should look like this:<br><br>
![](/exercises/dd1/images/dd1-016a.jpeg)<br><br>


## Deep Dive 1.4 - Delta-enablement for complex ABAP CDS Views (joining multiple tables)

The main task for exposing a CDS view with CDC delta method is to provide the mapping information between the fields of a CDS view and the key fields of the underlying tables. The mapping is necessary to enable a comprehensive logging for each of the underlying tables and subsequently a consistent selection/(re-)construction of records to be provided for extraction. This means the framework needs to know which tables to log, i.e. monitor for record changes.

Given one record changes in possibly only one of the underlying tables, the framework needs to determine which record/s are affected by this change in all other underlying tables and need to provide a consistent set of delta records to the Operational Data Queue (ODQ).

All key fields of the main table and all foreign key fields used by all on-conditions of the involved join(s) need to be exposed as elements in the CDS views.

The first step is to identify the tables participating in the join and its roles in the join. Currently only Left-outer-to-One joins are supported by the CDC framework. These are the common CDS views with one or more joins based on one main table. Columns from other (outer) tables are added as left outer to one join, e.g. join from an item to a header table.

Given there are no restrictions applied to the CDS view, the number of records of the CDS view constitute the number of records of the main table. All records from the main table are visible in the CDS view. Deletions of a record with regards to this CDS view only happen, if the record in the main table is deleted.

Secondly the developer needs to provide the mapping between the key fields of the underlying tables and their exposure as elements in the CDS view. Please check the following figure in which you see the representation of all underlying key fields surfacing in the CDS view.<br>

![](/exercises/dd1/images/dd1-017a.jpeg)<br><br>
***Source:*** [CDS based data extraction – Part II Delta Handling](https://blogs.sap.com/2019/12/16/cds-based-data-extraction-part-ii-delta-handling/) (an excellent blog by Simon Kranig).<br><br>

In case of our EPM tables, we only need to consider one key field per table, which is the field `node_key` in all cases.
For mapping the key fields of all underlying tables to the fields of the CDS view, we use the annotation `Analytics.dataExtraction.delta.changeDataCapture.mapping`. This implies the requirement to make the key fields of all tables in the join condition elements of the ABAP CDS View.<br><br>

1. Include the following code under the list of existing annotations:
   ```abap
   @Analytics:{
       dataCategory: #FACT,
       dataExtraction: {
           enabled: true,
           delta.changeDataCapture: {
               mapping:
               [{table: 'SNWD_SO',
                 role: #MAIN,
                 viewElement: ['SalesOrderGuid'],
                 tableElement: ['node_key']
                },
                {table: 'SNWD_SO_I',
                 role: #LEFT_OUTER_TO_ONE_JOIN,
                 viewElement: ['ItemGuid'],
                 tableElement: ['node_key']
                },
                {table: 'SNWD_PD',
                 role: #LEFT_OUTER_TO_ONE_JOIN,
                 viewElement: ['ProductGuid'],
                 tableElement: ['node_key']
                },
                {table: 'SNWD_TEXTS',
                 role: #LEFT_OUTER_TO_ONE_JOIN,
                 viewElement: ['TextGuid'],
                 tableElement: ['node_key']
                }
               ]
          }
       }
   }
   ```
   ![](/exercises/dd1/images/dd1-018a.jpeg)<br><br>

2. ***Save*** (CTRL+S or ![](/exercises/dd1/images/1-008a.jpeg)) and ***Activate*** (CTRL+F3 or ![](/exercises/dd1/images/1-008b.jpeg)) the CDS View.<br><br>

3. Verify the results in the ***Data Preview*** by pressing ***F8***. The ABAP CDS View should still provide the same data as before delta-enabling.<br><br>

We have now enabled our Sales Order object CDS View for Change Data Capture and are able to obtain any delta from one of the involved tables.<br>

In the next deep dive 2, we test the Initial Load and Delta Load capabilities with a Replication Flow in SAP Datasphere including an introduction to Replication Flows.<br>

Please click here to continue with [Deep Dive 2 - Introduction to Replication Flows in SAP Datasphere](../dd2/)

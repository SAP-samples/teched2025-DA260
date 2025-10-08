# Exercise 1 - Replicate CDS Views from SAP S/4HANA via Replication Flows to SAP Datasphere

This exercise involves creating a Replication Flow that reads data from a SAP S/4 HANA CDS Views and replicates this data into SAP Datasphere local tables with delta capture as target. This process involves modelling of a replication flow and configuring it to consume a pre-existing S4 HANA connection and pick the required source objects to copy them into new target tables in SAP Datasphere.

In this exercise we will make use of connections that are pre-delivered in your SAP Datasphere instance, e.g. the SAP S/4HANA on Premise source system. You can check the the S/4HANA connection in the “Connections” application inside your SAP Datasphere space.

The Task is to load the CDS Views for
- Business Partner -  Z_CDS_EPM_BUPA
- Product - Z_CDS_EPM_PD
- Sales Order - Z_CDS_EPM_SO
- Sales Order Items - Z_CDS_EPM_SO_I

in delta mode into Datasphere. The delta mode is required to setup the historic price derivation in the transformation flow later

Step by Step guide:
Refer to the provided solution below for a detailed, step-by-step guide to complete Exercise 1.

1.	Open your SAP Datasphere using the provided credentials. Your user is associated with a default space that has the same name as your user where you can work and create your various data artifacts like the replication flow.
   
    ![ex_01_01](images/ex_01_01.png)

2.	Click on the Data Builder to see the Data Builder homepage as shown below and scroll the horizontal scroll bar to the middle until you see *New Replication Flow* tile.
   
    ![ex_01_02](images/ex_01_02.png)

3.	Click on *New Replication Flow* tile to launch the creation of new a replication flow.
   
    ![ex_01_03](images/ex_01_03.png)

4.	Click on *Select Source Connection* button that launches a popup window to select the source connection.

    ![ex_01_04](images/ex_01_04.png)

5.	Select *S4_HANA* which is using connection type *ABAP* from the list of available connections. It will update the connection and *Select Source Container* button is auto selected for next step on the bottom of the screen highlighted in blue.

    ![ex_01_05](images/ex_01_05.png)

6.	Click on “Select Source Container” button and it launches the *Select Container* popup. Then click on the *CDS – CDS Views* Container.

    ![ex_01_06](images/ex_01_06.png)

7.	On selecting the *CDS – CDS Views*, you will see that the container is updated in Replication Flow upper left part of the Data Builder screen

    ![ex_01_07](images/ex_01_07.png)

8.	Now click on *Add Source Objects* button that launches *Select Source Objects* popup as shown below. Scroll down in the tree hierarchy on the left and select *TMP – Local Objects*. In a next step, please enter “Z_CDS” in search bar and click enter to filter for the CDS Views that are required for this exercise. Now, please select the following CDS Views as shown below:
   <br>
   - Z_CDS_EPM_BUPA <br>
   - Z_CDS_EPM_PD  <br>
   - Z_CDS_EPM_SO  <br>
   - Z_CDS_EPM_SO_I  <br>

   <br>

![ex_01_07](images/ex_01_08.png)
    
9.	Click on *Next* button to see the updated popup window

    ![ex_01_09](images/ex_01_09.png)

10.	Click on *Add Selection* that starts the fetching of source objects details from the source

    ![ex_01_10](images/ex_01_10.png)

11.	The four selected CDS Views are now added to the Replication Flow:

    ![ex_01_11](images/ex_01_11.png)

12.	You have the possibility to create projections for each CDS View (e.g. creating a filter), but in this exercise no projections are required and hence you can skip the creation of projections. 

      As a next step, click on the icon adjacent to *Select Target Connection*. 

    ![ex_01_11_2](images/ex_1_11_2.png)

      The following popup window will appear where you need to select the target connection. In this case, please select *SAP Datasphere* as target connection.

    ![ex_01_12](images/ex_01_12.png)

13.	The target connection details are now updated in your Replication Flows using *SAP Datasphere* as target and the target container is automatically updated with the space in which your user is logged in.
In the highlighted section it shows the new target local tables that will be created in SAP Datasphere, which will be used as data sink for the data replication. 


    ![ex_01_13](images/ex_01_13.png)

14.	Select each of the target objects and update the Load Type to *Initial and Delta*. Repeat the same for all the target objects.

    ![ex_01_14](images/ex_01_14.png)

    Note: As an alternative, you can click on the *Settings* tab in the middle of the screen to change the load type to *Initial and Delta*.

15.	For each target object, select the three dot menu icon and select *Rename Target Object*:

      ![Rename_Replication_Flow](images/Rename_Replication_Flow.jpg)     

      Please rename Z_CDS_EPM_PD to Products, Z_CDS_EPM_SO to SalesOrders, Z_CDS_EPM_SO_I to SalesOrderItems and Z_CDS_EPM_BUPA to BusinessPartners. In this scenario we will let the replication flow create the target local tables instead of using pre-created tables.
   	
    ![ex_01_15](images/ex_01_15.png)

      Note: The replication flows can also write into already existing target tables in SAP Datasphere that have been created before. For this you can click on the three buttons next to the target table name and select *Map to Existing Target Object*. You can identify such tables that do not yet exist in your target system by looking at the name of the target data set, which are displayed slightly transparent and written in italic like it is currently displayed in your replication flow. 

17.	Click on Deploy icon ![ex_01_16_1](images/ex_01_16_1.png) in the general tab on top that launches Save popup window.

   ![ex_01_16_0](images/ex_01_16_0.png)

   Change the default name being displayed by defining the business name as *Inbound RepFlow* which will automatically set technical name as *Inbound_RepFlow*. At the moment, replication flows will always have the same name for business as well as technical name, which cannot be changed.
    
   ![ex_01_16](images/ex_01_16.png)

17.	Click on the *Save* button, which will start the deploy process. Check for the status in Properties Panel. The status is shown as *Not Deployed* initially and will get updated to *Deployed* after few seconds.

    ![ex_01_17](images/ex_01_17.png)

    Note: A message popup on the bottom of the screen will appear once the deployment process is finished and you can also check it using the notifications icon in the upper-right corner of your browser.

    ![ex_01_17_1](images/ex_01_17_1.png)

19.	Once the status is Deployed, click on run icon ![ex_01_18_0](images/ex_01_18_0.png) in the General tab above. You will see the Run Status in property panel getting updated to “Running”.

    ![ex_01_18](images/ex_01_18.png)

20.	Click on Monitor icon ![ex_01_19_1](images/ex_01_19_1.png)  in Run Status tab in property panel, which will directly navigate you to the detailed monitoring screen of your replication flow:

      ![ex_01_19_0](images/ex_01_19_0.png)

      Here you can see different information such as the source and target connection, load statistics and the status of the data replication for all four CDS Views

   	![ex_01_19](images/ex_01_19.png)


21.	Wait until all the four replication objects are run successfully, which means the initial load is done and they are in the delta load stage to receive updates from the source SAP S/4HANA system.
Once the Initial is done the status of each replication object will switch to status *Retrying*, which means that it is in delta load stage and will check every 1h for any new change data to arrive coming from the four source CDS views. 

      Note: You can also check in the *Metrics* tab for additional statistics such as the initial load duration as well as the number of transferred records:

      ![ex_01_21](images/ex_01_21.png)
      
      In case of any error message, please check the *Message* tab to access details of the error message.


22.	Finally, you can check the replicated data from SAP S/4HANA CDS views in the Datasphere local tables. Therefore, go to the main page of the Data Builder and check for the tables you have defined in the Replication Flow before:
    
      ![ex_01_22_0](images/ex_01_22_0.png)

    Then select one of the local tables in SAP Datasphere, e.g. SalesOrder, by double clicking on the table.

    Click on the preview button as highlighted below:

    ![ex_01_22_1](images/ex_01_22_1.png)

    You can now see the data that was replicated from SAP S/4HANA CDS View containing Sales order information on the bottom of your screen.

    

**This concludes the Exercise 1 where the objective is to replicate data from SAP S/4HANA source into SAP Datasphere.**

Note: If Replication flow fails, Please follow these steps to create local tables with import csn or import csv which are placed in the ex1 folder.
1. Import csn to import the meta data of table.
2. upload the given csv to load the data in the table

Pleae click here to continue with [Exercise 2 - Transforming data using Transformation Flows in SAP Datasphere](../ex2/)


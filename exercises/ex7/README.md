# Exercise 7 - Replicate Local Tables from SAP Datasphere to Google BigQuery (GBQ) with Replication Flows

This exercise involves creating a Replication Flow that reads data from SAP Datasphere local tables and replicates this data into Google BigQuery (GBQ). This process includes modeling a replication flow, configuring it to use a pre-existing GBQ connection, and selecting the required source objects to replicate them into new target tables in Google BigQuery.

The task is to load the SAP Datasphere local table:
- BusinessPartnersOpenSQL

**Step-by-step guide:**

Refer to the provided solution below for a detailed, step-by-step guide to complete Exercise 7.

1. Open your SAP Datasphere using the provided credentials. Your user is associated with a default space that has the same name as your user, where you can work and create your various data artifacts such as the replication flow.

   ![ex_09_01](images/ex_09_01.png)

2. Click on the **Data Builder** to see the Data Builder homepage, where you will find the *New Replication Flow* tile.  

   Then click **New Replication Flow** to start creating a new replication flow.

   ![ex_09_02](images/ex_09_02.png)

3. Click **Select Source Connection**, which opens a popup window where you can select the source connection.

   ![ex_09_03](images/ex_09_03.png)

4. Select **SAP Datasphere** as the source connection (technically using connection type HANA).  

   The connection updates, and the **Add Source Objects** step is automatically selected at the bottom. 

   Click **Add Source Object**.

   ![ex_09_05](images/ex_09_05.png)

5. After clicking **Add Source Object**, a popup appears showing all available repository objects. 

   Select **BusinessPartnersOpenSQL** and click **OK**.

   ![ex_09_06](images/ex_09_06.png)

   **Note:**  
   You can add additional objects into the Replication Flow, but for this exercise you will only replicate one local table to illustrate the general approach.  

   Only *Initial Load* is supported when replicating from the OpenSQL schema. Delta capabilities require local tables with delta capture enabled. 
   
   Many other sources support native delta capabilities that can be used in a replication such as ABAP-based sources (SAP S74HANA, SPA BW, SAP ECC etc.), databases (e.g. Microsoft SQL, SAP HANA etc.) any additional data sources.

6. You may create projections for each listed object, but they are not required for this exercise.  

   Next, click the icon next to **Select Target Connection**.

   ![ex_09_07](images/ex_09_07.png)

   A popup appears where you should select **Google Big Query** as the target connection.

   ![ex_09_08](images/ex_09_08.png)

7. The target connection details are now updated.  
   Click **Select Container**, choose the container **DA260_TARGET**, and click **Select**.  

   Choose **BusinessPartnersOpenSQL** as the object to replicate.

   ![ex_09_09](images/ex_09_09.png)

   ![ex_09_10](images/ex_09_10.png)

   ![ex_09_11](images/ex_09_11.png)

8. Click the three-dot icon to rename the target object.  
   Rename it to **UserX_businessPartnersOpenSQL**, where **X** is your user ID.  
   Example: if your ID is `10`, name it `User10_businessPartnersOpenSQL`.

   ![ex_09_12](images/ex_09_12.png)

   ![ex_09_13](images/ex_09_13.png)

   Below you can see the renamed target object:

   ![ex_09_15](images/ex_09_15.png)

9. Click the **Deploy** icon in the upper toolbar to open the *Save* popup.

   ![ex_09_14](images/ex_09_14.png)

   Change the default name by entering **Outbound Replication Flow 1**, which sets the technical name to `Outbound_Replication_Flow1`.  

   Click **Save**.

   ![ex_09_16](images/ex_09_16.png)

   ![ex_09_17](images/ex_09_17.png)

10. Once the status shows *Deployed*, click the **Run** icon ![ex_09_18](images/ex_09_18.png).  

    The Run Status updates to *Running*.

    ![ex_09_19](images/ex_09_19.png)

11. Click the **Monitor** icon ![ex_09_20](images/ex_09_20.png) in the Run Status panel or in the right-side Replication Flow Properties panel. 
 
    This opens the detailed monitoring view.

    ![ex_09_21](images/ex_09_21.png)

    ![ex_07_23](images/ex_07_23.png)

    The monitoring window shows all relevant details:

    ![ex_09_22](images/ex_09_22.png)

    You can start, pause, resume, rename, or stop the run.  
    If the replication flow has not completed yet, click **Refresh** (arrow shown below):

    ![ex_07_24](images/ex_07_24.png)

    Here you can also see statistics and the status of the data replication.

**This concludes Exercise 7, where the objective is to replicate data from SAP Datasphere into Google BigQuery (GBQ).**
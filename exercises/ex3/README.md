# Exercise 3 - Replicate Files from Google Cloud Storage (GCS) via Replication Flows to SAP Datasphere

This exercise involves creating a Replication Flow that reads data from Google Cloud Storage (GCS) CSV files and replicates this data into SAP Datasphere local tables. This process involves modeling a replication flow and configuring it to consume a pre-existing GCS connection and pick the required source objects to copy them into new target tables in SAP Datasphere.

In this exercise we will make use of connections that are pre-delivered in your SAP Datasphere instance, e.g., the Google Cloud Storage (GCS) connection. You can check the GCS connection in the **Connections** application inside your SAP Datasphere space.

The task is to load the CSV views from Google Cloud Storage for:
- Products  
- Sales Orders  
- Business Partners  

into SAP Datasphere.

Refer to the provided solution below for a detailed, step-by-step guide to complete Exercise 3.

1. Open your SAP Datasphere using the provided credentials. Your user is associated with a default space that has the same name as your user, where you can work and create your various data artifacts like the replication flow.

   ![ex_03_01](images/ex_03_01.png)

2. Click on the **Data Builder** and select your space to see the Data Builder homepage as shown below, where you can see the **New Replication Flow** tile.

   ![ex_03_02](images/ex_03_02.png)

3. Click on the **New Replication Flow** tile to launch the creation of a new replication flow.

   ![ex_03_03](images/ex_03_03.png)

4. Click on the **Select Source Connection** button to launch a popup window where you can select the source connection.

   ![ex_03_04](images/ex_03_04a.png)

5. Select **GCS**, which is using the connection type GCS (Google Cloud Storage), from the list of available connections. The connection will update, and the **Select Source Container** button will be automatically selected for the next step.

   ![ex_03_05](images/ex_03_05.png)

6. Click on the **Select Source Container** button to launch the container selection popup. Then click on **DA260** and select **Select**.

   ![ex_03_06](images/ex_03_06.png)

7. After selecting **DA260**, you will see that the container is updated in the upper-left part of the Replication Flow screen.

   ![ex_03_07](images/ex_03_07.png)

8. Click on the **Add Source Objects** button to launch the Select Source Objects popup.

   This window lists all files inside the selected container. Select the following CSV files:
   - *Products*  
   - *SalesOrders*  
   - *BusinessPartners*

   Please remember that you must repeat this step for each CSV file you want to add.

   ![ex_03_08](images/ex_03_08.png)

9. After selecting **Products**, a new window will open. Select the file named `Products.csv` and click **Next**.

   ![ex_03_09](images/ex_03_09.png)

10. Click **Add Selection**...

   ![ex_03_10](images/ex_03_10.png)

   ...which starts the fetching of source object details.

   ![ex_03_11](images/ex_03_11.png)

   After adding the `Products.csv` file, click the **+** button to add the other two source objects (`BusinessPartners.csv` and `SalesOrders.csv`), as shown below:

   ![ex_03_30](images/ex_03_30.png)

   Repeat steps 9–10 for the remaining files.

11. The three selected CSV files are now added to the Replication Flow:

   ![ex_03_12](images/ex_03_12.png)

12. You will see red notifications next to each Source Object.

   Select each dataset to open the **Object Properties** window on the right. Scroll down and select **Configure Schema**.

   A new popup window opens, displaying various properties for the CSV file. For this exercise, do not change these properties; leave them as they are.

   Make sure **UTF-8** is selected for Encoding. Click **Apply Changes**, then select the checkbox for the **Primary Key** column (each file should have an `ID` column). Click **Save**.

   ![ex_03_13](images/ex_03_13.png)

   ![ex_03_14](images/ex_03_14.png)

   **Note:** Repeat these steps for the other two CSV files to remove all red notifications.

13. You have the option to create projections for each CSV file, but no projections are required in this exercise.  
   As the next step, click the icon next to **Select Target Connection**.

   ![ex_03_15](images/ex_03_15.png)

   In the popup window, select **SAP Datasphere** as the target connection.

   ![ex_03_16](images/ex_03_16.png)

14. The target connection details are now updated in your Replication Flow. The target container is automatically set to the space your user is logged into. The highlighted section shows the new target local tables that will be created in SAP Datasphere and used as the data sink for replication.

   ![ex_03_17](images/ex_03_17.png)

15. For each of the target objects, click the **...** menu and select **Rename Target Object**:

   ![ex_03_18](images/ex_03_18.png)

   Rename `Products` to `Products_LT`, `BusinessPartners` to `BusinessPartners_LT`, etc.  
   In this scenario, you allow the replication flow to create the target local tables instead of using existing ones.

   ![ex_03_19](images/ex_03_19.png)

   **Note:** Replication flows can also write into pre-existing target tables. You can map to existing tables using the three-dot menu. Tables that don't yet exist appear slightly transparent and italicized.

16. Click the **Deploy** icon ![ex_01_16_1](images/ex_01_16_1.png) in the top toolbar to launch the Save popup:

   ![ex_03_20](images/ex_03_20.png)

   Change the default name to **Inbound Replication Flow**, which automatically sets the technical name to `Inbound_Replication_Flow`.

17. After deployment, click the **Run** button ![ex_03_29](images/ex_03_29.png). Check the status in the Properties Panel. It will start as *Not Deployed* and change to *Deployed* after a few seconds.

   ![ex_03_21](images/ex_03_21.png)

   **Note:** A popup notification will appear once the deployment finishes, and you can also check notifications in the top-right corner.

   ![ex_03_22](images/ex_03_22.png)

18. Click the **Monitor** icon ![ex_03_24](images/ex_03_24.png) in the Run Status tab or in the Replication Flow Properties panel to navigate to the monitoring screen:

   ![ex_03_25](images/ex_03_25.png)  
   ![ex_03_31](images/ex_03_31.png)

   Here you can see information such as source and target connections, load statistics, and replication status.

   ![ex_03_26](images/ex_03_26.png)

   You can start/pause/resume/stop the run using the three-dot menu. If the replication flow has not yet completed, click **Refresh** as shown below:

   ![ex_03_32](images/ex_03_32.png)

19. Once completed, you can check the replicated data in the Datasphere local tables. Go to the main page of the **Data Builder** and locate the tables created by the Replication Flow:

   ![ex_03_27](images/ex_03_27.png)

   Then select one of the local tables, e.g., **`BusinessPartners_LT`**, by clicking it once.

   Click the **Preview** button:

   ![ex_03_28](images/ex_03_28.png)

   ![ex_03_33](images/ex_03_33.png)

   After a few seconds, you will see the replicated data from Google Cloud Storage containing Business Partner information.

**This concludes Exercise 3, where the objective is to replicate data from Google Cloud Storage into SAP Datasphere.**

Continue with [Exercise 4 - Federation in Datasphere with Remote Tables](../ex4/).
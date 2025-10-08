# Exercise 4 - Replicate data from SAP S/4HANA to SAP HANA Data Lake Files using Replication Flows.

**Important Note**: Before beginning with this exercise please follow the steps in the following link to create a HDFL connection in your SAP Datasphere user space described in this link: [Connection Creation for SAP HANA Cloud, Data Lake Files](../connections/HDLFS/)

Additionally, you need to stop the Replication Flow created in [exercise 1](../ex1/) in case it is still running! To stop the replication flow created in exercise 1, please open the Data Integration Monitor and click in the *Stop* button located in the upper left menu bar within the detailed monitoring screen of your replication flow:

![Stop_Replication_Flow](images/Stop_Replication_Flow.jpg)

**Please wait until your replication flow is stopped successfully, before you continue with the steps below!**


1. Go to data builder, Select *New Replication flow* tile:
   
   ![Ex04_01](images/Ex04_01.png)
   
2. Click on *Select source Connection*:
   
   ![Ex04_02](images/Ex04_02.png)
   
3. In the connection dropdown, please select the *S4HANA* connection.
   
   ![Ex04_03](images/Ex04_03.png)
   
4. After selecting the connection, click on *Select Source container*

   ![Ex04_04](images/Ex04_04.png)
   
5. Inside source container, Select *CDS - CDS View*:
   
   ![Ex04_05](images/Ex04_05.png)
   
6. After selecting the container, *Add source objects*:
   
   ![Ex04_06](images/Ex04_06.png)
   
7. Select objects from left side folder browser, in *TMP Local Objects* folder.
    
8. Search Objects inside *TMP Local Objects* folder, with "Z_CDS" prefix. And select "Z_CDS_EPM_SALESORDER" CDS View:

   ![Ex04_07](images/Ex04_07.png)
   
9. Click *Next* and then click *Add selection*. Wait until the CDS views are imported successfully.
    
   ![ex_04_08](images/ex_04_08.png)
   
10. After the import is successful, add a target connection:
    
   ![Ex04_09](images/Ex04_09.png)

11. Select the target connection *HDLFS*, which you have created previously:
    
   ![Ex04_10](images/Ex04_10.png)
   
12. After selecting the target connection, select the *target container*:
    
   **Important Note:** Please select the target container using the following instructions: 
   
   - In case your user starts with prefix **AC60851U**XX (where XX stands for an integer value that is part of your Datasphere login user), please select the target container (=folder) in HDLFS that is matching the pattern teched-**XX**, where XX are the last two digits (numbers) that are part of your SAP Datasphere user ID, e.g. for AC60851U**01**, please select the folder teched-**01** as target container. If you select another folder of another user, the replication will fail.
     
   - In case your user starts with prefix **AC61257U**XX (where XX stands for an integer value that is part of your Datasphere login user), please select the target container (=folder) in HDLFS that is matching the pattern teched-1**XX**, where XX are the last two digits that are part of your SAP Datasphere user ID, e.g. for AC61257U**01**, please select the folder teched-**101** as target container. If you select another folder of another user, the replication will fail.

   ![Ex04_11](images/Ex04_11.png)
    
13. All the target tables should be listed like this:
   
14. Select each target table and change *load type* to “Initial and Delta”:
    
   ![Ex04_13](images/Ex04_13.png) 
   
15. Deploy the replication flow.
    
16. After successful deployment, Run the replication flow to create these tables in HDLFS target connection.
    
17. Once Replication flow execution completes. Go to *New Data Flow* editor available in the *Data Builder* application:
    
   ![Ex04_14](images/Ex04_14.png)
   
18. In Data flow editor, go to source, open the connection tree and browse the HDLFS connection:
    
   ![Ex04_15](images/Ex04_15.png)
   
19. In HDLFS connection, search for the folder, which was set as target container in the replication flow including your user ID. And there we can see all the tables are successfully replicated in SAP HANA Cloud, Data Lake Files:
    
   ![ex_04_19_1](images/ex_04_19_1.png)


20. Once you have successfully loaded your CDS view data to HDLFS, please go to the Data Integration Monitor to *Stop* your replication flow similar like it was explained in the beginning of this exercise. To stop your replication flow, please open the detailed flow monitor of your running replication flow and click the *Stop* button in the top menu bar:

   ![Stop_Outbound_RepFlow](images/Stop_Outbound_RepFlow.jpg)
     

**Done!** You have now successfully completed the last exercise of this Hands-On session DA260. 






 










# Exercise 5 - Push data into Datasphere with OpenSQL

In this exercise we are going to open an SQL end point that can used by external tools to push data into SAP Datasphere.  
We will create credentials for the external tools to authenticate on SAP Datasphere. We will also learn how to add the pushed entities to the repository. 




### Step-by Step-guide:
Refer to the provided solution below for a detailed, step-by-step guide to complete Exercise 5.

1.	Open your SAP Datasphere using the provided credentials. Your user is associated with a default space that has the same name as your user where you can work and create your various data artifacts.
   
    ![ex_05_01](images/ex_05_01.png)

2.	Navigate in the main menu to **Space Management** and open your space. 
   
    ![ex_05_02](images/ex_05_02.png)

3.	The Database User list in the section Database Access is used to open the endpoint and create the credentials to access the JDBC endpoint. Click on **Create** to create a new set of credentials. Enter a Database user suffix and enable read and write access and click **"*Create**
   
    ![ex_05_03](images/ex_05_03.png)

4. Please click on **Deploy** in the upper right corner of the screen to deploy the changes and activate the user creation.
Please wait until the status of your is changed to **Active** before you proceed.

5.	The user is now created in the database, to get to the connection details and the credentials click on the information **symbol (i)** of the newly created user. 
   
    ![ex_05_04](images/ex_05_04.png)    

6.	The user is now created in the database, to get to the connection details and the credentials click on the information symbol (i) of the newly created user. Click in the pop-up window **Request New Password**. This will show you all the connection details required to establish a JDBC connection to SAP Datasphere. This is the only time the password that can be copied into the clipboard or be shown, after closing the pop-up you need to request a new password, as the old one can no longer be retrieved, make sure to copy it and close the pop-up. 
   
    ![ex_05_05](images/ex_05_05.png)    



7.  Please select the user you have just created by clicking the checkbox next to the user and then click on **Open Database Explorer** to use the JDBC connection. 
    ![ex_05_07](images/ex_05_07.png)    

<<<<<<< HEAD
8.  A new browser tab will now be opened and here please enter "academy-platform" into the next box and click on **Sign in with alternative identity provider**.
=======
8.  Use your SAP Account to login, if you don't have one go up the prerequisite of this exercise. Then the Database explorer is acting as the external tool. The DB Explorer is as SAP tool integrated into our landscape, so that the connection details get pre-populated for you, for other tools they need to manually transferred to create the connection. Enter the previously generated password, if you check the **Save Password** box the DB Explorer will store the password for future use. It can be helpful to change the display name to something more human readable, from the GUID that is hat by default. Click **OK** to create the connection. 
Please etner the text "academy-platform" and lick on **Sign in with alternative identitiy provider**
>>>>>>> 640df28a136cd77cb54d6a22003f8cbbc8d5cd1a

 ![ex_05_08a](images/ex_05_08a.png)

 In the following screen, please click on **Authorize** and then you will be re-directed to the Database Explorer application.

  ![ex_05_08b](images/ex_05_08b.png)

Note: The Database Explorer is an SAP tool integrated into our landscape, so that the connection details get pre-populated for you, for other tools they need to manually transferred to create the connection. 

Now enter the previously generated password. If you check the **Save Password** box, the Database Explorer will store the password for future use. It can be helpful to change the display name to something more human readable, from the GUID that is hat by default. Click **OK** to create the connection. 

    ![ex_05_08](images/ex_05_08.png)


9. By right clicking the database connection, you can open the SQL console and create a new table, with the statement
    ![ex_05_09](images/ex_05_09.png)

<<<<<<< HEAD
10. We are simulating an external tool with the Database explorer, that is creating a table and pushing data into it (like an ETL tool would). You can create a new table, with the statement below, replace the schema name with your database user name that you created earlier. The statement will also enter a row for later usage (make sure to replace both schema placeholder).  After pasting the statement click *"Run"*
=======
10. We are simulating an external tool with the Database explorer, that is creating a table and pushing data into it (like an ETL tool would). We can create a new table, with the statement below, replace the schema name with your database user name that you created earlier. The statement will also enter a row for later usage (make sure to replace both schema placeholder).  After pasting the statement click **Run**
>>>>>>> 640df28a136cd77cb54d6a22003f8cbbc8d5cd1a
    ```
    CREATE COLUMN TABLE "<schema>"."BusinessPartnersOpenSQL"(
        "PARTNERID" NVARCHAR(10) NOT NULL,
        "PARTNERROLE" NVARCHAR(3),
        "EMAILADDRESS" NVARCHAR(255),
        "PHONENUMBER" NVARCHAR(30),
        "FAXNUMBER" NVARCHAR(30),
        "WEBADDRESS" NVARCHAR(1024),
        "ADDRESSID" NVARCHAR(10),
        "COMPANYNAME" NVARCHAR(80),
        "LEGALFORM" NVARCHAR(10),
        "CREATEDBY" NVARCHAR(10),
        "CREATEDAT" DATE,
        "CHANGEDBY" NVARCHAR(10),
        "CHANGEDAT" DATE,
        "CURRENCY" NVARCHAR(5),
        "Change_Type" NVARCHAR(1) DEFAULT 'I' NOT NULL,
        "Change_Date" LONGDATE DEFAULT CURRENT_UTCTIMESTAMP NOT NULL,
    PRIMARY KEY(
	    "PARTNERID"
    )
    )   PAGE LOADABLE
    UNLOAD PRIORITY 5 AUTO MERGE;

    INSERT INTO "<schema>"."BusinessPartnersOpenSQL" VALUES(
        '100001'/*PARTNERID <NVARCHAR(10)>*/,
        '1'/*PARTNERROLE <NVARCHAR(3)>*/,
        'bdc@sap.com'/*EMAILADDRESS <NVARCHAR(255)>*/,
        '0800/5 34 34 24'/*PHONENUMBER <NVARCHAR(30)>*/,
        '0800/5 34 34 24'/*FAXNUMBER <NVARCHAR(30)>*/,
        'www.sap.com'/*WEBADDRESS <NVARCHAR(1024)>*/,
        '12398789'/*ADDRESSID <NVARCHAR(10)>*/,
        'SAP SE'/*COMPANYNAME <NVARCHAR(80)>*/,
        'SE'/*LEGALFORM <NVARCHAR(10)>*/,
        'SAP'/*CREATEDBY <NVARCHAR(10)>*/,
        '20251004'/*CREATEDAT <DATE>*/,
        'SAP'/*CHANGEDBY <NVARCHAR(10)>*/,
        '20251004'/*CHANGEDAT <DATE>*/,
        'EUR'/*CURRENCY <NVARCHAR(5)>*/,
        ''/*Change_Type <NVARCHAR(1)>*/,
        ''/*Change_Date <TIMESTAMP>*/
    )
    ```
    ![ex_05_10](images/ex_05_10.png)
    Upon successful execution you will see the success messages on the bottom. 

<<<<<<< HEAD
11. Navigating back to the Data Builder in SAP Datasphere, the just created table is not automatically visible, but can be used. Create a new graphical view. Switch the *"Repository Browser to Source"*, on the left side of the canvas. There you will see the OpenSQL schema, it carries the name of the User you created in step 3. When expanding the listed schema, the created table should be visible and can be dragged into the canvas. This will trigger the creation of the Repository Object for the OpenSQL table. 
=======
11. Navigating back to the Data Builder in SAP Datasphere, the just created table is not automatically visible, but can be used. Create a new graphical view. Switch the **Repository Browser to Source**, on the left side of the canvas. There you will see the OpenSQL schema, it carries the name of the User we created in step 3. Under stat schema the created table should be visible and can be dragged into the canvas. This will trigger the creation of the Repository Object for the OpenSQL table. 
>>>>>>> 640df28a136cd77cb54d6a22003f8cbbc8d5cd1a
    ![ex_05_11](images/ex_05_11.png)


12. Once the table is deployed you can start previewing and consuming the table. 

    ![ex_05_12](images/ex_05_12.png)


**You have created an endpoint, created a table and filled with a record, that table is available in SAP Datasphere. This simulates an external tool, that creates a table and writes data into Datasphere. This concludes the Exercise 5 where the objective is to create Remote Tables in in SAP Datasphere.**

### Additional Information

The database is protected by a firewall. Any external tool trying to access the database needs to come from a whitelisted IP. In our trial system the user do not have sufficient privileges to modify the IP Whitelist. To modify the IP Whitelist, you need to navigate to System -> Configuration -> IP Allowlist -> Trusted IP. This will show you the list of all trusted IP's.

**Important Note:** This is not required for this exercise, but a general hint that you need to consider in case you plan to sue this functionality in your own landscapes
   
![ex_05_06](images/ex_05_06.png)    

By clicking the **Add** button you can add entries to the whitelist. Here you can add single IP's or networks of IP's

![ex_05_06_2](images/ex_05_06_2.png)    

Please click here to continue with [Exercise 6](../ex6/)

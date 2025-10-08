# Exercise 4 - Fedeeration in Datasphere with Remote Tables

This exercise involves creating Remote Tables that that graete a federated connectiont to tables from Google Big Query. 

In this exercise we will make use of connections that are pre-delivered in your SAP Datasphere instance, e.g. the GQB cloud source system. You can check the the GBQ connection in the “Connections” application inside your SAP Datasphere space.

The Task is to create Remote Tables fo
- Business Partner -  businesspartner
- Product - products
- Sales Order - salesorder
- Sales Order Items - salesorderitem


Step by Step guide:
Refer to the provided solution below for a detailed, step-by-step guide to complete Exercise 1.

1.	Open your SAP Datasphere using the provided credentials. Your user is associated with a default space that has the same name as your user where you can work and create your various data artifacts.
   
    ![ex_04_01](images/ex_04_01.png)

2.	Click on the Data Builder to see the Data Builder homepage as shown below and find the import button, select Import Remote Table
   
    ![ex_04_02](images/ex_04_02.png)

3.	A step by step import wizard opens. Select the GBQ connection and click on "Next Step"
   
    ![ex_04_03](images/ex_04_03.png)

4.	In the next step of the wizard we are to select the source objects we want to create Remote Tables for. Open the tree on the left hand side and navigate to the folder DA260

    ![ex_04_04](images/ex_04_04.png)

5.	Select the four tables either by cliking them one by one or by slecting the check box in the header and click "Next Step"

    ![ex_04_05](images/ex_04_05.png)

6.	The wizard provides you with an review of what it is about to do. As the tables have not been imported before the "Import Status" is will be imported. Should an object already exist it will show here in the status. In additon you can rename the objects that will be created, note that the technical name can't be changed later. Adjust the names if desired and click "Import and Deploy"

    ![ex_04_6](images/ex_04_06.png)

7.	This will take a while, the system is now pulling the meta data from the source, creates the design time for the remote table and deployes them, to create the runtime objects. You will see toasts appearing with messages. Once done it will show a summary, click "Close"

    ![ex_04_7](images/ex_04_07.png)   
   
8.	After the import we have succesfully created the Remote Tables in SAP Datasphere. To check if they are functioning, click on one of the table to go into the Remote Table editor. 

    ![ex_04_8](images/ex_04_08.png)   

9.	In the Remote Table editor we can open the preview window to test the that data can be read. Click in the section view on the preview button. This will open a preview on the lower section of the screen. 

    ![ex_04_9](images/ex_04_09.png)   

    The Remote Table Editor allows to make changes properties that are not technically bound to the source objects, like the Business Names, the Remantic Usage, Filter (if supported), Associations or Business Purpose informaiton. Properties that are technically bound the source like technical names or data types of columns can't be chanded in SAP Datasphere, the must be changed in the source as the Remote Table is mirror image. You do have the ability to hide fields from the Remote Table in the column section, the fields will become and queryable but can be added again with the + symbol. 

10.	Navigate in the main menue to the "Data Integration Monitor" and select Remote Queries under Remote Queries. This will show you the statements we have send to the remote, in our case it contains the two statemenbts used for the data preview. One for the record count and one to pull the data for the preview. 

    ![ex_04_10](images/ex_04_10.png)   


**This concludes the Exercise 4 where the objective is to create Remote Tables in in SAP Datasphere.**


Pleae click here to continue with [Exercise 5](../ex5/)


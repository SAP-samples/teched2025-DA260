# Exercise 8 - Loading Data into an existing SAC model

In exercises 1 and 2, you created a model from data. In this exercise, you load new data into **Teched2025-DA260_Ex1_Games2022**, which you created in exercise 1. This is SAC's `Extract, Transform, Load (ETL)` workflow, where you connect, bring the data into SAC, and then transform it to fit the semantic model that it will be used with. You will spend more time in the modeling tools than in the previous exercises, because SAC's data connectivity and semantic modeling are closely intertwined.

**Step 0** to **Step 28** were carried out in Continue to – [Exercise 1 - Create an Analytics Cloud Model with Acquired Data](../ex1/README.md), and this exercise carries on from **Step 29** onwards.

## Step 29

Return to the modeling app and re-open **Teched2025-DA260_Ex1_Games2022**.

Note that the **score** column uses a dash between the home and away scores. You would like this to be a semicolon, so you will reload this data and fix this with a wrangling transform.

Click the eraser icon in the Data group to delete records from the fact table.

![Step 29](images/Teched2025-DA260_Ex1_31.png)

## Step 30

Next comes the fact filter dialog. Here, you can set the filter for fact deletion; all records where the specified dimension value(s) are checked. This gives you the option to delete specific records matching the specified filter pattern. By default, all dimension members of the first dimension in the list are checked, and this will delete all facts from the table.

Click **OK**.

![Step 30](images/Teched2025-DA260_Ex1_32.png)

## Step 31

Click **OK** to confirm that you want to clear the fact table.

![Step 31](images/Teched2025-DA260_Ex1_48.png)

## Step 32

You will now see an empty fact table in your model.

![Step 32](images/Teched2025-DA260_Ex1_49.png)

## Step 33

Navigate to the **Data Management** workspace.

![Step 33](images/Teched2025-DA260_Ex1_35.png)

## Step 34

Recall that when you originally connected to the data to start creating the model, you created an initial import job. When you create a model from data, you skip data wrangling and column mapping, which is why the import job "has not been set up." You will now set this import job up.

Click **Set Up Import**.

![Step 34](images/Teched2025-DA260_Ex1_34.png)

## Step 35

Here you see a significant difference in behavior compared to what you encounter with Datasphere Replication Flows in [Exercise 3](../ex3/README.md).  
- With Replication Flows, remote data is replicated into Datasphere tables, and you can then do what you want with those tables later.  
- SAC import jobs always exist in the context of a data model. The remote data is replicated into local tables, but this is regarded as draft data, yet to be prepared for the model. This draft data is used when preparing wrangling (data preparation) and mapping, but is not visible outside this context and is not retained for very long.

If you recently created your model, the draft data may still be present, and you will not see this popup. If you return a few days later, the draft data is cleaned up. If the draft data is still present, you will simply go to the next step. Otherwise, this popup prompts you to re-run the query before proceeding. You will almost always be prompted to rerun your query.

If you are prompted, click **Rerun Query**.

![Step 35](images/Teched2025-DA260_Ex1_37.png)

## Step 36

Take a moment to orient yourself in the **Data Wrangler**. Here is where you transform data.  
- It uses a spreadsheet visual paradigm, allowing you to work interactively on the data and see the effects of your transforms in real time.  
- Sometimes data needs to be transposed from columnar to row format. For example, a set of revenue figures might be split across columns for side-by-side comparison of year-on-year results, but you may want these figures in a single measure later. You can transpose data using **Unpivot**.  
- You have access to two separate "formula bars": the interactive **Create Transform** builder and a powerful **Custom Expression Editor**.  
- You can toggle the transform log to see what transforms you have done in the session, revert them, or edit them.  
- Lastly, note that the Wrangler detected that text cells containing numbers are actually numeric and assigned the data type appropriately.

![Step 36](images/Teched2025-DA260_Ex1_38.png)

## Step 37

Click the **Custom Expression Editor** icon to open the editor.

![Step 37](images/Teched2025-DA260_Ex1_50.png)

## Step 38

You will use the `replaceContect()` expression. You can use the **Custom Expression Editor**'s code completion assistant by beginning to type the command. Type:

`re`

Select **replaceContect** from the dropdown.

![Step 38](images/Teched2025-DA260_Ex1_51.png)

## Step 39

The custom expression formula initially looks like this:

`[column] = replaceContent(string1, substring1, string2)`

- **column** – the name of the new column that will be created  
- **string1** – the column where the change will occur  
- **substring1** – the pattern that will be replaced  
- **string2** – the pattern that will be inserted  

![Step 39](images/Teched2025-DA260_Ex1_52.png)

## Step 40

Create a new column called **score2**, which duplicates **score** and replaces "–" with ":".

`[score2] = replaceContent([score], "–", ":")`

**Note!** The **"–"** coming from the database is a long dash, not the ASCII **"-"**. It is best to copy and paste it from the table or from this document.

Click the checkmark to execute the formula.

![Step 40](images/Teched2025-DA260_Ex1_53.png)

## Step 41

You can now compare **score** and **score2** and see the difference in the text.

Click **Next** to proceed to mapping.

![Step 41](images/Teched2025-DA260_Ex1_54.png)

## Step 42

Now choose **Step 2: Map to Facts**.

In **Mapping**, look at the mapping section on the right side. See where the **score** column in the draft data is mapped to the **score** dimension.

Click the **X** next to the **score** column in the draft data to delete this mapping.

![Step 42](images/Teched2025-DA260_Ex1_55.png)

## Step 43

The **score** dimension now has no mapping.

Drag **score2** from **Source Columns** to the "Drag a column" box.

![Step 43](images/Teched2025-DA260_Ex1_56.png)

## Step 44

See where the **score2** column in the draft data is mapped to the **score** dimension.

Click **Next** to proceed to validation.

![Step 44](images/Teched2025-DA260_Ex1_57.png)

## Step 45

Click **Next**.

The draft data will now be validated against the model. Any problems are reported here, allowing you to fix them before committing them to the fact table.

![Step 45](images/Teched2025-DA260_Ex1_58.png)

## Step 46

No problems should be reported. A common issue would be unbooked dimension members, where a column mapped to a dimension does not have a value in the dimension table.

Since your model uses only "single column" dimensions, where no separate dimension table exists, there are no foreign key constraints. If your fact data does not align with master data, this is normally where you would discover it.

**Note!** This exercise deliberately uses only single column dimensions, as it is focused on data connectivity rather than modeling.

![Step 46](images/Teched2025-DA260_Ex1_41.png)

## Step 47

If no problems are reported, click **Run Import**.

![Step 47](images/Teched2025-DA260_Ex1_42.png)

## Step 48

Click **Finish** to start the data load.

![Step 48](images/Teched2025-DA260_Ex1_43.png)

## Step 49

While the data load is running, you will see a running animation under **Last Known Status**.

![Step 49](images/Teched2025-DA260_Ex1_44.png)

## Step 50

Once the data load is finished, you should see a chain of green checkmarks under **Last Known Status**. This indicates the status of the various steps of the process—connection, query, wrangling, validation. If there is a problem or an incomplete process (such as clicking **Save and Exit**), you will see it here.

You can set up automatic, scheduled data refreshes. To do so:

- Click the checkbox next to all load jobs of a model that you want to maintain a particular schedule for.  
- Then click the Calendar icon.

![Step 50](images/Teched2025-DA260_Ex1_60.png)

## Step 51

You can set up automatic, scheduled data refreshes. To do so:

- Click the checkbox next to all load jobs of a model that you want to maintain a particular schedule for.  
- Then click the Calendar icon.

![Step 51](images/Teched2025-DA260_Ex1_60.png)

## Step 52

Maintain your desired schedule settings—for example, once a week at 6 AM. You can schedule load jobs more frequently than once per hour.

![Step 52](images/Teched2025-DA260_Ex1_61.png)

## Step 53

Return to the **Model Structure** workspace.

![Step 53](images/Teched2025-DA260_Ex1_46.png)

## Step 54

Look in your data foundation. You will see that the members of the **score** dimension now display the transformed version.

![Step 54](images/Teched2025-DA260_Ex1_47.png)

## Summary

You have now created a new model in SAC by importing data.

Continue to – [Exercise 2 - Analytics Cloud Model with Live Data](../ex2/README.md)
# Manage Tables

## Introduction

In this lab, you will use Database Actions to view table definitions and table data in Oracle Database. You will also learn to create a new table and load data into the new table.

Estimated time: 20 minutes

### Objective

Perform these tasks in your Oracle Database from Oracle Database Actions:

-   View an existing table
-   Create a new table
-   Load data into the table

### Prerequisites

This lab assumes you have-

-   An Oracle Cloud account
-   Completed all previous labs successfully
-   ORDS installed and configured
-   *HR* schema enabled to access Database Actions
-   Logged in to Oracle Database Actions in a web browser as *HR*

## Task 1: View existing table in your schema

In this task, you will view the existing tables in the HR schema in your Autonomous Database using Oracle Database Actions.

1.  Log in to Database Actions as *HR* if you are not logged in.

2.  Click the **SQL** card under Development. This opens the SQL page in Database Action.
    ![SQL Card](../manage-tables/images/sql-card.png)
    
    Alternatively, click the **Selector Icon** ![Selector Icon](../manage-tables/images/selector-icon.png) and under Development section click **SQL**. The SQL page appears. ![SQL Page](../manage-tables/images/sql-page.png)
    
    > **Note:** If this is your first time accessing the SQL Worksheet, click the binocular icon at the top-right to access hopscotch tour. Click the "**X**" in the tour popup window to quit the tour.

3.  In the Navigator tab, verify schema selected is *HR* from the first drop-down list and *Tables* from the second drop-down list.
    ![Table List](../manage-tables/images/table-list.png)
    The navigator pane displays the list of tables of the selected schema HR.

4.  Right-click one of the tables, for this task, *COUNTRIES* and select **OPEN**.
    ![Tables](../manage-tables/images/open-table.png)
    
    This option opens a window that displays the properties of the selected table. The properties window displays information for the following properties of the table:

    -   Columns
    -   Data
    -   Constraints
    -   Grants
    -   Statistics
    -   Triggers
    -   Dependencies
    -   Details
    -   Partitions
    -   Indexes

5.  Look at the Columns tab from the properties window to view the column names and their definitions.
    ![Columns Tab](../manage-tables/images/columns-tab.png)
    The values may differ depending on the system you are using.

6. Select the **Data** tab from the properties window to view the data stored in COUNTRIES.
  ![Data Tab](../23c-manage-tables/images/data-tab.png)
  The values may differ depending on the system you are using.

Click **Close** at the bottom-right to close the properties dialog box.

## Task 2: Create a new table

You can create a new table and insert data in your Oracle Database using the SQL card in the Database Actions. The code editor in the SQL page enables you to run SQL statements, PL/SQL scripts, and JavaScript code. You can enter SQL and PL/SQL statements to create a table and insert data into the table.

1.  Click the **Clear** icon in the SQL Toolbar to remove the statements from the editor if they exist.
    ![Clear Icon](../manage-tables/images/clear-icon.png)

2.  Copy and paste the following SQL statements in the editor.

    ```
    <copy>
    CREATE TABLE account (
    id NUMBER NOT NULL
    , account_no VARCHAR2(20)
    , customer_id NUMBER
    , open_date VARCHAR2(20)
    , balance NUMBER
    , CONSTRAINT account_pk PRIMARY KEY (id)
    );
    INSERT INTO account VALUES (201,&#39;xxx-yyy-201&#39;,101,&#39;2015-10-04&#39;,1500);
    INSERT INTO account VALUES (202,&#39;xxx-yyy-202&#39;,102,&#39;2012-09-13&#39;,200);
    INSERT INTO account VALUES (203,&#39;xxx-yyy-203&#39;,103,&#39;2016-02-04&#39;,2100);
    INSERT INTO account VALUES (204,&#39;xxx-yyy-204&#39;,104,&#39;2018-01-05&#39;,100);
    INSERT INTO account VALUES (211,&#39;xxx-zzz-211&#39;,NULL,NULL,NULL);
    INSERT INTO account VALUES (212,&#39;xxx-zzz-212&#39;,NULL,NULL,NULL);
    COMMIT;
    </copy>
    ```

3.  Select the **Run Script** icon to run the script.
    ![Run Script](../manage-tables/images/run-script.png)

    The SQL statements above creates a new table named ACCOUNT and adds values into it.

4. Verify the following values in the Navigator tab to view the table list.
    - **Schema**: *HR*
    - **Object Type**: *Tables*

    You can view the newly added ACCOUNT table in the tables list.
    ![New Table](../manage-tables/images/new-table.png)

## Task 3: Load data from a file to an existing table

You can load data from a file to an existing table named *ACCOUNT*.

1.  In the Navigator tab, right-click the ACCOUNT table.

2.  Click **Data Loading** and select **Upload Data**.
    ![Upload Data](../manage-tables/images/upload-data.png)
    An Upload Data into HR.ACCOUNT dialog box appears.

3.  Drag and drop the file that contains data, which you want to load into the table. You can also click **Add File** to browse for the file in your system and upload it. 
    ![Add Files](../manage-tables/images/add-files.png)
    
    > **Note:** The file formats that you can load are CSV, XLS, XLSX, TSV, TXT, XML, JSON, and AVRO. 

4.  Verify the file name after adding the file in the Upload Data Into HR.ACCOUNT dialog box.
    ![Data Loaidng](../manage-tables/images/data-loading.png)

    > **Note**: This lab provides a CSV file with dummy data to upload into your database for learning purpose.

5.  Click the file name to open the Details page.
    -   **Column names:** Select **Get from file** to display column headers in the first row.
    -   **Encoding:** You can view the *UTF-8* value from the drop-down. This is the default value. 
    -   **Text enclosure** and **Field delimiter**: Enter " (single quote) in the Text enclosure field and ","(comma) in the Field delimiter field. These options are visible only when the selected file is in plain text format (CSV, TSV, or TXT).
    -   **Rows to skip:** Select the number of rows to skip. For example, *0*.
    -   **Preview size:** Select the number of rows to preview. For example, *100*.
    -   **Limit rows to upload:** This check box is to specify the number of rows to load. For this task, do not select this check box.
        ![Details of the file](../manage-tables/images/details.png)

6.  Click **Next** to progress to the Target tab of the dialog box. For each Source column, select the value from the drop-down in the Target column.
    For this task, select the following values from Target column.
    -   COL1: Select *ID*
    -   COL2: Select *ACCOUNT_NO*
    -   COL3: Select *CUSTOMER_ID*
    -   COL4: Select *OPEN_DATE*
    -   COL5: Select *BALANCE*
    ![Target Tab](../manage-tables/images/target-tab.png)
    The values differ depending on the file you have uploaded.

7.  Click **Upload File** to load the selected data. It will direct you back to the Upload Data Into HR.ACCOUNT dialog box.
    ![Upload File](../manage-tables/images/upload-file.png)

8.  Once the status changes from PENDING to UPLOADED the data file has been uploaded successfully.
    ![File Uploaded](../manage-tables/images/uploaded.png)
    After the data upload process is complete, an entry is added to the log with the status.

9.  To view the log status, click the **Open History** button present in the bottom-left corner of the dialog box.
    ![Open History](../manage-tables/images/open-history.png)
    The below table is displayed.
    ![Data History](../manage-tables/images/data-history.png)
    The values may differ depending on the system you are using.

You can also view the summary of the data uploaded from the SQL main window. Right-click the ACCOUNT table in the Navigator tab, click **Data Loading** and select **History** to view the summary of the data upload. You can view the total number of rows that fail if the data file fails to upload.

You may now **proceed to the next lab**.

## Acknowledgments

- **Author** - Aayushi Arora, Database User Assistance Development Team
- **Contributors** - Manish Garodia
- **Last Updated By/Date** - Aayushi Arora, September 2023



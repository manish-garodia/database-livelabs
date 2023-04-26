# View container details from SQL command line

## Introduction

This lab walks you through the steps to log in to SQL prompt and explore Container Database (CDB) and Pluggable Database (PDB) with basic SQL commands.

Estimated time: 10 minutes

### Objectives

 - Set environment variables
 - Log in to CDB (root container) with *SYSDBA* privileges
 - Run SQL commands to view details of CDB and PDB

### Prerequisites

This lab assumes you have -

 -   An Oracle Cloud account
 -   Completed all previous labs successfully
 -   Logged in to your host as the *oracle* user

## Task 1: Set environment variables

[](include:set-env-var)

> **Tip:** If you have reserved a Livelabs sandbox environment, then you can run the script `.set-env-db.sh` from the home location and enter the corresponding number for the `ORACLE_SID`. It sets the environment variables automatically.

## Task 2: Connect to SQL prompt and explore the container

In this task, you will view some basic details of the container, such as current user, container name, container ID, PDBs, database version, instance name, and its current status.

1.  From `$ORACLE_HOME/bin`, log in to the SQL command line as *SYSDBA*. 

    ```
    $ <copy>./sqlplus / as sysdba</copy>
    ```

	```
	SQL*Plus: Release 23.0.0.0.0 - Beta on Fri Feb 24 15:30:47 2023
	Version 23.1.0.0.0

	Copyright (c) 1982, 2022, Oracle.  All rights reserved.


	Connected to:
	Oracle Database 23c Enterprise Edition Release 23.0.0.0.0 - Beta
	Version 23.1.0.0.0

	SQL>
	```

1.  Check the current user connected to the database.  

    ```
    SQL> <copy>show user</copy>

    USER is "SYS"
    ```

1.  View the container name and the container id.

    ```
    SQL> <copy>show con_name</copy>

    CON_NAME
    ------------------------------`  
    CDB$ROOT
    ```

    ```
    SQL> <copy>show con_id</copy>

    CON_ID
    ------------------------------
    1 
    ```

1.  View all PDBs in the CDB.

    ```
    SQL> <copy>show pdbs</copy>
    ```

	```
		CON_ID CON_NAME                  OPEN MODE  RESTRICTED
	---------- ------------------------- ---------- ----------
			 2 PDB$SEED                  READ ONLY  NO
			 3 ORCLPDB                   READ WRITE NO
	```

1.  Check the version of the core library components. 

    ```
    SQL> <copy>select banner from v$version;</copy>
    ```
    ```    
    BANNER
    ------------------------------------------------------------------------
	Oracle Database 23c Enterprise Edition Release 23.0.0.0.0 - Beta
    ```

1.  Verify that your Oracle Database is a multitenant container database.   

    ```
    SQL> <copy>select name, cdb, con_id from v$database;</copy>    
    ```
    ```
    NAME      CDB     CON_ID
    --------- --- ----------
    ORCL      YES          0
    ```

    The value *0* indicates that the data pertains to the entire CDB.

1.  View the instance name and the status of the CDB.

    ```
    SQL> <copy>select instance_name, status, con_id from v$instance;</copy>
    ```
    ```
    INSTANCE_NAME    STATUS           CON_ID
    ---------------- ------------ ----------
    orcl             OPEN                  0
    ```

In this lab, you connected to the SQL command line of your Oracle Database and checked container details, such as current user, container name, container ID, PDBs, and so on.

You may now **proceed to the next lab**.

## Acknowledgments

 - **Author**: Manish Garodia, Database User Assistance Development team
 - **Contributors** - <if type="hidden">Suresh Rajan, Dharma Sirnapalli, Subhash Chandra, Steven Lemme</if>
 - **Last Updated By/Date** - Manish Garodia, March 2023

<!--

To connect to your Oracle Database from a terminal, you must set the environment variables first. These variables remain in the terminal until you close the terminal window.

> Note that environment variables set in one terminal do not apply automatically to other terminals you may have. If you open a new terminal or have a terminal window already open, then you must set these variables in that terminal to connect to Oracle Database.

In this task, you will set the following environment variables for your Oracle Database.
 - *`$ORACLE_SID`*
 - *`$ORACLE_HOME`*
 - *`$ORACLE_BASE`*

1. Open a terminal window and go to the `bin` directory in Oracle home.

	```
	$ <copy>cd /u01/app/oracle/product/23.0.0/dbhome_1/bin</copy>
	```

1. Set the environment variables with the script, *oraenv*.

	```
	$ <copy>./oraenv</copy>
	```

1. When prompted for `$ORACLE_SID`, enter *orcl*.

	```
	ORACLE_SID = [oracle] ? <copy>orcl</copy>
	The Oracle base has been set to /u01/app/oracle
	```

	This command sets the variables *`$ORACLE_SID`* and the *`ORACLE_BASE`* location. It also sets the the the *`$ORACLE_HOME`* path to *`/u01/app/oracle/product/23.0.0/dbhome_1`*.

You have set the environment variables for your Oracle Database in the currently active terminal. You can now connect to Oracle Database and run the commands.


-->
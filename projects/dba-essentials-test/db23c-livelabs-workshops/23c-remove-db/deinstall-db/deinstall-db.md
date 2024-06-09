# Deinstall Oracle Database and remove Oracle home

## Introduction

This lab walks you through the steps for removing the Oracle Database software from your host. It not only shows how to delete the database but also removes Oracle home and the database components completely.

Estimated time: 10 minutes

### Objectives

Remove the Oracle Database software, delete Oracle Database, and remove *Oracle home 2* from your host system using the *deinstall* command.

> **Note:** [](include:user-data)

### Prerequisites

This lab assumes you have -

 - An Oracle Cloud Account
 - Completed all previous labs successfully

You are logged in to your host as *oracle*, the user who can remove Oracle Database.

> **Note:** [](include:example-values)

## Task 1: Remove Oracle Database software and delete Oracle Database

In this task, you will remove the database, *CDB2*, from Oracle home 2 using the *`deinstall`* command.

> **Note:** The `deinstall` command deletes Oracle Database configuration files, user data, and fast recovery area (FRA) files even if they are outside the Oracle base directory.

1. Open a terminal window and go to Oracle home 2 where the command resides.
	In the Livelabs environment, `deinstall` resides in the following directory.

    ```
	$ <copy>cd /opt/oracle/product/23c/dbhome_2/deinstall</copy>
	```

	> **Caution:** Do not shut down the database or stop any processes for the database that you are removing before running `deinstall`.

1.  Run this command to start the deinstallation process.  

    ```
	$ <copy>./deinstall</copy>
	```

    > **Note:** For every step, `deinstall` displays the values in square brackets `[ ]`. You can press **Enter** to use the default or specify a different value manually. 

	## Output

	```
	Checking for required files and bootstrapping ...
	Please wait ...
	Location of logs /opt/oracle/oraInventory/logs/

	############ ORACLE DECONFIG TOOL START ############


	######################### DECONFIG CHECK OPERATION START #########################
	## [START] Install check configuration ##


	Checking for existence of the Oracle home location /opt/oracle/product/23c/dbhome_2
	Oracle Home type selected for deinstall is: Oracle Single Instance Database
	Oracle Base selected for deinstall is: /opt/oracle
	Checking for existence of central inventory location /opt/oracle/oraInventory

	## [END] Install check configuration ##

	## [START] GIMR check configuration ##
	Checking for existence of GIMR
	GIMR Home not detected
	## [END] GIMR check configuration ##

	Network Configuration check config START

	Network de-configuration trace file location: /opt/oracle/oraInventory/logs/netdc_check2023-11-02_10-32-43AM.log
	```

1.  The window prompts to specify the listeners that you want to unconfigure.

	```
	Specify all Single Instance listeners that are to be de-configured. Enter .(dot) to deselect all.
	[LISTENER]: **Enter**
	```

    For this task, press **Enter** to remove the current listener.

	## Output

	```
	Network Configuration check config END

	Database Check Configuration START

	Database de-configuration trace file location: /opt/oracle/oraInventory/logs/databasedc_check2023-11-02_10-35-37AM.log
	```

1. The window provides an option to specify the database instances that you want to remove from the current Oracle home. 

    > **Tip:** If you have multiple database instances in an Oracle home, then you can either remove a specific database instance or remove all database instances together using `deinstall`. To specify multiple databases, enter the database name followed by a command.

	```
	Use comma as separator when specifying list of values as input

	Specify the list of database names that are configured in this Oracle home [CDB2]: **Enter**
	```

	For this task, press **Enter** to remove the default database instance from Oracle home 2.

	## Output

	```
	###### For Database 'CDB2' ######

	Single Instance Database
	The diagnostic destination location of the database: /opt/oracle/diag/rdbms/cdb2
	Storage type used by the Database: FS
	Database file location: /opt/oracle/oradata/CDB2,/opt/oracle/recovery_area/CDB2
	Fast recovery area location: /opt/oracle/recovery_area/CDB2
	database spfile location: /opt/oracle/dbs/spfileCDB2.ora
	```

1.  The `deinstall` command discovers the details of the databases automatically in the current Oracle home and asks if you want to modify them. The default option is *n*, which means no.

	```
	The details of database(s) CDB2 have been discovered automatically. Do you still want to modify the details of CDB2 database(s)? [n]: **Enter**
	```

	For this task, press **Enter** to continue with the default values.

	> **Note:** To verify each detail and to specify this information manually, enter `y`. You can then provide the details of your database, for example, the database name, storage type, location for diagnostic destination, fast recovery area, spfile, and so on. 

	## Output

	```
	Database Check Configuration END

	######################### DECONFIG CHECK OPERATION END #########################


	####################### DECONFIG CHECK OPERATION SUMMARY #######################
	Oracle Home selected for deinstall is: /opt/oracle/product/23c/dbhome_2
	Inventory Location where the Oracle home registered is: /opt/oracle/oraInventory
	Following Single Instance listener(s) will be de-configured: LISTENER
	The following databases were selected for de-configuration. The databases will be deleted and will not be useful upon de-configuration : CDB2
	Database unique name : CDB2
	Storage used : FS
	```

1.  The window awaits for your confirmation to remove the Oracle Database instance from your host.

    ```
	Do you want to continue (y - yes, n - no)? [n]: y
    ```

    Enter ***y*** to start removing the database.

	> **Tip:** The default option is **n**, which means no. If you press Enter or type **n** here, then `deinstall` exits without removing the database.

    The deinstallation process creates log files and starts removing the database.

	## Output

	```
	A log of this session will be written to: '/opt/oracle/oraInventory/logs/deinstall_deconfig2023-11-02_10-37-24-AM.out'
	Any error messages from this session will be written to: '/opt/oracle/oraInventory/logs/deinstall_deconfig2023-11-02_10-37-24-AM.err'

	######################## DECONFIG CLEAN OPERATION START ########################
	## [START] GIMR configuration update ##
	## [END] GIMR configuration update ##
	Database de-configuration trace file location: /opt/oracle/oraInventory/logs/databasedc_clean2023-11-02_10-37-25AM.log
	Database Clean Configuration START CDB2
	This operation may take few minutes.
	Database Clean Configuration END CDB2

	Network Configuration clean config START

	Network de-configuration trace file location: /opt/oracle/oraInventory/logs/netdc_clean2023-11-02_10-37-25AM.log

	De-configuring Single Instance listener(s): LISTENER

	De-configuring listener: LISTENER
		Stopping listener: LISTENER
		Listener stopped successfully.
		Deleting listener: LISTENER
		Listener deleted successfully.
	Listener de-configured successfully.

	De-configuring Naming Methods configuration file...
	Naming Methods configuration file de-configured successfully.

	De-configuring backup files...
	Backup files de-configured successfully.

	The network configuration has been cleaned up successfully.

	Network Configuration clean config END


	######################### DECONFIG CLEAN OPERATION END #########################


	####################### DECONFIG CLEAN OPERATION SUMMARY #######################
	Successfully de-configured the following database instances : CDB2
	Following Single Instance listener(s) were de-configured successfully: LISTENER
	#######################################################################


	############# ORACLE DECONFIG TOOL END #############

	Using properties file /tmp/deinstall2023-11-02_10-37-05AM/response/deinstall_2023-11-02_10-37-24-AM.rsp
	Location of logs /opt/oracle/oraInventory/logs/

	############ ORACLE DEINSTALL TOOL START ############





	####################### DEINSTALL CHECK OPERATION SUMMARY #######################
	A log of this session will be written to: '/opt/oracle/oraInventory/logs/deinstall_deconfig2023-11-02_10-37-24-AM.out'
	Any error messages from this session will be written to: '/opt/oracle/oraInventory/logs/deinstall_deconfig2023-11-02_10-37-24-AM.err'

	######################## DEINSTALL CLEAN OPERATION START ########################
	## [START] Preparing for Deinstall ##
	Setting LOCAL_NODE to localhost
	Setting CRS_HOME to false
	Setting oracle.installer.invPtrLoc to /tmp/deinstall2023-11-02_10-37-05AM/oraInst.loc
	Setting oracle.installer.local to false

	Removing directory '/opt/oracle/homes/OraDB23Home2' on node(s) 'localhost'
	## [END] Preparing for Deinstall ##

	Oracle Universal Installer clean START

	Detach Oracle home 'OraDB23Home2' from the central inventory on the local node : Done

	Delete directory '/opt/oracle/product/23c/dbhome_2' on the local node : Done

	The Oracle Base directory '/opt/oracle' will not be removed on local node. The directory is in use by Oracle Home '/opt/oracle/product/23c/dbhome_2'.

	You can find a log of this session at:
	'/opt/oracle/oraInventory/logs//Cleanup2023-11-02_10-40-22AM.log'

	Oracle Universal Installer clean END


	## [START] Oracle install clean ##


	## [END] Oracle install clean ##


	######################### DEINSTALL CLEAN OPERATION END #########################


	####################### DEINSTALL CLEAN OPERATION SUMMARY #######################
	Successfully detached Oracle home 'OraDB21Home2' from the central inventory on the local node.
	Successfully deleted directory '/opt/oracle/product/23c/dbhome_2' on the local node.
	Oracle Universal Installer cleanup was successful.

	Review the permissions and contents of '/opt/oracle' on nodes(s) 'localhost'.
	If there are no Oracle home(s) associated with '/opt/oracle', manually delete '/opt/oracle' and its contents.
	Oracle deinstall tool successfully cleaned up temporary directories.
	#######################################################################


	############# ORACLE DEINSTALL TOOL END #############
	```

	You have completed the deinstallation process and removed the database from your host.

You have successfully reached the end of this workshop on *Oracle Database Deinstallation*. 

In this workshop, you learned how to: 
 - Delete an Oracle Database from an Oracle home keeping the database software and Oracle home intact. 
 - You deleted another Oracle Database from a different Oracle home, removed the database software and the components, and also deleted the Oracle home from the host.

## Acknowledgments

 - **Author** - Manish Garodia, Database User Assistance Development team
 - **Contributors** - <if type="hidden">Subrahmanyam Kodavaluru, Suresh Rajan, Prakash Jashnani, Malai Stalin, Subhash Chandra, Dharma Sirnapalli</if>
 - **Last Updated By/Date** - Manish Garodia, November 2023

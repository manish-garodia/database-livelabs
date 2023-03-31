# Administer listener operations

## Introduction

This lab shows how to perform listener operations, such as starting and stopping the listener, checking listener status, and so on, using the listener control utility.

Estimated time: 10 minutes

### Objectives

 - Set environment variables
 - View listener configuration and status
 - Stop the listener
 - Start the listener

### Prerequisites

This lab assumes you have -

 -   An Oracle Cloud account
 -   Completed all previous labs successfully

## Task 1: Set environment variables

[](include:set-env-var)

> **Tip:** If you have reserved a Livelabs sandbox environment, then you can run the script `.set-env-db.sh` from the home location and enter the corresponding number for the `ORACLE_SID`. It sets the environment variables automatically.

## Task 2: View listener configuration

In this task, you will check whether the listener is up and running and view listener configuration. 

1. From `$ORACLE_HOME/bin`, run `lsnrctl status`. 

	```
	$ <copy>./lsnrctl status</copy>
	```

	## Output

	This command displays listener configuration and status. The values may differ depending on the system you are using.

	```
	LSNRCTL for Linux: Version 23.0.0.0.0 - Development on 31-MAR-2023 08:32:12

	Copyright (c) 1991, 2023, Oracle.  All rights reserved.

	Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=localhost.example.com)(PORT=1523)))
	STATUS of the LISTENER
	------------------------
	Alias                     LISTENER
	Version                   TNSLSNR for Linux: Version 23.0.0.0.0 - Development
	Start Date                23-MAR-2023 11:32:38
	Uptime                    7 days 20 hr. 59 min. 34 sec
	Trace Level               off
	Security                  ON: Local OS Authentication
	SNMP                      OFF
	Listener Parameter File   /u01/app/oracle/product/23.0.0/dbhome_1/network/admin/listener.ora
	Listener Log File         /u01/app/oracle/diag/tnslsnr/localhost/listener/alert/log.xml
	Listening Endpoints Summary...
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=localhost.example.com)(PORT=1523)))
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1523)))
	Services Summary...
	Service "f41450abd5c34d62e053a12f466429aa.us.oracle.com" has 1 instance(s).
	  Instance "orcl", status READY, has 1 handler(s) for this service...
	Service "f78ebbfe030b3885e0538e08466494f2.us.oracle.com" has 1 instance(s).
	  Instance "orcl", status READY, has 1 handler(s) for this service...
	Service "orcl.us.oracle.com" has 1 instance(s).
	  Instance "orcl", status READY, has 1 handler(s) for this service...
	Service "orclXDB.us.oracle.com" has 1 instance(s).
	  Instance "orcl", status READY, has 1 handler(s) for this service...
	Service "orclpdb.us.oracle.com" has 1 instance(s).
	  Instance "orcl", status READY, has 1 handler(s) for this service...
	The command completed successfully
	```

	> The Listener Control Utility displays a summary of listener configuration settings, listening protocol addresses, and the services registered with the listener.

If your Oracle Database contains PDBs, then the status displays a service for each PDB running on the database instance.

## Task 3: Stop and start the listener

The listener runs automatically when the host system starts. If a problem occurs in the system or if you manually stop the listener, then you can start the listener again from the command line. 

In this task, you will learn how to stop and start the listener.

1. From `$ORACLE_HOME/bin`, stop the listener first, if it is already running. 

	```
	$ <copy>./lsnrctl stop</copy>
	```

	## Output

	The values may differ depending on the system you are using.

	```
	LSNRCTL for Linux: Version 23.0.0.0.0 - Development on 31-MAR-2023 08:40:35

	Copyright (c) 1991, 2023, Oracle.  All rights reserved.

	Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=localhost.example.com)(PORT=1523)))
	The command completed successfully
	```

	Now that you have stopped the listener, run the following to check if you can still connect to your Oracle Database.

1. From `$ORACLE_HOME/bin`, log in to SQL Plus as the *SYSTEM* user using the service name *orcl*.

	```
	$ <copy>./sqlplus system@orcl</copy>
	```

	## Output

	```
	SQL*Plus: Release 23.0.0.0.0 - Development on Fri Mar 31 08:49:46 2023
	Version 23.1.0.0.0

	Copyright (c) 1982, 2023, Oracle.  All rights reserved.

	Enter password: 
	```

1. When prompted for password, enter the administrative password for your Oracle Database, for example *We!come1*.

	```
	ERROR:
	ORA-12541: Cannot connect. No listener at host 0.0.0.0 port 1523.
	Help: https://docs.oracle.com/error-help/db/ora-12541/
	```

	The error indicates that the listener is not running. 

	> **Note:** If the listener is not running on the host when Oracle Enterprise Manager (Oracle EM) tries to establish connection with your Oracle Database, then it returns an I/O error indicating failure.

	Exit the prompt by pressing **Ctrl + C** followed by **Enter**. 

1. Start the listener again from the $ORACLE_HOME/bin directory.

	```
	$ <copy>./lsnrctl start</copy>
	```

	## Output

	The values may differ depending on the system you are using.

	```
	LSNRCTL for Linux: Version 23.0.0.0.0 - Development on 31-MAR-2023 09:04:31

	Copyright (c) 1991, 2023, Oracle.  All rights reserved.

	Starting /u01/app/oracle/product/23.0.0/dbhome_1/bin/tnslsnr: please wait...

	TNSLSNR for Linux: Version 23.0.0.0.0 - Development
	System parameter file is /u01/app/oracle/product/23.0.0/dbhome_1/network/admin/listener.ora
	Log messages written to /u01/app/oracle/diag/tnslsnr/localhost/listener/alert/log.xml
	Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=localhost.example.com)(PORT=1523)))
	Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1523)))

	Connecting to (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=localhost.example.com)(PORT=1523)))
	STATUS of the LISTENER
	------------------------
	Alias                     LISTENER
	Version                   TNSLSNR for Linux: Version 23.0.0.0.0 - Development
	Start Date                31-MAR-2023 09:04:31
	Uptime                    0 days 0 hr. 0 min. 0 sec
	Trace Level               off
	Security                  ON: Local OS Authentication
	SNMP                      OFF
	Listener Parameter File   /u01/app/oracle/product/23.0.0/dbhome_1/network/admin/listener.ora
	Listener Log File         /u01/app/oracle/diag/tnslsnr/localhost/listener/alert/log.xml
	Listening Endpoints Summary...
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=localhost.example.com)(PORT=1523)))
	  (DESCRIPTION=(ADDRESS=(PROTOCOL=ipc)(KEY=EXTPROC1523)))
	The listener supports no services
	The command completed successfully
	```

	You have started the listener on the host again.

	> **Note:** To access Oracle Database, the listener must be up and running. 

1. View listener status as explained in the previous task.

	```
	$ <copy>./lsnrctl status</copy>
	```

	You will see that the listener service is running.

1. Check whether you can log in to SQL Plus as *SYSTEM* using the password and service name.   
   For this lab, the password is *We!come1* and the service name is *orcl*.

	```
	$ <copy>./sqlplus system/We!come1@orcl</copy>
	```

	## Output

	The values may differ depending on the system you are using.

	```
	SQL*Plus: Release 23.0.0.0.0 - Development on Fri Mar 31 09:11:48 2023
	Version 23.1.0.0.0

	Copyright (c) 1982, 2023, Oracle.  All rights reserved.

	Last Successful login time: Thu Mar 23 2023 09:15:20 +00:00

	Connected to:
	Oracle Database 23c Enterprise Edition Release 23.0.0.0.0 - Development
	Version 23.1.0.0.0

	SQL> 
	```

You can now connect to Oracle Database.

Congratulations! You have successfully completed this workshop on *Network environment configuration for Oracle Database*. 

In this workshop, you learned how to check listener status, start and stop the listener, and view network configuration of Oracle Database. 

## Acknowledgements

 - **Author**: Manish Garodia, Database User Assistance Development team
 - **Contributors**: <if type="hidden">Suresh Rajan, Prakash Jashnani, Malai Stalin, Subhash Chandra, Dharma Sirnapalli, Subrahmanyam Kodavaluru, Manisha Mati</if>
 - **Last Updated By/Date**: Manish Garodia, March 2023

<!--

## Task 1: Set the environment -- OLD

To connect to Oracle Database and run SQL commands, set the environment first.

1. Log in to your host as *oracle*, the user who can perform database administration.

1. Open a terminal window and run the command *oraenv* to set the environment variables.

	```
	$ <copy>. oraenv</copy>
	```

1. Enter the Oracle SID, for this lab it is *CDB1*.

	```
	ORACLE_SID = [oracle] ? <copy>CDB1</copy>
	The Oracle base has been set to /opt/oracle
	```

	This command also sets the Oracle home path to `/opt/oracle/product/21c/dbhome_1`.

	> **Note:** Oracle SID is case sensitive.  

1. Change the current working directory to `$ORACLE_HOME/bin`. This is the directory where the listener control utility is located.

	```
	$ <copy>cd /opt/oracle/product/21c/dbhome_1/bin</copy>
	```

You have set the environment variables for the active terminal session. You can now connect to Oracle Database and run the commands.

> **Note:** Every time you open a new terminal window, you must set the environment variables to connect to Oracle 	Database from that terminal. Environment variables from one terminal do not apply automatically to other terminals.

Alternatively, you may run the script file `.set-env-db.sh` from the home location and enter the number for `ORACLE_SID`. It sets the environment variables automatically.




-->
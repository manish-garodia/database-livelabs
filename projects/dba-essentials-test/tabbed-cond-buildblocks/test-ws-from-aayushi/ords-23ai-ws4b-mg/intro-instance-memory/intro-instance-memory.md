﻿# View and Manage Database Instance and Memory for Oracle Database 23c

## About this Workshop

This workshop features the basic know-how of the Oracle Database Instance and guides you to view the initialization parameters and memory structures of your Oracle Database. In the EM lab, manage the initialization parameters to perform critical tasks on your Oracle Database, such as administering the database instance and adjusting the size of memory components, to improve the database's performance.

In Oracle Database Actions, you use the instance viewer window to view a particular database's details.

> **Note:** Available only if you are signed in as a Database User with DBA or PDBDBA roles.

Estimated workshop time: 1 hour 50 minutes

### Objective

For Oracle Database Actions lab:

-   View Initialization Parameters

For Oracle Enterprise Manager lab:

-   View and modify the initialization parameters


### Prerequisites
This lab assumes you have -

-   An Oracle Cloud account
-   Or an Oracle account to reserve the workshop on LiveLabs
-   Oracle Enterprise Manager, Oracle Database Actions and Oracle Database installed

<if type="dba-act">

## Appendix 1: Oracle Database Actions

Oracle Database Actions is a web-based interface for on-premises Oracle Database that uses Oracle REST Data Services to provide many of the database development, management, and administration features of desktop-based Oracle SQL Developer in Autonomous Databases. The main features include running SQL statements and scripts in the worksheet, exporting data, creating RESTful web services, managing JSON collections, monitoring databases, and creating Data Modeler diagrams. You can use it without downloading or installing additional software on your system. Database Actions was earlier known as SQL Developer Web. Database Actions was earlier known as SQL Developer Web.

**About Initialization Parameters**

Initialization Parameters are used to configure the database instance, including memory structures, and define locations for database files. A database instance is a set of memory structures that manage database files.

The Parameters page has values for initialization parameters that are stored in a text-based initialization parameter file (PFILE) or binary server parameter file (SPFILE). The initialization parameter file is read at database instance startup. 

By performing this workshop in Oracle Database Actions, you will learn to view a graphical representation of information about the instance associated with a connection.**Different types of Initialization Parameters**Initialization parameters are of the following types:

-   Parameters that name entities such as files or directories
-   Parameters that set limits for a process, database resource, or the database itself
-   Parameters that affect capacity, such as the size of the SGA. These parameters are called variable parameters.

Click the next lab to **Get Started**.

## Learn More

-   [Oracle Database Actions](https://docs-uat.us.oracle.com/en/database/oracle/sql-developer-web/23.2/sdweb/changes-release-23.2.html#SDWEB-GUID-14F59AC3-485D-4EB2-8572-4A19F6BF6E05)

## Acknowledgments

-   **Author** - Aayushi Arora, Database User Assistance Development Team
-   **Contributors** - Jeff Smith, Manisha Mati
-   **Last Updated By/Date** - Aayushi Arora, September 2024
</if>

<if type="Oracle Enterprise Manager Cloud Control">

## Appendix 1: Overview of Oracle database instance and Memory Management

An Oracle Database system consists of an Oracle Database and an instance, also known as *database instance*. The instance contains a set of background processes that operates on the stored data and the shared allocated memory that the processes use. You can start up or shut down the Oracle instance as the `SYS` user with SYSDBA privileges.

Each instance has an instance ID, also known as a *System ID (SID)*. There are multiple Oracle Databases on a host computer, each with its own set of data files. You must identify the instance to which you want to connect. For a local connection, you identify the instance by setting operating system environment variables `ORACLE_SID` and `ORACLE_HOME`.

### Starting the database instance

The process of starting the instance is as follows.

1.  **Start** the instance using Oracle Enterprise Manager or SQL command line.  Oracle reads the initialization parameter file, allocates the *System Global Area (SGA)* memory, and starts the background processes for the instance.

2.  The database is then in the **mount** state. This state enables the administrators to perform certain functions which they cannot perform when other users are accessing the database.

3.  After mounting the database, the instance **opens** the redo log files and data files for the database. The database is now open and available for all user access.

The default startup mode for the database is `OPEN` which completes the above three stages in sequence. You can start the instance in the following modes.

- `NOMOUNT`— Starts up the instance without mounting the database.
- `MOUNT`— Starts up the instance and mounts the database, but leaves it closed. This state allows certain DBA activities but does not allow general access to the database.
- `OPEN` — Starts up the instance, mounts and opens the database. You can do this in unrestricted mode, allowing access to all users, or in restricted mode, allowing access for database administrators only.
- `FORCE`— Forces the instance to start up after a startup problem.

### Shutting down the database instance

The process of shutting down the instance is the reverse of starting it. It includes the following stages.

1.  Shut down the database using Oracle Enterprise Manager or SQL*Plus command. Data files and log files are closed. Users can no longer access the database after it is shut down.

2.  The Oracle instance dismounts the database and updates relevant entries in the control file to record a clean shutdown. The control file is closed. The database is now closed and only the instance remains.

3.  The Oracle instance stops the background processes of the instance and deallocates the shared memory used by the SGA.

You can shut down an instance in the following modes.

- `NORMAL` — The default shutdown mode. It takes long time to shut down.
- `IMMEDIATE` — Shuts down the database quickly.
- `TRANSACTIONAL` — Completes the active transaction and then shuts down the database.
- `ABORT` — Shuts down the database instantaneously without waiting for the transactions to complete.
    > **Note:** Use it in emergency situations only because it can cause loss of data.

- `TIMEOUT` — Waits for active users to disconnect or for the transactions to complete within a limited waiting period. If all events blocking the shutdown do not occur within one hour, the `SHUTDOWN` operation aborts.

### Initialization Parameters

Managing database instance includes configuring parameters that affect the basic operation of the Oracle instance. These parameters are called *I**nitialization Parameters*. The database instance reads the initialization parameters from the `INIT.ORA` file at startup.

During installation, when you select a preconfigured database workload available in Oracle Database Configuration Assistant (DBCA), the Initialization Parameters are optimized for typical use in the environment that you specified. As the number of database users increases and the workload increases, you might have to alter some initialization parameters.

The Initialization Parameters are a very important part of Oracle Database. You must have the basic parameters set for the database to run properly and efficiently. The database will not startup without a valid initialization parameter file. The file is only read at startup and contains the information required to set up the SGA.

The following are two types of parameter files:

-   **Server parameter file (SPFile)**- This is the preferred form of initialization parameter file. It is a binary file that can be written to and read by the database. It is stored on the host computer on which Oracle Database is running.

    > **Note:** When changing an initialization parameter in the SPFile, you can also specify that the in-memory value be changed, so that your change is reflected immediately in the current instance. If you do not change the in-memory value, then the change does not take effect until you shut down and restart the database.

-   **Text initialization parameter file (PFile)**- This type of initialization parameter file can be read by the database server, but it is not written to by the server. In this file, you can set initialization parameters with a text editor for them to be persistent across shutdown and startup.

Oracle reads the initialization parameter values from either a **SPFile** or **PFile** when the Oracle Database starts. The parameters inform the Oracle Database on how much memory to allocate, where to put files related to the database and the location of existing data files.

### About Instance Memory Management

The size of the instance memory structures affects the performance of the Oracle Database server and is controlled by initialization parameters. When you create a database with DBCA, the memory parameters are automatically set to optimal values based on the database workload, such as data warehouse, general purpose, or transaction processing. However, as your database usage expands, you can alter the settings of the memory parameters.

The basic memory structures associated with Oracle Database include:

-   **System Global Area (SGA)**The SGA is a group of shared memory structures, known as SGA components, that contain data and control information for one Oracle database instance. The SGA is shared by all server and background processes. Examples of data stored in the SGA include cached data blocks and shared SQL areas.

-   **Program Global Area (PGA)**The PGA is a memory region that contains data and control information for a server process. It is nonshared memory created by Oracle Database when a server process is started. Access to the PGA is exclusive to the server process. There is one PGA for each server process. Background processes also allocate their own PGAs. 

### Automatic Memory Management

Oracle Database can manage the SGA memory and instance PGA memory. You designate only the total memory size to be used by the instance, and the database dynamically exchanges memory between the SGA and the instance PGA as needed to meet processing demands. This capability is referred to as *Automatic Memory Management*. In this memory management mode, the database also dynamically tunes the sizes of the individual SGA components and the sizes of the individual PGAs.

Upon installation, you can let Oracle Database manage the memory automatically, or select to manually configure the instance memory structures. For both manual and automatic memory management, Oracle Database sends alerts which identify memory sizing problems that require your attention.

The simplest way to manage instance memory is to allow the database instance to automatically manage and tune it for you. You set a target memory size initialization parameter (`MEMORY_TARGET`) and optionally a maximum memory size initialization parameter (`MEMORY_MAX_TARGET`). The total memory that the instance uses remains relatively constant, based on the value of `MEMORY_TARGET`, and the instance automatically distributes memory between the system global area (SGA) and the instance program global area (instance PGA). As memory requirements change, the instance dynamically redistributes memory between the SGA and instance PGA.

If you do not enable Automatic Memory Management for your Oracle Database, then you must manually set the memory for both SGA and PGA. While installing Oracle Database, the installer gives you an option to enable Automatic Memory Management. If you did not enable Automatic Memory Management during database installation, you can enable it as explained in this workshop.

Click on the next lab to **Get Started**.

## Learn More

- [Database Reference - Basic Initialization Parameters](https://docs.oracle.com/en/database/oracle/oracle-database/23/refrn/basic-initialization-parameters.html#GUID-D75F1A77-47E2-4F35-B145-44B3A10ED85C)

- [Database Concepts - Oracle Instance Architecture](https://docs.oracle.com/en/database/oracle/oracle-database/23/cncpt/index.html#Oracle%C2%AE-Database)

## Acknowledgments

-   **Author** - Aayushi Arora, Database User Assistance Development Team
-   **Contributors** - Manish Garodia, Jayaprakash Subramanian, Ashwini R
-   **Last Updated By/Date** - Aayushi Arora, May 2024
</if>
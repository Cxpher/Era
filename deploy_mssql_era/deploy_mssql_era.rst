.. _mssqldeploy:

-------------------------
Deploying MSSQL with Era
-------------------------

**In this lab, you will use Era to deploy a new MSSQL database server.**

Creating MSSQL database server with Nutanix Era
++++++++++++++++++++++++++++++++++++

In this exercise you will deploy a fresh MSSQL database using a Nutanix Era pre-created MSSQL 2016 ‘Software Profile’. You will name these instances after your user alias (eg. User01_Name of Database).

|

.. note::

   In the lab screenshots, the alias 'XYZ or xyz' will be used. In your own lab attempts, this will be replaced by your own user alias.

|

#. Within **Era**, select **Databases** from the dropdown menu, and **Sources** from the left-hand menu.

#. Click **+ Provision > Microsoft SQL Server > Database**.

#. In the **Provision a SQL Server Database** wizard, fill out the following fields to configure the Database Server:

   - **Database Server VM** - Create New Server
   - **Database Server Name** - *Alias*\ -MSSQL
   - **Description** - (Optional)
   - **Software Profile** - DEFAULT_MSSQL_2016

|

.. note::

  .. raw:: html

    <strong><font color="red">IMPORTANT -  When selecting the software profile, ensure the 1st version of the software is selected. This will allow us to patch with the SQL 2016 SP1 patch later on in the patching lab.</font></strong>

|

   .. figure:: images/depmssql1-0.png

|

   .. figure:: images/depmssql1-1.png

|

   - **Compute Profile** - db.r.large
   - **Network Profile** - DEFAULT_MSSQL_NETWORK
   - Select **Join Domain**
   - **Windows Domain Profile** - NTNXLAB
   - **Windows License Key** - (Leave Blank)
   - **Administrator Password** - Nutanix/4u
   - **Instance Name** - MSSQLSERVER
   - **Server Collation** - (Leave Default)
   - **Database Parameter Profile** - DEFAULT_SQLSERVER_INSTANCE_PARAMS
   - **SQL Server Authentication Mode** - Windows Authentication

|

   .. figure:: images/depmssql1.png

|

   .. note::

         There is no need to check the checkbox for 'Grant Access to an Account for Windows/SQL Server Administration'.

|

   .. note::

      An **Instance Name** is the name of the database server, this is not the hostname. The default is **MSSQLSERVER**. You can install multiple separate instances of MSSQL on the same server as long as they have different instance names. This was more common on a physical server, however, you do not need additional MSSQL licenses to run multiple instances of SQL on the same server.

      **Server Collation** is a configuration setting that determines how the database engine should treat character data at the server, database, or column level. SQL Server includes a large set of collations for handling the language and regional differences that come with supporting users and applications in different parts of the world. A collation can also control case sensitivity on a database. You can have different collations for each database on a single instance. The default collation is **SQL_Latin1_General_CP1_CI_AS** which breaks out like below:
      - **Latin1** makes the server treat strings using charset latin 1, basically **ASCII**
      - **CP1** stands for Code Page 1252. CP1252 is  single-byte character encoding of the Latin alphabet, used by default in the legacy components of Microsoft Windows for English and some other Western languages
      - **CI** indicates case insensitive comparisons, meaning **ABC** would equal **abc**
      - **AS** indicates accent sensitive, meaning **ü** does not equal **u**

      **Database Parameter Profiles** define the minimum server memory SQL Server should start with, as well as the maximum amount of memory SQL server will use. By default, it is set high enough that SQL Server can use all available server memory. You can also enable contained databases feature which will isolate the database from others on the instance for authentication.

|

4. Click **Next**, and fill out the following fields to configure the Database:

   - **Database Name** - *Alias*\ -fiesta
   - **Description** - (Optional)
   - **Size (GiB)** - 200 (Default)
   - **Database Parameter Profile** - DEFAULT_SQLSERVER_DATABASE_PARAMS

|

   .. figure:: images/depmssql2.png

|

   .. note::

      Common applications for pre/post-installation scripts include:

      - Data masking scripts
      - Register the database with a database monitoring solution
      - Scripts to update DNS and/or IPAM
      - Scripts to automate application setup

|

5. Click **Next** and fill out the following fields to configure the Time Machine for your database:

|

.. note::

  .. raw:: html

    <strong><font color="red">It is critical to select the BRONZE SLA in the following step. The default BRASS SLA does NOT include Continuous Protection snapshots.</font></strong>

|

   - **Name** - *Alias*\ -fiesta_TM (Default)
   - **Description** - (Optional)
   - **SLA** - DEFAULT_OOB_BRONZE_SLA
   - **Schedule** - (Defaults)

|

   .. figure:: images/depmssql3.png

|

6. Click **Provision** to begin creating your new database server VM and **fiesta** database.

7. Select **Operations** from the dropdown menu to monitor the provisioning. This process should take between 20-60 minutes.

   .. figure:: images/22.png

   .. note::

      Observe the step for applying best practices in **Operations**.

      Some of the best practices automatically configured by Era include:
      - Distribute databases and log files across multiple vDisks.
      - Do not use Windows dynamic disks or other in-guest volume management
      - Distribute vDisks across multiple SCSI controllers (for ESXi)
      - For each database, use multiple data files: one file per vCPU.
      - Configure initial log file size to 4 GB or 8 GB and iterate by the initial amount to reach the desired size.
      - Use multiple TempDB data files, all the same size.
      - Use available hypervisor network control mechanisms (for example, VMware NIOC).

8. Proceed to the following exercises only after the database has completed provisioning. This process should take approximately 30 minutes.

Exploring the provisioned database server
++++++++++++++++++++++++++++++++++++

#. Within *Prism Element*, select **Storage > Table > Volume Groups**.

#. Select the **ERA_**\ *Alias*\ **_MSSQL_\** Volume Group (VG), and observe the layout by clicking on the **Virtual Disk** tab. What does this tell us?

|

   .. figure:: images/23.png

|

#. View the disk layout of your newly provisioned VM in Prism. What are all of these disks, and how is this different from the original VM we registered?

|

   .. figure:: images/24.png

|

#. Within Prism, note the IP address of your *Alias*\ **-MSSQL** VM, and connect to it via RDP/Console using the following credentials:
   - **User Name** - NTNXLAB\\Administrator
   - **Password** - nutanix/4u

#. Open **Start > Run > diskmgmt.msc** to view the in-guest disk layout. Right-click an unlabeled volume and select **Change Drive Letter and Paths** to view the path to which Era has mounted the volume. Note there are dedicated drives corresponding to SQL data and log locations, similar to the original SQL Server to which you manually applied best practices.

|

   .. figure:: images/25.png

|

Migrating Fiesta app data
+++++++++++++++++++++++++

In this exercise you will import data directly into your database from a backup exported from another database. While this is a suitable method for migrating data, it potentially involved downtime for an application, or our database potentially not having the very latest data.

Another approach could involve adding your new Era database to an existing database cluster (AlwaysOn Availability Group - AAG) and having it replicate to your Era provisioned database. This kind of application-level synchronous or asynchronous replication can be used to provide additional benefit to using Era, such as cloning and Time Machine to databases whose production instances run on bare metal and/or non-Nutanix infrastructure.

#. From your *Alias*\ **-MSSQL** session, launch **Microsoft SQL Server Management Studio**, and click **Connect** to authenticate as the currently logged in user.

#. Expand the **Databases** > *Alias*\ -fiesta, and note that it contains no tables.

#. Right-click the *Alias*\ -fiesta database, and select **New Query** from the menu to import your production application data.

#. Copy and paste the following script into the query editor (right-hand side), and click **Execute**.

   .. literalinclude:: FiestaDB-MSSQL.sql
     :caption: FiestaDB Data Import Script
     :language: sql

   .. figure:: images/28.png

   .. note:: The status bar at the bottom of the screen should read *Query executed successfully*.

#. Optionally, you can view the contents of the database by performing another query, this time using the following script:

   .. code-block:: sql

      SELECT * FROM dbo.products
      SELECT * FROM dbo.stores
      SELECT * FROM dbo.InventoryRecords

   .. figure:: images/29.png

#. Within Era, select **Time Machines** from the dropdown.

#. Select your *Alias*\ **-fiesta_TM** Time Machine, and then click **Actions > Log Catch Up > Yes** to ensure the imported data has been committed to disk prior to the cloning operation in the next lab.

Takeaways
+++++++++

What are the key things we learned in this lab?

- Existing databases can be easily onboarded into Era, and turned into templates
- Existing brownfield databases can also be registered with Era
- Profiles allow administrators to provision resources based on published standards
- Customizable recovery SLAs allow you to tune continuous, daily, and monthly RPO based on your app's requirements
- Era provides One-click provisioning of multiple database engines, including automatic application of database best practices

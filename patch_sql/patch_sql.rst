.. _patch_sql:

----------------------
Patching MSSQL with Era
----------------------

. note::

  Notable links 
  
  - `KB3177312 - SQL Server 2016 build versions => https://support.microsoft.com/en-us/help/3177312/kb3177312-sql-server-2016-build-versions - Refer to this article for Service Pack (SP) and Cumulative Update (CU) information. Please note that Microsoft has deprecated the use of the term *Service Pack* on SQL versions after 2016.
   
  -  SQL2016 SP1 CU15 - https://www.microsoft.com/en-us/download/details.aspx?id=54613

Patching your database server with patch software profile
++++++++++++++++++++++++++++++++++++++++

Perform the following procedure to apply updates from the available software profile versions to a provisioned/registered database server VM.

#. Within Era, select **Database Server VMs** from the drop-down list.

#. Click on **List** from the left-hand side, then click the *Alias*\ **-MSSQL** database server VM for which you want to update the software profile version. The *Database Server VM Summary* page appears.

   .. note::

      You could also select the clone database or clone a fresh database from a prod database server to patch, create a patch software profile with and use to patch your prod database servers with confidence in a production setting.

#. Under Profiles, note that the newer, published software profile is being recommended as an available update to the database server. Click Update.

|

   .. figure:: images/patch222.png

|

   .. note::

      The `Update` option only appears when a new software profile version is available.

|

#. Select the following in the indicated fields:

   - **Software Profile** DEFAULT_SQL2016_SP1_CU15

|

   .. figure:: images/four.png

#. Confirm the update by typing *Alias*\ **-MSSQL** in the text box, and click **Update**.

   A message appears at the top indicating that the operation to update a database has started. Click the message to monitor the progress of the operation. Alternatively, select **Operations** in the drop-down list of the main menu to monitor the progress of the operation.

#. You can demonstrate the patch process was successful, by opening MS SQL Server Management Studio, and observing the server version and comparing that version with the SQL Server 2016 build versions web page.

   .. figure:: images/4a.png

Takeaways
+++++++++

What are the key things we learned in this lab?

- Software Profiles can be versioned and used to deploy consistent updates to existing database servers
- Software Profiles also simplify the patching process reducing the amount of manual patching needed in an environment
- Scheduling updates can be used to hit change windows or SLA uptime windows

.. _admin_mssqldb:

--------------------------
DB administration with Era
--------------------------

**In this lab you will perform some administrative tasks on your deployed MSSQL database server.**

Recovering database from snapshot
++++++++++++++++++++++

In the previous lab, you have already populated the database with some data. Therefore, in this lab, you will take a snapshot of that data first.

Take manual snapshot of your database
................................

#. Within **Era**, select **Databases** from the dropdown menu, and then **Sources** from the left-hand menu.

#. Click on the *Time Machine* for your Database (ex. *Alias*\ -fiesta_TM).

|

   .. figure:: images/admin1.png

|

#. Click **Actions > Snapshot**.

|

   .. figure:: images/admin2.png

   - **Snapshot Name** - *Alias*\ -MSSQL-1st-Snapshot

|

   .. figure:: images/admin3.png

|

#. Click **Create**

#. Select **Operations** from the dropdown menu to monitor the registration. This process should take approximately 2-5 minutes.

|

   .. figure:: images/9a.png

|

Clone your database server & database
+++++++++++++++++++++++++++++++++++++

#. In **Era**, select **Time Machines** from the dropdown menu, and then select *Alias*\ -fiesta_TM.

#. Click **Actions > Create Database Clone > Database**.

   - **Snapshot** - *Alias*\ -MSSQL-1st-Snapshot (Date Time)

|

   .. figure:: images/10.png

|

#. Click **Next**.

   - **Database Server** - Create New Server
   - **Database Server Name** - *Initials*\ -MSSQL_Clone1
   - **Compute Profile** - db.r.large
   - **Network Profile** - Primary-MSSQL-Network
   - **Administrator Password** - Nutanix/4u

|

   .. figure:: images/11.png

|

#. Click **Next**.

   - **Clone Name** - *Initials*\ -LABSQLDB_Clone1
   - **Database Name on VM** - SampleDB_Clone1
   - **Instance Name** - MSSQLSERVER

|

   .. figure:: images/12.png

|

#. Click **Clone**

#. Select **Operations** from the dropdown menu to monitor the registration. This process should take approximately 10-15 minutes.

Delete table and refresh clone
++++++++++++++++++++++++++++++

There are times when a table or other data gets deleted (by accident), and you would like to get it back. Here we will delete a table and use Era to refresh the clone from the last snapshot we took.

Delete Table
............

#. RDP/Console into your *Alias*\ -MSSQL_Clone1 VM.

#. Open SQL Server Managment Studio (SSMS), choose **Windows Authentication** from the *Authentication* dropdown, and click **Connect**.

#. Expand **Databases > SampleDB_Clone1 > Tables**.

#. Right-click on *dbo.Products*, select **Delete**, and then **OK**.

Refresh your clone
..................

#. Within **Era**, select **Databases** from the dropdown menu, and then **Clones** from the left-hand menu.

#. Select the clone for your database *Initials*\ -LABSQLDB_Clone1, and click **Refresh**.

#. Click the radio button for *Snapshot*, and choose the entry for *Initials*\ -MSSQL-1st-Snapshot (Date Time).

#. Click **Refresh**.

#. Select **Operations** from the dropdown menu to monitor the registration. This process should take approximately 2-5 minutes.

   .. figure:: images/13.png

Verify the previously deleted table has been restored
.....................................................

#. RDP/Console into your *Initials*\ -MSSQL_Clone1 VM.

#. Open SQL Server Managment Studio (SSMS), choose **Windows Authentication** from the *Authentication* dropdown, and click **Connect**.

#. Expand **Databases > SampleDB_Clone1 > Tables**.

#. Right-click on on *Tables*, and choose **Refresh**.

#. Verify the table *dbo.Products* has been restored.

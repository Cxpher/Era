.. _admin_oracle:

--------------------------
DB administration with Era
--------------------------

**In this lab you will perform some administrative tasks on your deployed Oracle Database Server**

Explore your database
++++++++++++++++++++++

#. In **Era**, select **Databases** from the dropdown menu and **Sources** from the lefthand menu.

#. Click into your *Alias*\ _proddb, this will take you back into the Database Summary page. This page provides summary details of the Database, Database Server VM, Time Machine & relevant Profiles used to provision.

|

    - **Database Summary:**

    .. figure:: images/2.png

|

    - **Database Server VM:**

    .. figure:: images/3.png

|

    - **Time Machine:**

    .. figure:: images/4.png

|

    - **Profiles:**

    .. figure:: images/5.png

|

Recovering database from snapshot
++++++++++++++++++++++++

Before we take a manual snapshot of our database, let's write a new table into our *Alias*\ _Oracle_Prod database.

Write New Table Into Database
.............................

|

#. SSH (Terminal/Putty) into your *Alias*\ **_Oracle_Prod** VM
   - **User Name** - oracle
   - **Password** - Nutanix/4u

#. Launch **sqlplus**

     .. code-block:: Bash

       sqlplus / as sysdba

#. Execute the following to create a table:

     .. code-block:: Bash

       CREATE TABLE testlabtable
       (
       column1 VARCHAR(30),
       column2 DATE
       );

#. Verify the new table is there by executing the following to list the table:

     .. code-block:: Bash

       select owner as schema_name,
       table_name
       from sys.all_tables
       where table_name like 'TEST%';

|

Take manual snapshot of your database
................................

|

1. Within **Era**, select **Databases** from the dropdown menu, and then **Sources** from the left-hand menu.

2. Click on the Time Machine for your Database *Alias*\ _proddb_TM.

|

   .. figure:: images/6.png

|

3. Click **Yes**. This should take approximately 2-3 minutes to complete.

4. Click **Actions > Snapshot**. Enter *Alias*\ _proddb-1st-Snapshot as the *Snapshot Name*, and click **Create**.

|

   .. figure:: images/7.png

|

5. Select **Operations** from the dropdown menu to monitor the registration. This process should take approximately 2-5 minutes.

|

Clone your database server & database
+++++++++++++++++++++++++++++++++++++

#. Within **Era**, select **Time Machines** from the dropdown menu, and then select *Alias*\ _proddb_TM.

#. Click **Actions > Create Single Instance Database Clone**.

#. Click the radio button for *Snapshot*, and choose the entry for *Alias*\ proddb-1st-Snapshot (Date Time). Click **Next**.

|

   .. figure:: images/9.png

|

4. Fill out the following fields, and click **Next**.

   - **Database Server VM** - Create New Server
   - **Database Server VM Name** - *Alias*\ _oracle_prod_Clone1
   - **Compute Profile** - db.r.large
   - **Network Profile** - DEFAULT_ORACLE_NETWORK
   - **SSH Public Key Through** - Select **Text**. Copy and paste the following into the text box.

|

   ::

      ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAii7qFDhVadLx5lULAG/ooCUTA/ATSmXbArs+GdHxbUWd/bNGZCXnaQ2L1mSVVGDxfTbSaTJ3En3tVlMtD2RjZPdhqWESCaoj2kXLYSiNDS9qz3SK6h822je/f9O9CzCTrw2XGhnDVwmNraUvO5wmQObCDthTXc72PcBOd6oa4ENsnuY9HtiETg29TZXgCYPFXipLBHSZYkBmGgccAeY9dq5ywiywBJLuoSovXkkRJk3cd7GyhCRIwYzqfdgSmiAMYgJLrz/UuLxatPqXts2D8v1xqR9EPNZNzgd4QHK4of1lqsNRuz2SxkwqLcXSw0mGcAL8mIwVpzhPzwmENC5Orw==

|

   .. figure:: images/10.png

|

5. Fill out the following fields, and click **Next**.

   - **Name** - *Alias*\ _proddb_Clone1
   -  **SID** - *Alias*\ prod
   -  **SYS and SYSTEM Password** - Nutanix/4u
   -  **Database Parameter Profile** - ORACLE_r.large_PARAMS

|

   .. figure:: images/11.png

|

6. Click **Clone**.

7. Select **Operations** from the dropdown menu to monitor the registration. This process should take approximately 30-50 minutes.

Delete table and refresh clone
++++++++++++++++++++++++++++++

There are times when a table or other data gets deleted (accidentally or maliciously), and you would like to recover it. Here we will delete a table, and then use the Era *Clone Refresh* action from the last snapshot to restore it.

Delete table
............

#. SSH (Terminal/Putty) into your *Alias*\ _proddb_Clone1 VM
   - **User Name** - oracle
   - **Password** - Nutanix/4u

#. Launch **sqlplus**

   .. code-block:: Bash

     sqlplus / as sysdba

#. Execute the following to Drop the table:

   .. code-block:: Bash

     DROP TABLE testlabtable;

#. Verify the table is gone by executing the following to list the table:

   .. code-block:: Bash

     select owner as schema_name,
     table_name
     from sys.all_tables
     where table_name like 'TEST%';

|

Refresh clone
.............

#. In **Era**, select **Databases** from the dropdown menu and **Clones** from the lefthand menu.

#. Select the clone for your Database *Alias*\ _proddb and select - **Snapshot** - *Alias*\ _proddb-1st-Snapshot (Date Time)

#. Click **Refresh**

|

   .. figure:: images/13.png

|

#. Select **Operations** from the dropdown menu to monitor the registration. This process should take approximately 2-5 minutes.

|

Verify that table is back
....................

#. SSH (Terminal/Putty) into your *Alias*\ _proddb_Clone1 VM

   - **User Name** - oracle
   - **Password** - Nutanix/4u


   .. code-block:: Bash

     ssh oracle@PRODDB_Clone1 IP

#. Launch **sqlplus**

   .. code-block:: Bash

     sqlplus / as sysdba

#. Verify the table is back by executing the following to list the table:

   .. code-block:: Bash

     select owner as schema_name,
     table_name
     from sys.all_tables
     where table_name like 'TEST%';

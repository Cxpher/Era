.. _deploy_oracle_era:

-------------------------
Deploying Oracle Single Instance Database with Nutanix Era
-------------------------

Create Oracle Database Server with Nutanix Era
+++++++++++++++++++++++++++++

In this exercise you will deploy a fresh Oracle database using a Nutanix Era pre-created Oracle 19c 'Software Profile'. You will name these instances after your user alias (eg. User01_Name of Database).

|

.. note::

   In the lab screenshots, the alias 'XYZ or xyz' will be used. In your own lab attempts, this will be replaced by your own user alias.

|

#. Select **Databases** from the dropdown menu, and then **Sources** from the left-hand menu.

#. Click **+ Provision > Oracle > Single Instance Database** and fill out the following fields:

   - **Database Server** - Create New Server
   - **Database Server Name** - *Alias*\ _Oracle_Prod
   - **Description** - (Optional)
   - **Software Profile** - DEFAULT_Oracle_19c
   - **Compute Profile** - db.r.large
   - **Network Profile** - DEFAULT_ORACLE_NETWORK (be careful NOT to select DEFAULT_OOB_ORACLE_NETWORK)
   - Select **Enable High Availability**
   - **SYS ASM Password** - Nutanix#4u
   - **ASM Driver** - None
   - **SSH Public Key for Node Access** - Select **Text** and copy and paste the below into the *Text* box.

|

   ::

      ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAii7qFDhVadLx5lULAG/ooCUTA/ATSmXbArs+GdHxbUWd/bNGZCXnaQ2L1mSVVGDxfTbSaTJ3En3tVlMtD2RjZPdhqWESCaoj2kXLYSiNDS9qz3SK6h822je/f9O9CzCTrw2XGhnDVwmNraUvO5wmQObCDthTXc72PcBOd6oa4ENsnuY9HtiETg29TZXgCYPFXipLBHSZYkBmGgccAeY9dq5ywiywBJLuoSovXkkRJk3cd7GyhCRIwYzqfdgSmiAMYgJLrz/UuLxatPqXts2D8v1xqR9EPNZNzgd4QHK4of1lqsNRuz2SxkwqLcXSw0mGcAL8mIwVpzhPzwmENC5Orw==


|

   .. note::

         By selecting Enable High Availability, Oracle Grid is configured as part of the deployment and Oracle Automatic Storage Management (ASM) is used for volume management. Without High Availability enabled, Linux LVM and file systems would be used for database storage. Grid and ASM are required for clustered Oracle RAC deployments.

|

   .. figure:: images/4.png

|

#. Click **Next**, and fill out the following fields to configure the Database:

   -  **Database Name** - *Alias*\ _proddb
   -  **SID** - *Alias*\ prod
   -  **SYS and SYSTEM Password** - Nutanix#4u
   -  **Database Parameter Profile** - ORACLE_r.large_PARAMS

|

   .. note::

         There is no need to check the checkbox for 'Encryption'.

|

   .. figure:: images/5.png

|

   .. note::

      For each database engine supported by Era, you have the opportunity to run scripts before and after database creation. Common use cases include:

      - Data masking scripts
      - Register the database with DB monitoring solution
      - Scripts to update DNS/IPAM
      - Scripts to automate application setup, such as app-level cloning for Oracle PeopleSoft

      Additonally, by enforcing data-at-rest encryption in the database layer can prevent would-be attackers from bypassing the database, and reading sensitive information directly from storage.

|

#. Click **Next** and fill out the following fields to configure the Time Machine for your database:

   - **Name** - *Alias*\ _proddb_TM (Default - Should automatically be populated with your alias - There is no need to change this)
   - **Description** - (Optional)
   - **SLA** - DEFAULT_OOB_GOLD_SLA
   - **Schedule** - (Defaults)

|

   .. figure:: images/6.png

|

#. Click **Provision** to begin creating your new database server VM containing your *Initials*\ _proddb database.

#. Select **Operations** from the dropdown menu to monitor the provisioning.

#. Proceed to the following exercises only after the database has completed provisioning. This process should take approximately 30 minutes.

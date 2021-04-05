.. _deploy_oracle_era:

-------------------------
Deploying Oracle DB with Era
-------------------------

**In this lab, you will use Era to deploy a new Oracle database server.**

Create Oracle database server with Nutanix Era
+++++++++++++++++++++++++++++

In this exercise you will deploy a fresh Oracle database using a Nutanix Era pre-created Oracle 19c 'Software Profile'. You will name these instances after your user alias (eg. User01_Name of Database).

|

.. note::

   In the lab screenshots, the alias 'XYZ or xyz' will be used. In your own lab attempts, this will be replaced by your own user alias.

|

#. Within **Era**, select **Databases** from the dropdown menu, and **Sources** from the left-hand menu.

#. Click **+ Provision > Oracle > Single Instance Database** and fill out the following fields in the **Provision an Oracle Single Instance Database** wizard:

   - **Database Server** - Create New Server
   - **Database Server Name** - *Alias*\ _Oracle_Prod
   - **Description** - (Optional)
   - **Software Profile** - DEFAULT_Oracle_19c

|

.. note::

  .. raw:: html

    <strong><font color="red">IMPORTANT -  When selecting the software profile, ensure the 1st version of the software is selected. This will allow us to patch with the PSU later on in the patching lab.</font></strong>

|

   .. figure:: images/7.png

|

   .. figure:: images/8.png

|

   - **Compute Profile** - db.r.large
   - **Network Profile** - DEFAULT_ORACLE_NETWORK (be careful NOT to select DEFAULT_OOB_ORACLE_NETWORK)
   - Select **Enable High Availability**
   - **SYS ASM Password** - Nutanix/4u
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

3. Click **Next**, and fill out the following fields to configure the Database:

   -  **Database Name** - *Alias*\ _proddb
   -  **SID** - *Alias*\ prod
   -  **SYS and SYSTEM Password** - Nutanix/4u
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

4. Click **Next** and fill out the following fields to configure the Time Machine for your database:

   - **Name** - *Alias*\ _proddb_TM (Default - Should automatically be populated with your alias - There is no need to change this)
   - **Description** - (Optional)
   - **SLA** - DEFAULT_OOB_GOLD_SLA
   - **Schedule** - (Defaults)

|

   .. figure:: images/6.png

|

5. Click **Provision** to begin creating your new database server VM containing your *Initials*\ _proddb database.

6. Select **Operations** from the dropdown menu to monitor the provisioning.

7. Proceed to the following exercises only after the database has completed provisioning. This process should take approximately 30 minutes.

Takeaways
+++++++++

What are the key things we learned in this lab?

- Existing databases can be easily onboarded into Era, and turned into templates
- Existing brownfield databases can also be registered with Era
- Profiles allow administrators to provision resources based on published standards
- Customizable recovery SLAs allow you to tune continuous, daily, and monthly RPO based on your app's requirements
- Era provides One-click provisioning of multiple database engines, including automatic application of database best practices

.. _patching_oracle:

------------------------
Patching Oracle with Era
------------------------

Maintaining consistent patch levels across database servers in a traditional environment can be a very difficult, and time-consuming process. Each quarter, Oracle releases a grouping of patches referred to as Patch Set Updates (PSU). Era makes this simple by providing a means of patching via software profiles. Individual or groups of database servers can be patched, or rolled back through Era, using the web interface, CLI, or API.

**In this lab you will walk through the patching of both Oracle and Grid software for an Oracle 19c database using Era.**

#. Select VM and click **Actions > Power On**.


Creating Software Profile with Updates
++++++++++++++++++++++++++++++++++++++++

#. Return to **Era > Database Server VMs > List** and click your *Initials*\ **_oracle_prod** database server.

#. Under **Profiles**, note that the newer, published software profile is being recommended as an available update to the database server. Click **Update**.

   .. figure:: images/15.png

#. Select the desired patch profile from the drop down menu (in a real environment you could potentially publish several options) and click **Patch 1 Database** to begin the update process.

   .. note::

      Era also offers the ability to schedule patching application, allowing you to select a pre-determined maintenance window. For clustered database deployments, Era supports rolling updates, ensuring database accessibility throughout the update process.

      .. figure:: images/17.png

#. Monitor the progress on the **Operations** page. This process should take approximately 25 minutes.

   During the patching process, Era will gracefully bring down database and Grid services, shut down the VM, replace the relevant virtual disks with thin clones from the 2.0 Software Profile, and bring the database server back online.

   .. figure:: images/18.png

#. Once the patching operation has completed, you can easily validate the VM is running with the patched software outside of Era. SSH into your *Initials*\ **_oracle_prod** VM with the following credentials:

   - **User Name** - oracle
   - **Password** - Nutanix/4u

#. Execute the following command to display installed patch versions:

   ::

    $ORACLE_HOME/OPatch/opatch lsinventory | egrep 'appl|desc'

   .. figure:: images/19.png

Takeaways
+++++++++

What are the key things we learned in this lab?

- Software Profiles can be versioned and used to deploy consistent updates to existing database servers
- Software Profiles also simplify the patching process reducing the amount of manual patching needed in an environment
- Scheduling updates can be used to hit change windows or SLA uptime windows.

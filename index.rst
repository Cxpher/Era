.. Era documentation master file, created by
   sphinx-quickstart on Sun Apr  4 12:45:29 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Nutanix Era database workshop!
===============================

.. toctree::
    :maxdepth: 2
    :caption: MSSQL with Nutanix Era (Option A)
    :name: _dbs
    :hidden:

    deploy_mssql_era/deploy_mssql_era
    admin_mssqldb/admin_mssqldb
    patch_sql/patch_sql

.. toctree::
   :maxdepth: 2
   :caption: Oracle with Nutanix Era (Option B)
   :name: _dbs
   :hidden:

   deploy_oracle_era/deploy_oracle_era
   admin_oracle/admin_oracle
   patching_oracle/patching_oracle

.. toctree::
   :maxdepth: 2
   :caption: Nutanix Era FAQ
   :name: _dbs
   :hidden:

   faq/faq

.. title: Welcome to Nutanix Era database workshop

|

   .. figure:: images/databasebanner.png

|

.. note:: 

   Below is a short introduction to our workshop and on the left is the navigation panel to navigate the labs. Select either MSSQL track (Option A) or Oracle track (Option B). If time permits, do both!

   Each track will take approx. 2 hrs to complete from start to finish.

   Here are a list of pre-requisites you will need to attain to participate in these labs:
        - Internet access
        - A laptop (running a recent version of MS Windows or GNU/Linux) without any form of lockdown that prevents VPN client installation or accessing the environment via a Nutanix hosted virtual desktop
        - Web browser installed on MS Windows or Linux client
        - Remote access software installed (PuTTY & PuTTYgen) on MS Windows client or (SSH client and ssh-keygen packages) installed on Linux client
        - Ideally, your DBA bragging rights worn on your sleeves!

Welcome to the our Nutanix Era Database as a Service (DBaaS) workshop. This workshop is meant to provide you with first hand experience in why Nutanix is an ideal platform for database workloads.

Historically, it has been a challenge to virtualize database servers because of the high cost of traditional virtualization stacks and the impact that a SAN-based architecture can have on performance. Businesses and their IT departments have constantly fought to balance cost, operational simplicity, and consistent predictable performance.

The Nutanix Enterprise Cloud removes many of these challenges and makes virtualizing a business-critical application such as an Oracle or MSSQL server much easier. The Acropolis Distributed Storage Fabric (ADSF) is a software-defined solution that provides all the features one typically expects in an enterprise SAN, without a SAN’s physical limitations and bottlenecks. Database servers particularly benefits from the following DSF features:

 - Localized I/O and the use of flash for index and key database files to lower operation latency.
 - A highly distributed approach that can handle both random and sequential workloads.
 - The ability to add new nodes and scale the infrastructure without system downtime or performance impact.
 - Nutanix data protection and disaster recovery workflows that simplify backup operations and business continuity processes.
 - In addition to solving common infrastructure problems for hosting business critical applications, Nutanix also seeks to address many of the key pain points associated with managing databases.

|

   .. figure:: images/dbissue1.png

|

Maintaining the status quo leads to inefficient usage of both storage and administrator time. The issues shown above all exist and are only further compounded with time and complexity.

**Meet Nutanix Era!**

|

   .. figure:: images/dbissue2.png

|

Nutanix Era provides DBaaS for your Enterprise Cloud. Leveraging the Nutanix Enterprise Cloud OS, we are able to take advantage of the power of full stack - data, compute, and software. Nutanix Era hides the complexity of database operations and provides common APIs, CLI, and consumer-grade GUI experience for multiple database engines. It makes database operations such as cloning efficient, thereby driving down the TCO of database management for our customers.

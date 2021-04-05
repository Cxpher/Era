.. Era documentation master file, created by
   sphinx-quickstart on Sun Apr  4 12:45:29 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to Era's documentation!
===============================

.. toctree::
    :maxdepth: 2
    :caption: Era with MSSQL Track
    :name: _dbs
    :hidden:

    deploy_mssql_era/deploy_mssql_era
    admin_mssqldb/admin_mssqldb
    patch_sql/patch_sql

.. toctree::
   :maxdepth: 2
   :caption: Era with Oracle Track
   :name: _dbs
   :hidden:

   deploy_oracle_era/deploy_oracle_era
   admin_oracle/admin_oracle
   patching_oracle/patching_oracle

|
   .. figure:: images/databasebanner.png
|
.. title: Welcome to Nutanix Era database workshop

Welcome to the Databases bootcamp. This bootcamp is meant to provide you with first hand experience in why Nutanix is an ideal platform for Database workloads.

Historically, it has been a challenge to virtualize SQL Server because of the high cost of traditional virtualization stacks and the impact that a SAN-based architecture can have on performance. Businesses and their IT departments have constantly fought to balance cost, operational simplicity, and consistent predictable performance.

The Nutanix Enterprise Cloud removes many of these challenges and makes virtualizing a business-critical application such as SQL Server much easier. The Acropolis Distributed Storage Fabric (DSF) is a software-defined solution that provides all the features one typically expects in an enterprise SAN, without a SAN’s physical limitations and bottlenecks. SQL Server particularly benefits from the following DSF features:

 - Localized I/O and the use of flash for index and key database files to lower operation latency.
 - A highly distributed approach that can handle both random and sequential workloads.
 - The ability to add new nodes and scale the infrastructure without system downtime or performance impact.
 - Nutanix data protection and disaster recovery workflows that simplify backup operations and business continuity processes.
 - In addition to solving common infrastructure problems for hosting business critical applications, Nutanix also seeks to address many of the key pain points associated with managing databases.


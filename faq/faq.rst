.. _deploy_oracle_era:

-------------------------
Frequenty Asked Questions aka FAQ about Nutanix Era
-------------------------

.. note::

   This FAQ aims to address commonly asked questions. If you have questions about Nutanix Era beyond the scope of this FAQ, please reach out to your friendly Nutanix SE.

|

#. What database engines are supported by Nutanix Era?

   Nutanix Era supports the following databases:
   - MariaDB/MySQL (Single)
   - PostgreSQL (Single & Clustered - Percona)
   - MSSQL (Single & AlwaysOn)
   - Oracle on Linux (SID, SIHA & RAC)
   - SAP HANA (Single)

#. Are there plans to support other types of databases in future (eg. like NoSQL)?

   We have plans to support MongoDB in the near future.

#. Does my database have to run on Nutanix to use Nutanix Era?

   Yes. Nutanix Era uses much of the goodness of the Nutanix Acropolis Operating System (AOS) and the Acropolis Distributed Storage Fabric (ADSF) for it's magic so it's very much needed

#. Can i save on storage space for my clones with Nutanix Era?

   Yes. Every clone you take will initially be a 0 byte clone thanks to our redirect-on-write snapshot technology. Nutanix Era brings database awareness to that technology. Only delta from the initial snapshots will consume storage space.

#. Can i provision databases from a Nutanix Era platform to another Nutanix Cluster in my environment?

   Assuming that the network is routable, you can. Nutanix Era has multi cluster support. You can even provision MSSQL AAG and Oracle RAC nodes across different clusters, all managed by Nutanix Era.

#. Does Nutanix Era support non x86 platforms like AIX and SPARC?

   No. Oracle databases running on those platforms are not supported. You can however, migrate databases on these platforms, broadly speaking, to Linux on x86 and then you can use Nutanix Era with them.

#. Does Nutanix support MSSQL databases running on Linux or Oracle databases running on Windows?

   Not at the moment.

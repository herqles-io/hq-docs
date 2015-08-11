Requirements
============

RabbitMQ 3.5.x
--------------

One RabbitMQ Cluster per datacenter with at least 3 nodes. The recommended cluster setup and installation guide from
RabbitMQ should be referenced for optimal setup. Federation or Shovel plugins should not be used and RabbitMQ clusters
in different datacenters should not communicate.

RabbitMQ version 3.5.x is required due to breaking changes in the 3.5 release. As new RabbitMQ versions are released
Herqles will be tested and validated against them.

PostgreSQL or MySQL
-------------------

Please reference the Master/Slave setup guides for the chosen SQL server. Herqles must always communicate with the Master
SQL server due to replication latency issues.

Herqles has been developed and tested against PostgreSQL 9.4.x and MariaDB 5.5.x but should work with most new versions.

Python 2.7
----------

Herqles is limited to Python 2.7.x due to library constraints. Once all libraries are updated for Python 3 Herqles will
be updated and validated for Python 3. Running Herqles under Python 3 may have unintended results therefore it is not recommended.

LDAP
----

Herqles has been tested against Active Directory on Windows Server 2012. Other LDAP implementations have not been tested.
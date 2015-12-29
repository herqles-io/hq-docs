Quick Start Guide
=================

Requirements
------------

* RabbitMQ 3.5.x
* PostgreSQL 9.4.x or MySQL 5.5.x
* Python 2.7

Pre-Installation
----------------

In this guide we will be installing all Herqles modules on the same system. In a production like environment there should be
multiple Framework and Manager modules running across multiple nodes and the Workers should be placed on systems that should
allow them to perform their specific tasks.

We will also not go over how to install RabbitMQ or the SQL server of your choice. The user should be aware of how to setup
these services in development and production like environments.

Installation
------------

1. Create a python virtual environment to install Herqles into

.. code-block:: bash

   mkdir /var/lib/herqles
   virtualenv /var/lib/herqles/venv --python=python2.7

2. Activate the virtual environment and install the Herqles components

.. code-block:: bash

   source /var/lib/herqles/venv/activate
   pip install hq-manager hq-framework hq-worker hq-cli

* Optionally install any Framework and Worker implementations.
* Optionally install any CLI plugins.

3. Create the basic configuration for the Manager, Framework and Worker

.. code-block:: bash

   mkdir -p /etc/herqles/{manager,framework,worker}
   mkdir /etc/herqles/framework/config.d
   mkdir /etc/herqles/worker/config.d
   mkdir /var/log/herqles

:code:`/etc/herqles/manager/config.yml`

.. code-block:: yaml

  ---
  rabbitmq:
    hosts:
      - "rabbit1.example.com:5672"
      - "rabbit2.example.com:5672"
      - "rabbit3.example.com:5672"
    username: herqles
    password: password123
    virtual_host: herqles
  sql:
    driver: postgres
    host: sql.example.com
    port: 5432
    database: herqles
    username: herqles
    password: password456
    pool_size: 20
  identity:
    driver: hqmanager.identity.sql_driver
    admin_username: admin
    admin_password: supersecretpassword
  assignment:
    driver: hqmanager.assignment.sql_driver
    admin_username: admin
  paths:
    logs: /var/log/herqles
    pid: /var/run/hq-manager.pid

:code:`/etc/herqles/framework/config.yml`

.. code-block:: yaml

  ---
  rabbitmq:
    hosts:
      - "rabbit1.example.com:5672"
      - "rabbit2.example.com:5672"
      - "rabbit3.example.com:5672"
    username: herqles
    password: password123
    virtual_host: herqles
  sql:
    driver: postgres
    host: sql.example.com
    port: 5432
    database: herqles
    username: herqles
    password: password456
    pool_size: 20
  paths:
    logs: /var/log/herqles
    pid: /var/hq-framework.pid
    framework_configs: /etc/herqles/framework/config.d

:code:`/etc/herqles/worker/config.yml`

.. code-block:: yaml

  ---
  rabbitmq:
    hosts:
      - "rabbit1.example.com:5672"
      - "rabbit2.example.com:5672"
      - "rabbit3.example.com:5672"
    username: herqles
    password: password123
    virtual_host: herqles
  paths:
    logs: /var/log/herqles
    pid: /var/run/hq-worker.pid
    worker_configs: /etc/herqles/worker/config.d

* Optionally configure any Framework and Worker implementations.

4. Run the Manager

.. code-block:: bash

   hq-manager -c /etc/herqles/manager/config.yml

5. Run the Framework

.. code-block:: bash

   hq-framework -c /etc/herqles/framework/config.yml

* Framework will exit if there are no framework implementations installed.

6. Run the Worker

.. code-block:: bash

   hq-worker -c /etc/herqles/worker/config.yml

* Worker will exit if there are no worker implementations installed.

7. Configure the CLI

.. code-block:: bash

   mkdir -p ~/.herq/plugins

:code:`~/.herq/config.yml`

.. code-block:: yaml

   manager_url: 'http://127.0.0.1:8080'
   framework_url: 'http://127.0.0.1:8081'

* The manager and framework will only listen on localhost and will need a reverse-proxy to allow outside requests.
* Optionally configure any CLI plugins

8. Run the CLI


.. code-block:: bash

   herq --help

The CLI will use your current systems username to interact with the APIs if you need to change this user please see
the CLI documentation.


.. Herqles documentation master file, created by
   sphinx-quickstart on Fri Aug  7 13:43:28 2015.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Introduction to Herqles
=======================

Herqles is a multi-datacenter distributed task system. The goal of this system is to easily allow groups of tasks
to run across multiple hosts in many datacenters. Some use cases for this system are automated application deployment,
puppet manifest and hiera data deployments, and docker container clustering. The core of Herqles is based off of Mesos
but more focused on task management instead of utilized resources.

Herqles is split up into 3 modules (Manager, Framework, and Worker) and uses a master-less system to group and execute tasks.

.. toctree::
   :caption: Table of Contents
   :maxdepth: 2

   quickstart
   system/index
   manager/index
   framework
   worker

.. toctree::
   :caption: Supported Frameworks
   :maxdepth: 2


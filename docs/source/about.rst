About Vision
============

The Vision supercomputer is made by 2 compute nodes and a management node. Each compute node is a NVIDIA DGX A100 systems with the following specifications:

 - CPU: Dual AMD Rome 7742, 128 cores total
 - System Memory: 1TB
 - GPUs: 8x NVIDIA A100 Tensor Core GPUs (40GB per GPU)
 - GPU Memory: 320GB total

The two DGX A100 systems are interconneted by 8 x 200Gb/s HDR InfiniBand links.

Storage
-------

The users have access to two main storage areas in Vision:

 - Home folder
 - External storage

Home folder
^^^^^^^^^^^

The home folder is located in ``/home/<username>`` and is shared between all nodes of the cluster (management node and compute nodes).

This folder should be used to store personal files and source code for the applications of the user.

External storage
^^^^^^^^^^^^^^^^

The Vision supercomputer has an external storage for data with the capacity of 15TB. This storage is made avaialbe in the management node and in the compute nodes via an NFS share mounted in ``/data``. Each user has a folder in ``/data/<username>`` and/or ``/data/<project>/<username>``. The data stored in ``/data`` is shared between all nodes.

This folder should be used to store data that will be processed by your applications. The data created by your applications should also be stored in this storage area.

.. warning::

  This storage uses a RAID 0 volume to increase read performance while feeding data to the GPUs, wihtout any redundancy. If any of the drives fail, all data in the external storage will be lost. There are no backups of this volume.

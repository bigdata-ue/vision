.. _software:

Software
========

Vision has available Python Environments and Anaconda, allowing users to create their own execution envirnment according to the needs of each application. Vision also has available software modules, that users can load to meet the dependencies of their applications.

Python Environments
-------------------

To create a Pytohn Environment, the user can run the following command:

.. code-block:: console

  $ python3 -m venv ./venv

After creating the environment, the user can run the following command to activate the envirnment and install new packages:

.. code-block:: console

  $ source ./venv/bin/activate
  (venv) $ pip install tensorflow==2.7.0
  (venv) $ pip install matplotlib

Anaconda
--------

Anaconda is available at /opt/conda/. To activate Anaconda, the user should run the following command:

.. code-block:: console

  $ source /opt/conda/etc/profile.d/conda.sh

To create a Conda environment, the use can run the following command:

.. code-block:: console

  (base) $ conda create -n tf-gpu tensorflow-gpu

In this example, we are creating environment named ``tf-gpu`` is created, based on the Conda environment ``tensorflow``. After creating the environment, you can activate it and install new packages:

.. code-block:: console

  (base) $ conda activate tf-gpu
  (tf-gpu) $ pip install tensorflow==2.7.0
  (tf-gpu) $ pip install matplotlib


Software modules
----------------

To list the available software modules, the user should run the following command:

.. code-block:: console

  $ module av

To load a software module, the user should run, for example, the following command:

.. code-block:: console

  $ module load foss/2021a

You can learn more about software modules in :doc:`./software_modules`.

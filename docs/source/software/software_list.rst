.. _software_list:

Available software modules
==========================

In this page you can find the list of the available software modules in Vision and instructions on how to load them.

Loading software modules
------------------------

To load any of the modules found in the following list, you should first run the command ``module spider`` to list the modules that you should before loading the desired module.

For example, to load the Gromacs module, the user should first run:

.. code-block:: console

  $ module spider GROMACS
  ....
      You will need to load all module(s) on any one of the lines below before the "GROMACS/2021.3-CUDA-11.3.1" module is available to load.

        GCC/10.3.0  OpenMPI/4.1.1
  ....

Then, the user can load all the needed software modules:

.. code-block:: console

  $ module load GCC/10.3.0  OpenMPI/4.1.1 GROMACS

List of software modules
------------------------

The following is a list of software modules avaliable in Vision. You can check this list in Vision by running the command ``module spider``:

.. include:: software_list.txt
   :literal:

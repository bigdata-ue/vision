Quick start
===========

In this page you can find a quick start guide on how to use Vision:

1. Access Vision
----------------

First you need to access Vision. To do so, you should use ssh with your credentials:

.. code-block:: console

  $: ssh user@main.vision.uevora.pt
  [user@frontend ~]$

You can find more information on how to access Vision in :ref:`access`.

2. Prepare your software environment
------------------------------------

After logging in to Vision, you should change your working directory to your project directory and prepare the environment to run/build your application. You can use:

  - :ref:`venv`
  - :ref:`conda`
  - :ref:`software_modules`

3. Create your slurm job script
-------------------------------

After setting up your runtime environment, you should create a slurm job script, so that you can submit your job. The following is a Slurm job script to submit a project that uses Conda for dependency management:

.. code-block:: console

  #!/bin/bash
  #SBATCH --job-name=cnn                    # create a short name for your job
  #SBATCH --output="slurm-cnn-conda-%j.out" # %j will be replaced by the slurm jobID
  #SBATCH --nodes=1                         # node count
  #SBATCH --ntasks=1                        # total number of tasks across all nodes
  #SBATCH --cpus-per-task=4                 # cpu-cores per task (>1 if multi-threaded tasks)
  #SBATCH --gres=gpu:2                      # number of gpus per node

  source /opt/conda/bin/activate
  conda activate tf-gpu

  python3 cnn.py

  conda deactivate

The script is made of two parts: 1) specification of the resources needed as well to run the job as some general job information; and 2) specification of the taks that will be run.

In the first part of the script, we define the job name, the output file and the requested resources (4 CPUs and 2 GPUs). Then, in the second part, we define the tasks of the job. When using Conda, we should run the following:

1. Activate the Conda environment;
2. Excecute the code;
3. Deactivate Conda  environment;

You can find more information and examples on how to submit jobs in :ref:`examples`.

4. Submit the job
-----------------

To submit the job, you should run the following command:

.. code-block:: console

  $ sbatch script_conda.sh
  Submitted batch job 144

You can check the job status using the following command:

.. code-block:: console

  $ squeue
                JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
                143       batch      cnn     user  R       0:33      1 vision2

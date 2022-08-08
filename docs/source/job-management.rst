Job management
==============

Jobs in Vision are managed by the Slurm Workload Manager, a job scheduler which schedules jobs according to the available computational resources and the requirements of each job.


How to submit a jobs
--------------------
To submit a job in Slurm you have to first create a job script, which defines the job, the required resources by your job and the tasks that will run in the nodes. In particular, you should:

  #. Access Vision: check :doc:`./access` for details
  #. Copy your code to Vision: use ``scp`` or another tool that transfer files over SSH.
  #. Create a Slurm job script: check `Slurm job scripts`_. and :doc:`./examples` for details.
  #. Submit the job: see bellow.


.. _Slurm job scripts:

Slurm job scripts
-----------------

Slurm job scripts allow users to define the jobs that will run in the cluster. These are ``bash`` scripts which allows specify: 1) general properties of job, such as name an output files; 2) the resources that will be allocated to job; and 3) the code that will be run.

The following example represents a simple Slurm job script:

.. code-block:: console
  :linenos:

  #!/bin/bash
  #SBATCH --job-name=cnn                    # create a short name for your job
  #SBATCH --output="slurm-cnn-venv-%j.out"  # %j will be replaced by the slurm jobID
  #SBATCH --nodes=1                         # node count
  #SBATCH --ntasks=1                        # total number of tasks across all nodes
  #SBATCH --cpus-per-task=4                 # cpu-cores per task (>1 if multi-threaded tasks)
  #SBATCH --gres=gpu:2                      # number of gpus per node

  source venv/bin/activate

  python3 cnn.py

  deactivate

In this script, we start by 1) defining the job name and the output file (lines 3-3); 2) specifying the required resources (4 CPUs and 2 GPUs) (lines 4-7); and 3) defining the code that will run (lines 9-13). For more information about this and other examples, please check :doc:`./examples`.

Accounting
----------

The resources used by a user are allways associated with project and are logged in order to control the cluster usage. To check the resources used in a time interval, the users should use the ``sreport`` command:

.. code-block:: console

  $ sreport cluster AccountUtilizationByUser account=prject start=0101 -T cpu,gres/gpu
  --------------------------------------------------------------------------------
  Cluster/Account/User Utilization 2022-01-01T00:00:00 - 2022-05-10T23:59:59 (11232000 secs)
  Usage reported in TRES Minutes
  --------------------------------------------------------------------------------
    Cluster         Account     Login     Proper Name      TRES Name      Used
  --------- --------------- --------- --------------- -------------- ---------
        hpc       project-x                                      cpu   2863935
        hpc       project-x                                 gres/gpu     88738
        hpc       project-x     user1           user1            cpu        17
        hpc       project-x     user1           user1       gres/gpu        14
        hpc       project-x     user2           user2            cpu   2863917
        hpc       project-x     user2           user2       gres/gpu     88724


In this example, the user is checking the resources consumed in the context of project ``project-x`` since January 1. Usage values are presented in minutes.


Common Slurm commands
---------------------
In this section you can find some common useful commands to submit, manage and monitor jobs. You can find more detailed information on https://slurm.schedmd.com/quickstart.html.

Submit a job
^^^^^^^^^^^^

To submit a job, you should use the ``sbatch`` command:

.. code-block:: console

  $: sbatch my-job-script.sh
  Submitted batch job 439

In this example, the job was submited with the id 439.

Cancel a job
^^^^^^^^^^^^

To cancel a job, the user should use the ``scancel`` command:

.. code-block:: console

  $ scancel 439


In this example, the job was submited with the id 439.

List job queue
^^^^^^^^^^^^^^

To list the job queue, the user use should use the command ``squeue``. This command lists all submited jobs to the cluster, including the job status and the node(s) where they are running:

.. code-block:: console

  $: squeue
               JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
               444     compute theJobNa     user  R      11:01      1 vision2

List job information
^^^^^^^^^^^^^^^^^^^^

To list detailed information about a job, the user should use the ``scontrol`` command. This list the relevant information about the job, including the requested resources, the job script and the output files. The user needs to know the job id:

.. code-block:: console

  $: scontrol show jobid <jobId>
  JobId=444 JobName=The_Job_Name
     UserId=user(1000) GroupId=emedeiros(1000) MCS_label=N/A
     Priority=4294901696 Nice=0 Account=asr-pt QOS=normal
     JobState=RUNNING Reason=None Dependency=(null)
     Requeue=1 Restarts=0 BatchFlag=1 Reboot=0 ExitCode=0:0
     RunTime=00:18:08 TimeLimit=5-00:00:00 TimeMin=N/A
     SubmitTime=2022-05-11T10:32:29 EligibleTime=2022-05-11T10:32:29
     AccrueTime=2022-05-11T10:32:29
     StartTime=2022-05-11T10:32:30 EndTime=2022-05-16T10:32:30 Deadline=N/A
     SuspendTime=None SecsPreSuspend=0 LastSchedEval=2022-05-11T10:32:30
     Partition=compute AllocNode:Sid=vision1:3110592
     ReqNodeList=vision2 ExcNodeList=(null)
     NodeList=vision2
     BatchHost=vision2
     NumNodes=1 NumCPUs=255 NumTasks=1 CPUs/Task=255 ReqB:S:C:T=0:0:*:*
     TRES=cpu=255,mem=980288M,node=1,billing=255,gres/gpu=8
     Socks/Node=* NtasksPerN:B:S:C=0:0:*:* CoreSpec=*
     MinCPUsNode=255 MinMemoryNode=980288M MinTmpDiskNode=0
     Features=(null) DelayBoot=00:00:00
     OverSubscribe=OK Contiguous=0 Licenses=(null) Network=(null)
     Command=/path/to/my-job-script.sh
     WorkDir=/path/of/my-job
     StdErr=/path/to/my-job-script.out
     StdIn=/dev/null
     StdOut=/path/to/my-job-script.out
     Power=
     TresPerNode=gpu:8
     NtasksPerTRES:0


Check node status
^^^^^^^^^^^^^^^^^

To check the status of eacch node of the cluster, users should use the ``sinfo`` command:

 .. code-block:: console

    $ sinfo
    PARTITION AVAIL  TIMELIMIT  NODES  STATE NODELIST
    compute*     up   infinite      1    mix vision1
    compute*     up   infinite      1  alloc vision2
    debug        up      15:00      1    mix vision1
    debug        up      15:00      1  alloc vision2

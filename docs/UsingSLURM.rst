Using Slurm
===========

.. _slurm:

Slurm is a free and open-source job scheduler for
Linux and Unix-like kernels, used by many of the
world's supercomputers and computer clusters.

Slurm is used @ CINECA, CERN, RIKEN, LIVERMORE,
OAK RIDGE, etc.

Installed Slurm version: 19.05.2 (Aug 13, 2019)

Slurm Partitions
----------------

.. _slurmpartitions:

A Slurm partition is a group of resources. Each
partition can be considered as a job queue, each of
which has some constraint (e.g. number of running
jobs, job time limit, etc.).

CAPRI has 2 partitions:

  * **allgroups**: partition to run both serial and parallel
    software. This partition should be used to run not
    interactive software;
  * **interactive**: partition to run software in an
    interactive way. This partition has limited resources
    (default: 1 cores, 1GB RAM). Interactive sessions
    should be shorter than 24 hours.

Which partition should I use?

The great majority of CAPRI users should use the
allgroups partition. Typical serial and parallel software
that require no interaction with the user should be run
in this partition.

The interactive partition should be used only when a
real time interaction is needed and/or for tasks having
low computation burden. Typical examples are the
installation of software having an interactive installation
procedure, simple file managing/manipulation (e.g.
compressing files), etc.

Slurm Jobs
----------

.. _slurmjobs:

To run a software on CAPRI, the user the user must
prepare a so-called (Slurm) *job file*. A job file is a text file containing
some Slurm instructions/options and the call to user software.

The typical job file is something like this: 

::

   #!/bin/bash
   
   #SBATCH --ntasks 4
   #SBATCH --partition allgroups
   #SBATCH --time 02:00
   #SBATCH --mem 1G
   
   cd $SLURM_SUBMIT_DIR
   
   srun <your_software>
   
Dissection of the job file
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _jobdissection:

``#!/bin/bash``

This is simply the interpreter of subsequent commands (bash in this case).

``#SBATCH ...``

Following the ``#SBATCH`` directive are special options geared at the SLURM
scheduler. We will see some of them in detail below.

``cd $SLURM_SUBMIT_DIR``

This is a useful command to ask the scheduler to change the current directory
before launching the program. This way all the paths can be considered as
relative to the directory the job file resides in.

``srun <your_software>``

This is where you ask the scheduler to run your program for you.

Slurm mandatory options
^^^^^^^^^^^^^^^^^^^^^^^

.. _mandatoryopts:

Slurm (actually *srun*) recognizes a large number of options to suit your needs.
Some options can be specified using either the short (prefixed with just one dash 
and a letter) or the long (two dashes) form. 

There are four **mandatory** options you must specify on your job to successfully run
on the CAPRI platform. These are:

 -n, -\\-ntasks <num_tasks>
  Number of tasks to launch. For serial code <num_task> should be set to 1, for
  parallel code <num_task> should be set to the
  number of parallel execution flows.

 -p, -\\-partition <partition_name>
  Slurm partition. For typical serial or parallel job <partition_name> is *allgroups*

 -t, -\\-time <time>
  Maximum job execution time, where time could be specified as one of

  * mm
  * mm:ss
  * hh:mm:ss
  * dd-hh
  * dd-hh:mm
  * dd-hh:mm:ss


 -\\-mem <size[units]>
  Maximum amount of RAM memory requested. Different units can be specified using the suffix [K|M|G|T]

A more complete job
^^^^^^^^^^^^^^^^^^^

.. _slurmjobfull:

::

  #!/bin/bash

  #SBATCH --jobname <job_name>
  #SBATCH --output output_%j.txt
  #SBATCH --error errors_%j.txt
  #SBATCH --mail-user james@gmail.com
  #SBATCH --mail-type ALL
  #SBATCH 
  #SBATCH --time 02:00
  #SBATCH --ntask 4
  #SBATCH --partition allgroups
  #SBATCH --mem 1G

  cd $SLURM_SUBMIT_DIR

  srun <your_software>


-\\-jobname <job_name>
  When you queue your job this option can provide a visual clue to distinguish between your jobs.

-\\-output output_%j.txt
  Your output file will be numbered with your JOBID (%j). Subsequent runs will not overwrite the output file.

-\\-error errors_%j.txt
  Same as above for standard error.

-\\-mail-user james@gmail.com
  Depending on what you specify on the companion directive ``mail-type`` the specified user will be
  notified via email.

-\\-mail-type ALL 
  Notify user by email when certain event types occur. See the *srun* manual page on the frontend node
  (issuing a ``man srun`` at the command prompt) for a complete list.


SLURM Interaction
-----------------

.. _slurminteract:

Submit a job
^^^^^^^^^^^^

.. _jobsubmit:

Once you wrote your job file you can *submit* it to the scheduler
to get it executed using the sbatch command:

::

 sbatch [options] <job_file>

e.g.: ``sbatch test.slurm``. Upon (successful) job submission, you will get a message like this:

::

 Submitted job 129774

Here 129744 is the JOBID. This number can be used to check for the job progress, to remove it from
the execution queue or for other operations. You can read the sbatch documentation using ``man sbatch``
from the frontend node or visiting the relative `web page <https://slurm.schedmd.com/sbatch.html>`_

Options specified inside the job file (after the ``#SBATCH`` directives) can be overridden or
modified on the command line, e.g.:

::

 sbatch --mem 10G --jobname test10G test.slurm

The above command line will set - just for this submission - the jobname to 'test10G' and will
request ten gigabytes of RAM, possibly overriding what specified inside the slurm job file.


Checking job status
^^^^^^^^^^^^^^^^^^^

Once the job enters the queue you can use the *squeue* command to check its status::

 squeue [-l]

The above command will list *all* the jobs in the queue. Since the list can be very long
you can filter only your jobs::

 squeue [-l] -u <user_id>

or you can check a single job providing the JOBID

::

 squeue -j JOBID

To see the complete list of output options and command flags use ``man squeue``
from the frontend node or visit the relative `web page <https://slurm.schedmd.com/squeue.html>`_

Checking running jobs
^^^^^^^^^^^^^^^^^^^^^

The status of jobs in a **running** state can be checked with::

 sstat

To see the complete list of output statistics (e.g. min/max/avg bytes read/written, min/max/avg CPU time, min/max/avg
memory usage, etc.)  and command options use ``man sstat`` from the frontend node or 
visit the relative `web page <https://slurm.schedmd.com/sstat.html>`_

Remove a job
^^^^^^^^^^^^

To remove a job from the queue use::

 scancel JOBID

Alternatively if you want to remove **all your jobs** from the queue you can use

::
 
 scancel -u <user_id>

.. caution:: there are no confirmation prompts.



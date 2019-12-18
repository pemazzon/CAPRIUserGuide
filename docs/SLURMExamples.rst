SLURM Job Examples
==================

.. _jobexamples:

MPI job
-------

.. _mpijob:

::

  #!/bin/bash
  #SBATCH -J hellompi
  #SBATCH -o output_%j.txt
  #SBATCH -e errors_%j.txt
  #SBATCH -t 01:30:00
  # request 32 MPI tasks
  #SBATCH -n 32
  #SBATCH -p allgroups
  #SBATCH --mem 640G
  
  cd $SLURM_SUBMIT_DIR
  spack load intel-parallel-studio@professional.2019.4
  
  srun ./mphello

.. note::
   ``spack load ...`` initializes the Intel MPI environment and
   is equivalent to ``module load intel-parallel-studio-professional.2019.4-gcc-8.2.1-fnvratt``

openMP job
----------

.. _openmpjob


  * GPU job
  * Singularity job
  * Interactive job


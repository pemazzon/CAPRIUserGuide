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

OpenMP job
----------

.. _openmpjob:

::

  #!/bin/bash
  #SBATCH -J helloopenmp
  #SBATCH -o output_%j.txt
  #SBATCH -e errors_%j.txt
  #SBATCH -t 01:30:00
  #SBATCH -n 1
  # notice we're using the '-c' option
  # to request for OMP threads
  #SBATCH -c 32
  #SBATCH -p allgroups
  #SBATCH –mem 640G
  
  cd $SLURM_SUBMIT_DIR
  # set this to what you asked with '-c'
  export OMP_NUM_THREADS=32
  
  srun ./omphello

.. note::
   * ``OMP_NUM_THREADS`` must be set to the same number as the ``-c`` parameter
   * set ``-n`` to 1 if the program uses OpenMP only. If using both MPI and
     OpenMP set ``-n`` to the number of MPI tasks. The total number of slots
     requested, in any case, will be ``n*c``

  
* GPU job
* Singularity job
* Interactive job


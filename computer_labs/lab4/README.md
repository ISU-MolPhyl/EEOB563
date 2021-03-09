# Lab #4: Maximum Likelihood
## Likelihood analysis using RAxML
<img src="./fisher.jpg" align="right" hspace="10">
Several programs implement the maximum likelihood method for molecular sequences,
including programs like MolPHY, PAUP and PHYLIP, which are accurate, but usually
limited to single gene datasets from up to a few dozens of taxa, and newer
programs including
[FastTree](http://meta.microbesonline.org/fasttree/),
[IQ-Tree](http://www.iqtree.org/),
[PhyML](http://www.atgc-montpellier.fr/phyml/), and
[RAxML](https://sco.h-its.org/exelixis/software.html), which are much faster but
use different heuristics and approximations. We will use
[RAxML-NG](https://github.com/amkozlov/raxml-ng) for this lab, a "faster,
easier-to-use and more flexible" version of the popular RAxML program.

An important additional goal of this lab is to lean how to interact properly
with the HPC-class cluster both in an interactive mode and using the Slurm
Workload manager.

## Using HPC-class in an interactive mode
When we log in to [HPC-class](https://www.hpc.iastate.edu/guides/classroom-hpc-cluster),
we interact with the head module. This is ok if we use simple UNIX commands, but
would slow down the system dramatically (and bring down the wrath of other users),
if we perform long computational tasks. Instead, we'll use the `salloc` command
to request access to compute nodes on the cluster. For this exercise use the
`salloc -N 1 -n 8 -t 2:00:00` command to request 8 cores on 1 node for 2 hours.

## Preliminaries
1. `raxml-ng` is already installed in the shared class directory (how do you check
  the location of a program?);
2. I also installed the `nw-display` tool that allows you to view phylogenetic
  trees on HPC-class;
3. The data for this lab is in the course repository. Make sure to update it with
 `git pull`

## RAxML-NG tutorial
Complete RAxML-NG [tutorial](./raxml-ng.md) by answering the questions in the
"Now it's your turn" section.

## Using Slurm Workload manager
So far, we used the Slurm Workload Manager in an interactive mode. However, for
longer jobs, the batch mode is preferred.  In this case a job script should be
created and submitted into queue by issuing: `sbatch <job_script>`.

#### Slurm Job Script Generator
The easiest way to create an Slurm job script is to use the
[Slurm job script generator](https://www.hpc.iastate.edu/guides/classroom-hpc-cluster/slurm-job-script-generator).
Choose the number of compute nodes, number of processor cores per node, maximum
time the job may run. **Read instructions in red while choosing these numbers**.
After your are done with the settings, copy the job script from the gray area
and paste it in a local file.  Add commands for loading modules and running the
programs at the bottom of the script.

#### Submitting your job
To submit the PBS script in the file myjob use the `sbatch <job_script>` command.  
You may submit several jobs in succession if they use different output files.
Jobs will be scheduled for queues* based on the resources requested. There are
limits on each queue regarding the maximum number of simultaneous jobs and
maximum number of processors that may be used by one user or class.

*In Slurm queues are called partitions. Only partitions for
[accelerator nodes](https://www.hpc.iastate.edu/guides/classroom-hpc-cluster/accelerator-nodes) need to be specified when submitting jobs. Otherwise Slurm will submit job into a partition
based on the number of nodes and time requested.

* To see the list of available partitions, issue: `sinfo`
* For more details on partitions limits, issue: `scontrol show partitions`
* To see the job queue, issue: `squeue`
* To cancel job \<job_id\>, issue: `scancel <job_id>`

# Kharma in Delta for Dummies.
## Some Quick Information

Using Kharma, or my own [Kharma_Blandford](https://github.com/MichaelC3/kharma_Blandford), within Delta is fairly easy. An important piece of note, however, is that most of the things you will do in Delta will occur within a Slurm job, this is unlike BH28, but is farily standard across large user base machines. 

For our use, we will use two Slurm commands for getting into a job. They are `srun` and `sbatch`. The first, is responsible for requesting the run. It takes a variety of options and flags such as number of nodes, number of GPUs per nodes, etc (For more information use the SLURM documentation page found [here](https://slurm.schedmd.com/srun.html)). The second command submits bash scripts to Slurm. This allows us to use scripts like `delta.sb`, contained here, enabling us to run our jobs in the background. 

An example use of `srun` would look like this: `srun --account=bbgv-delta-cpu --partition=cpu --nodes=1 --tasks=1 --tasks-per-node=1 --cpus-per-task=8 --mem=16g --time=24:00:00 --pty bas`

In this command, we specify the account that we are using, the partition, how many nodes, tasks, tasks per node, etc. you get the idea. Most of these are pretty self explanatory, but, again, are fully described in the Slurm documentation page. Using something like `sbatch` would instead look like this: `sbatch ./randomscript.sb`. 

This looks much simpler, but much of the work is being done within the `randomscript.sb` file. Using `delta.sb` as an example, you might notice that there is an `srun` command being used under the hood. For some context, `.sb` scripts can be thought of as shell scripts, they function exactly the same, however, here we issue commands using `#SBATCH`. Again, using `delta.sb` as an example, the script is using these `#SBATCH` commands to clarify the parameters of the job we want to make e.g. `#SBATCH -t 24:00:00` or `#SBATCH --account=bbgv-delta-gpu`. 

It is important to note that if you do anything requires a lot of computational power, i.e. running Kharma, outside of a Slrum job you are eligble to being BANNED. Please do not do this! If you are unsure if whatever you are doing requires that you enter a job, just ask!

I will now go into the specifics of building and running Kharma in Delta as well as how to use some useful scripts and how plotting.

## Building Kharma

### Compiling

Kharma is able to be compiled for both CPUs and GPUs, for our use we will be compiling using GPUs. To begin, we need to first clone the kharma-next branch of the repository and then accomplish any of the prerequisites as described in the Kharma github page. Before actually compiling Kharma, we need to load some modules within Delta. We can use the `module.sh` script contained here. From here we can run the command `./make.sh clean cuda hdf5`

### Running Kharma

Once compiled we can begin running simulations. To do that we must make use of a batch job. For a simulation using the parameter file `parfile.par` this will look like `sbatch ./delta.sb -i ./parfile.par`. It should be noted that you should output dumps, and also future plots, within the directory `/scratch/bbgv/<username>` and not within the login node of your account. Once the job is requested, you are free to leave, exit, get coffee or whatever you want to do, it will run in the background. Should you want to check on the run, you can use the command `squeue -u <yourusername>` to see how long the job has been running or if it is done. For more precise information, e.g. to what time the simulation has so far been run to, the `delta.sb` script also outputs an output file with the name `slurm-<jobid>.out` to the dump directory, this information can be found within it.

If you ever need to cancel a job you can use `scancel <jobid>`.

# Usage of SLURM

### Concepte
> The Slurm Workload Manager, formerly known as Simple Linux Utility for Resource Management, or simply Slurm, is a free and open-source job scheduler for Linux and Unix-like kernels, used by many of the world's supercomputers and computer clusters. --Wikipedia

Suppose that an institue has already a cluster. They deploy SLURM to manage different user's jobs.
This note reveals very basic usage of shell script based on SLURM.

### Usage
🔸detailed version:

`#!/bin/bash` tell computer to use which shell    
`#SBATCH --partition=partition1; partition2; partition3...` select partitions based on available partitions  
`#SBATCH --cpus-per-task=1` the number of cpu each task   
`#SBATCH --ntasks=1` specify the number of tasks to run   
`#SBATCH --job-name=anyname` the job name    
`#SBATCH --array=1-4` specify job array, e.g. from 1 to 4, 4 jobs  
`#SBATCH --out=absolute path/sim_result.txt` output results  
`#SBATCH --out=absolute path/sim_result_%a.txt` output different jobs' results

🔸simple version:    
`#!/bin/bash`   
`#SBATCH -p partition1; partition2; partition3...`    
`#SBATCH -c 1`    
`#SBATCH -n 1`     
`#SBATCH -j anyname`    
`#SBATCH -a 1-4`     
`#SBATCH -o absolute path/sim_result.txt`    
`#SBATCH -o absolute path/sim_result_%a.txt`    

Workflow of prepareing a shell script based on SLURM:

![slurm flowchart](https://github.com/jizhang02/Figure-Factory/blob/b1b6ccb6fb9fd26525a84803763934d77a264d92/Fig_CS/Figure-Factory-Page-3.drawio.png)
* case 1: submit a single job

🐚 in shell (pytest.sh):

```
#!/bin/bash
#SBATCH --partition=partition1; partition2; partition3
#SBATCH --cpus-per-task=1
#SBATCH --ntasks=1
#SBATCH --job-name=myjob
#SBATCH --out=result.txt

cd  /path of python code

singularity exec /absolute path of .sif file/container.sif bash -c "source $HOME/set_environment.sh && python test.py"

echo "   "
echo "Finished."
exit
```
👉 in command line `sbatch pytest.sh`

* case 2: submit mutiple jobs

📜 in python code (test.py):

```
import sys

...

# each job correponding to a specific data with passed arguement from shell
filename = 'data_'+str(sys.argv[1])+'.suffix'

print(f"{filename} is being processed...")

dataload(/path/filename)

...

```

🐚 in shell (pytestmulti.sh):

```
#!/bin/bash
#SBATCH -p partition1; partition2; partition3
#SBATCH -c 1
#SBATCH -n 1
#SBATCH -j myjob
#SBATCH -a 1-4
#SBATCH -o /path/result_%a.txt

cd  /path of python code

echo "My SLURM_ARRAY_TASK_ID: " $SLURM_ARRAY_TASK_ID

singularity run /absolute path/container.sif bash -c "source $HOME/set_environment.sh&& python test.py $SLURM_ARRAY_TASK_ID"

echo "   "
echo "Finished."
exit
```
👉 in command line `sbatch pytestmulti.sh`

### Reference
* [sbatch in SLURM](https://slurm.schedmd.com/sbatch.html)

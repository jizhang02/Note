# Usage of SLURM

### Concepte
> The Slurm Workload Manager, formerly known as Simple Linux Utility for Resource Management, or simply Slurm, is a free and open-source job scheduler for Linux and Unix-like kernels, used by many of the world's supercomputers and computer clusters. --Wikipedia

Suppose that an institue has already a cluster. They deploy SLURM to manage different user's jobs.
This note reveals very basic usage of shell script based on SLURM.

### Usage
🔸detailed version:

`#!/bin/bash` tell computer to use which shell    
`#SBATCH --partition=partition1,partition2,partition3...` select partitions based on available partitions, comma, no space  
`#SBATCH --gres=gpu:2` specify the gpu if has and the number of gpu    
`#SBATCH --cpus-per-task=1` the number of cpu each task   
`#SBATCH --ntasks=1` specify the number of tasks to run   
`#SBATCH --job-name=anyname` the job name    
`#SBATCH --array=1-4` specify job array, e.g. from 1 to 4, 4 jobs  
`#SBATCH --out=absolute path/sim_result.txt` output results  
`#SBATCH --out=absolute path/sim_result_%a.txt` output different jobs' results    
`#SBATCH --error=error_%j.txt`    output error results      
`#SBATCH --nodelist cn447` specify node    
`mkdir $SLURM_SUBMIT_DIR/$SLURM_JOB_ID`  move output data to target directory    
`cp -r /home/jzhang/python_code/DeepRT/ $SLURM_SUBMIT_DIR/$SLURM_JOB_ID`

🔸simple version:    

`#!/bin/bash`   
`#SBATCH -p partition1,partition2,partition3...`    
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
#SBATCH --partition=partition1,partition2,partition3
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
#SBATCH -p partition1,partition2,partition3
#SBATCH -c 1
#SBATCH -n 1
#SBATCH -j myjob
#SBATCH -a 1-4
#SBATCH -o /path/result_%a.txt

cd  /path of python code

echo "My SLURM_ARRAY_TASK_ID: " $SLURM_ARRAY_TASK_ID
start=$(date +%s)

singularity run /absolute path/container.sif bash -c "source $HOME/set_environment.sh&& python test.py $SLURM_ARRAY_TASK_ID"

end=$(date +%s)
secs=$((end - start))
printf 'This program takes %dd:%dh:%dm:%ds\n' $((secs/86400)) $((secs%86400/3600)) $((secs%3600/60)) \ $((secs%60))
echo "   "
echo "Finished."
exit
```
👉 in command line `sbatch pytestmulti.sh`

### Common commands on cluster
* `sinfo` see the cluster information
* `squeue -l` see the jobs
* `squeue --start` see the waiting jobs
* `scontrol show partition name` or `scontrol show node name` or `scontrol show job name` see specific part
* `scancel jobid` cancel a job
* `scancel -u username` cancel all jobs with a user
* `scancel -u username -p partition` cancel jobs witha a user under certain partition
* `sacct -j ID-number` the state of a job,  four states: Pending; Running; Completed;Failed
* `htop` see CPU info    
* `nvidia-smi` see GPU info    

#### An entire example
```
#!/bin/bash 

#SBATCH --partition=a6000,titanGPU
#SBATCH --gres=gpu
#SBATCH --cpus-per-task=6
#SBATCH --ntasks 1
##SBATCH --mem-per-cpu=1500MB
#SBATCH -J LUDL
#SBATCH --out=/home2/jzhang/python_code/log/%J-result.txt
#SBATCH --error=/home2/jzhang/python_code/log/%J-error.txt


# Move files to target directory
mkdir $SLURM_SUBMIT_DIR/$SLURM_JOB_ID
cp -r /home2/jzhang/python_code/DeepRT/04pretherapy/torch/ $SLURM_SUBMIT_DIR/$SLURM_JOB_ID
# Run
cd $SLURM_SUBMIT_DIR/$SLURM_JOB_ID
echo Working directory : $PWD
echo "Start running..."
start=$(date +%s)
srun singularity exec --nv /home2/jzhang/image_torch.sif python3 $PWD/torch/main.py
end=$(date +%s)
secs=$((end - start))
printf 'This program takes %dd:%dh:%dm:%ds\n' $((secs/86400)) $((secs%86400/3600)) $((secs%3600/60)) \ $((secs%60))
echo " "
echo `date "+%Y-%m-%d %H:%M:%S"`  
# Move results to target directory
cp -r /home2/jzhang/python_code/DeepRT/04pretherapy/torch/ $SLURM_SUBMIT_DIR/$SLURM_JOB_ID
# Delete results
rm -r /home2/jzhang/python_code/DeepRT/04pretherapy/torch/localruns/*
rm -r /home2/jzhang/python_code/DeepRT/04pretherapy/torch/predict/*
rm -r /home2/jzhang/python_code/DeepRT/04pretherapy/torch/model/*

exit
```
### Reference
* [sbatch in SLURM](https://slurm.schedmd.com/sbatch.html)

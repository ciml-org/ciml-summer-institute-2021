# Configuring Your Training Account

Each member of the class, and instructors have a training account with a default user environment customized with the right paths and software paths, including the conda/mininconda software.

## NOTES/UPDATES:

### [1] Do not replace the ```.bashrc``` with your own. 

Aliases and paths are pre-installed (see below) and if you replace the files you will not be able to run the example software.

### [2] Miniconda installs: 
Institute satff will provide instructions for installing miniconda for the workshop on the preparation day. Please do not re-install conda. If you have trouble, go to the Slack HelpDesk.

<hr>

### Default applications location:
**CHECK THIS**
You have been set up with a default user environment: you do not need have a .bashrc file. You will see the code in this folde *by default*

## Node Reservations:
### GPU reservations
*getcpu:  "srun --pty --nodes=1 --ntasks-per-node=24 -p compute -t 3:00:00 --reservation=si2020resday1 --wait 0 /bin/bash"
*getgpu:  "srun --pty --nodes=1 --ntasks-per-node=6 --gres=gpu:1 --partition gpu-shared -t 3:00:00  --reservation=si2020resday1 --wait 0 /bin/bash"
*getcpu1:  "srun --pty --nodes=1 --ntasks-per-node=24 -p compute -t 1:00:00 --reservation=si2020resday1 --wait 0 /bin/bash"

### CPU reservations
For the class, we have created special SLURM queue reservations so our jobs will run faster. Please use the following aliases:

```
getcpu - one comput node for 3 hours
getcpu1  - one comput node for 1 hour
```

### GPU reservations

```
getgpu - one GPU for 3 hours (on days with GPU hands-on)
getgpu1 - one GPU for 1 hour (on days with GPU hands-on)
```

## Using Jupyter Technologies

### Jupyter Notebooks 

** NEED TO UPDATE **
The command to run *secure* Jupyter notebook servers for this class is the *start_python_hpc_notebook* command (this will be in your path).

```
[train147@comet-ln2 ~]$ which start_python_hpc_notebook
/share/apps/compute/si2020/reverse-proxy/start_python_hpc_notebook
```

The default time is set to 240 minutes in the compute partition. If you want you can give some other value for the time, you can provide it as an argument:


### JupyterLab servers

```
start_python_hpc_jupyterlab
```

### Notebooks hosting *Spark*
Session 4.1b. Scalable Machine Learning 

```
start_python_sparkr_cpu
start_python_sparkr_gpu (gives you a K80 in gpu-shared)
```





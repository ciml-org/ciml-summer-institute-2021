# 1.4_installing_your_own_miniconda_creating_conda_environments

## Setup for Expanse
Login with your Expanse username (xdtrXX). Note, this username is different from your XSEDE username (trainXX).

```
ssh <username>@login.expanse.sdsc.edu
```

#### Install Miniconda3 for Linux-x86_64
Download the Minconda3 installation script.

```
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

Run the Miniconda3 installation script in batch mode.
```
bash Miniconda3-latest-Linux-x86_64.sh -b -f
```

Activate conda.
```
source miniconda3/bin/activate
```

Run the conda init script. It will configure your .bashrc file for conda.
```
conda init
```

Turn off the base environment which is otherwise activated by default.
```
conda config --set auto_activate_base false
```

**Log out of your account and log back in** to make the changes to your .bashrc file take effect.


Test the installation.
```
conda list
```
A list of installed packages appears if it has been installed correctly.


#### Create a Conda Environment for the notebooks-sharing Repository
First, create a local copy of the training repository by cloning it with git.
```
git clone https://github.com/sdsc-hpc-training-org/notebooks-sharing.git
```

Then, create a Conda environment that contains specific versions of all the packages needed to reproduce the results of this study. Note, the `&` at the end. This will run the command in the background. The nohup command will keep the installation going, even if you logout or get disconnected. **Note, this step may run for an hour or longer.**
```
nohup conda env create -f notebooks-sharing/environment.yml > conda-notebook-env-install.log &
```

To monitor progress of the installation you can look at the bottom of the log file.
```
tail -20 conda-notebook-env-install.log
```

When the installation is completed, the `notebooks-sharing` environment should be in the list of the conda environments.
```
conda env list
```

You should see the following output:
```
# conda environments:
#
base                  *  /home/xdtr99/miniconda3
notebooks-sharing        /home/xdtr99/miniconda3/envs/notebooks-sharing
```

If you do not see the expected output, check the `conda-notebook-env-install.log` file for error messages.

#### What should I do if any of these steps fail?
First, you can post any problem in the Slack channel and we'll work with you to try to fix it. We still have a few days to fix any issues. The hands-on session on Thursday will use this setup.

If all fails, we have a backup solution. 

Run the following command to add a preinstalled notebooks-sharing conda environment to your .bashrc file.
```
echo "source /home/xdtr99/miniconda3/etc/profile.d/conda.sh" >> ~/.bashrc 
```

**Log out of your account and log back in** to make the changes to your .bashrc file take effect.


### Test your installation by launching Jupyter

Use the galyleo script to launch Jupyter on the Expanse command line. First, set the path to the galyleo script.

```
export PATH="/cm/shared/apps/sdsc/galyleo:${PATH}"
```

Run the galyleo script to launch Jupyter. We already specified your Expanse project allocation account number (sds184) with the `--account` option. In general, you can look up your allocation information from the [Expanse Portal Dashboad](https://portal.expanse.sdsc.edu) under the Clusters->Allocation and Usage Information tab.

```
galyleo.sh launch --account sds184 --partition 'shared' --cpus-per-task 1 --memory-per-node 4 --time-limit 00:30:00 --jupyter 'lab' --notebook-dir "/home/${USER}" --conda-env 'notebooks-sharing'
```

After you run this command, a URL is displayed. Copy this URL and paste it into a web browser to launch your interactive session.

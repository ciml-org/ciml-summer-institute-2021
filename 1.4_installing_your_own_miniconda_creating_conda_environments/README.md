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
Run the Miniconda3 installation script.
```
bash Miniconda3-latest-Linux-x86_64.sh
```
Follow the prompts on the installer screens. Answer **yes** to the prompts and accept the defaults.

The installer will modify your .bashrc file. To make the changes take effect, run the following command.
```
source ~/.bashrc
```

Test the installation.
```
conda list
```
A list of installed packages appears if it has been installed correctly.


#### Create a Conda Environment for this repository
First, we create a local copy of the following training repository by cloning it with git.
```
git clone https://github.com/sdsc-hpc-training-org/notebooks-sharing.git
```

Then, we create a Conda environment that contains specific versions of all the packages needed to reproduce the results of this study. Note, the `&` at the end. This will run the command in the background.
```
conda env create -f notebooks-sharing/environment.yml &
```
Finally, disown the background process so it continues even if your terminal window times out.
```
disown %1
```

### Run the Jupyter Notebooks in an Expanse Terminal

Use the galyleo script to launch Jupyter on the Expanse command line. First, set the path to the galyleo script.

```
export PATH="/cm/shared/apps/sdsc/galyleo:${PATH}"
```

Run the galyleo script to launch Jupyter. We already specified your Expanse project allocation account number (sds184) with the `--account option`. In general, you can look up your allocation information from the [Expanse Portal Dashboad](https://portal.expanse.sdsc.edu) under the Clusters->Allocation and Usage Information tab.

```
galyleo.sh launch --account sds184 --partition 'shared' --cpus-per-task 1 --memory-per-node 4 --time-limit 00:30:00 --jupyter 'lab' --notebook-dir "/home/${USER}" --conda-env 'notebooks-sharing' --quiet
```

After you run this command, a URL is displayed. Copy this URL and paste it into a web browser to launch your interactive session.

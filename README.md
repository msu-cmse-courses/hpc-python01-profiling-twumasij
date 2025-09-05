[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/6fE7C1Oq)
# High Performance Python - Course Preparation

This course will use GitHab Classroom and Jupyter Notebooks for delivering instructional materials. 
We'll also want to run Python on the HPCC instead of on your personal computer.

This means there are a couple of things you need to make sure you have set up ahead of our first class period.

## Accessing the HPCC

ICER's documentation offers several options for [accessing the HPCC](https://docs.icer.msu.edu/accessHPCC_overview/).
Since we'll be using Jupyter Notebooks, I personally recommend using [OnDemand](https://docs.icer.msu.edu/Open_OnDemand/).
You can also use the terminal in OnDemand to setup your [Python environment](#setting-up-the-python-environment) and [cloning GitHub Classroom repositories](#cloning-github-classroom-repositories).

OnDemand offers both the traditional Jupyter Notebook and the newer JupyterLab through the [Jupyter Interactive App](https://ondemand.hpcc.msu.edu/pun/sys/dashboard/batch_connect/sys/bc_icer_jupyter_ubuntu/session_contexts/new). I personally recommend JupyterLab because it offers a Table of Contents for easier navigation inside Notebooks! You can switch between traditional Notebooks and JupyterLab using the checkbox. The Python environment provided for this class already has both options installed.

Optionally, if you prefer to run Jupyter Notebooks through VSCode, you can use the OnDemand [Code Server App](https://ondemand.hpcc.msu.edu/pun/sys/dashboard/batch_connect/sys/bc_icer_codeserver_ubuntu/session_contexts/new) or you can follow [this guide](https://docs.icer.msu.edu/Jupyter_Notebook_in_VS_Code) from ICER.

## Cloning GitHub Classroom Repositories

If you're reading this README, you've already successfully accepted this assignment from GitHub Classroom.
Now, clone this repository **to the HPCC.** You'll need `hpc-python.yml` to set up your course Python environment in the [next step](#setting-up-python-environment).
The Notebook `workbook_profiling.ipynb` will be used **on the first day of class,** August 29, 2025.

GitHub offers a choice of URL to use when cloning a repository. The GitHub docs contain a [useful explanation of the different options](https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls); I personally recommend either cloning with HTTPS or SSH. If you want to clone with HTTPS, you'll need to set up a [personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) on GitHub. If you want to clone with SSH, you'll need to create an SSH key **on the HPCC** and upload it to GitHub. This option is more sophisticated and best done if you are already familiar with SSH keys; e.g., from using them to connect to the HPCC.

## Setting Up the Python Environment

We will use a large variety of Python packages in this course. I recommend using the [Conda package manager](https://docs.conda.io/en/latest/) to install and access them. 

Conda is installed as part of the open source [Miniforge](https://github.com/conda-forge/miniforge) Python distribution. You may also be familiar with Conda from the Anaconda and Miniconda Python distributions; however, ICER now officially recommends the use of Miniforge. You can read more about [migrating an existing installation](https://docs.icer.msu.edu/Replacing_conda_install/) if you are interested.

Whether you wish to access Conda through ICER's `Miniforge3` module or you wish to [install it yourself](docs.icer.msu.edu/Using_conda/), you have two options for this course: utilize the [preinstalled Python environment](#use-the-pre-installed-environment) (managed by me, so you don't have to do anything!) or [install the environment yourself](#install-the-environment-yourself).

### Use the Pre-Installed Environment

New for 2025 I'm offering a pre-installed Python environment through the course [Research Space](https://docs.icer.msu.edu/Research_Space/), `/mnt/research/CMSE_890_F25_601`.

Using this environment is straightforward. In your home directory, there should be a file called `.condarc` (you can create it if it's not already there). Open this file in your favorite editor and add:
```
envs_dirs:
  - /mnt/research/CMSE_890_F25_601/envs/
```
to the bottom of the file. If the `envs_dirs` section is already present, just add the `/mnt/research/CMSE_890_F25_601/envs/` line.

To use this environment from the command line, run
```
module purge
module load Miniforge3 OpenMPI
conda activate hpc-python
```
Alternatively, you can load `Conda` instead of `Miniforge3` if you have your own installation.

### Install the Environment Yourself

As part of this repository, I have included `hpc-python.yml`, a file compatible with Conda, that will install the necessary packages into a *separate environment*. This way, if you already use Conda to manage Python for your research on the HPCC, this course will not interfere.

Assuming you're using ICER's Miniforge installation, you'll want to run:
```
ssh dev-amd20-v100
module purge
module load Miniforge3 OpenMPI
conda env create -f hpc-python.yml
```
If you're using your own Conda installation, replace `Minigforge3` with `Conda`.

**The installation will probably take a while!** Please do it before class.

**Creating this environment *must* be done on the V100 development node,** as this is the GPU will we use in the last part of class. If you install the environment on a node without a GPU, the GPU-related packages will not install correctly. Note that you don't have to keep using `dev-amd20-v100` once the environment is installed.

To use this environment from the command line, run
```
module purge
module load Miniforge3 OpenMPI
conda activate hpc-python
```
Alternatively, you can load `Conda` instead of `Miniforge3` if you have your own installation. If using the Jupyter OnDemand app, you'll need to specify `hpc-python` as the name of the environment you're using.

## Pre-Class Survey

This class is open to students with a wide range of backgrounds and research goals. Please fill out this [pre-class survey](https://docs.google.com/forms/d/e/1FAIpQLSeuwv3JQioi-WoDjQ8_e2NbWzSa7Y6Eo6GrYjSA60AWjd8Mqw/viewform?usp=sf_link) so I can better adapt the material to your needs.

## Reading for Day 1

These brief readings will familiarize you with concepts needed for in-class activities on Day 1.

- [Profiling and Timing Magic Commands](https://jakevdp.github.io/PythonDataScienceHandbook/01.07-timing-and-profiling.html)
- [Python Operator Precedence](https://introcs.cs.princeton.edu/python/appendix_precedence/)
# Using this repository

This is an overview of the structure of this repository and how to use it.

## Repository Structure
The structure of this repository is:

- Project Folders
  - Each folder contains all of the files needed (notebooks, data, etc.) for a single project.
- Dependency File
  - A special file that lists the dependencies required to run the notebooks. *n.b. this is shared across all projects*
- Readme File
  - A readme file that lists all the projects, their short descriptions, and how to run them.

## Using Binder
[Binder](https://mybinder.org/) is a free web service that copies a public git repository and launches a single user Jupyter server with its contents.
It accomplishes this by building a docker image with the `repo2docker` tool and launches it on their platform.
While not technically accurate, for simplicity, you can think of this as a virtual machine.
Building the docker image starts from a blank slate, installs jupyter and the dependencies you provide, and then launches as a service.
This has advantages in that the runtime environment is exactly that which you specify and disadvantages that the image must be rebuilt after any changes to this repository, sometimes a lengthy process. 
However, the build process uses caching which speeds up subsequent builds. It's a small price to pay for portability and reproducability. 

Getting binder to build a repository is as simple as going to [mybinder.org](https://mybinder.org/) and inputting the url of the repository. 
Using the default options will launch a jupyter server with the same directory structure as the original repository. 
The user can launch any of the notebooks in the repository. 

Binder offers a button that can be added to any markdown file (README.md). 
With this you can make the launch process a single click for your users.
You can even provide a path to a notebook file to open by default.
So, you can list all of the projects in the readme which have their own buttons.

> **Note:** Binder instances are ephemeral! They will be destroyed after 20 minutes of inactivity or 12 hours total runtime. 
> This is done to keep the hardware resources under control and the service free. 

Here is a [full tutorial on using binder](https://github.com/alan-turing-institute/the-turing-way/blob/master/workshops/boost-research-reproducibility-binder/workshop-presentations/zero-to-binder-python.md).

## Generating Dependency Files
Binder uses [configuration files](https://mybinder.readthedocs.io/en/latest/using/config_files.html) to define the environment in which the notebooks are run.
The main challenge of generating the dependency file is listing only the packages you need and nothing more. 
If you were to run `pip freeze` on your machine, it would list every package that has been installed *system-wide*.
There will be a lot of unneccessary packages in this list.
However, we can use virtual environments to start from a clean slate and install only what we need.
In essence, virtual environments are a combination of downloading software to a user folder and then altering `PATH` such that those packages are used over the system installed versions.
There are two main tools to do this: venv and conda.

### venv
Venv is the built-in python virtual environment module. 
It is very simple to use, but can only manage python packages.

```bash
python -m venv <venv_folder>      # Create the virtual environment
source <venv_folder>/bin/activate # Activate the virtual environment
pip install <packages>            # Install packages
pip freeze > requirements.txt     # List packages and their dependecies in requirements.txt
# Run some python scripts in environment
deactivate                        # Deactivate virtual environment and return to normal shell
```

### [conda](https://docs.conda.io/en/latest/)
[Conda](https://docs.conda.io/en/latest/) takes the idea of python virtual environments to the next level.
It allows you to install any kind of package into a virtual environment, not just python packages. 
e.g. C libraries, command line tools, GUI applications, etc.
If your project depends on a tool outside of the python ecosystem (e.g. `ffmpeg` for rendering animations), conda is the way to go.
However, it is a bit more complicated to get running.
First you must [install conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/index.html). 
There are [two main distributions of conda](https://docs.conda.io/projects/conda/en/latest/user-guide/install/download.html#anaconda-or-miniconda).
[Anaconda](https://docs.conda.io/projects/conda/en/latest/glossary.html#anaconda-glossary) comes with 250+ automatically installed, open-source scientific packages and their dependencies.
[Miniconda](https://docs.conda.io/en/latest/miniconda.html) is stripped down to just the package manager.
I would recommend miniconda as it is simpler, smaller, and you can install anything you want after the fact.

```bash
conda env create <env_name>        # Create the virtual environment
conda activate <env_name>          # Activate the virtual environment
conda install <packages>           # Install packages
conda env export > environment.yml # List packages and their dependecies in environment.yml
# Run some commands in environment
conda deactivate                   # Deactivate virtual environment and return to normal shell
```
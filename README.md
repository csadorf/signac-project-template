# About

This repository provides a template for [signac-flow](https://bitbucket.org/glotzer/signac-flow) projects based on the simple data management framework [signac](https://signac.readthedocs.io/).

# Documentation

The template project features the generation of a p-V phase diagram of a simulated Lennard-Jones (LJ) fluid and an ideal gas estimate.
The LJ fluid is sampled via molecular dynamics using the HOOMD-blue particle simulation toolkit.

The [signac](https://signac.readthedocs.io) data management framework itself does not enforce any specific workflow.
Basic workflow management functions are implemented in the complementary [signac-flow](https://bitbucket.org/glotzer/signac-flow) package, which provides the `FlowProject` class.
This template is designed to demonstrate how to specialize a `FlowProject` to implement a workflow on top of a **signac** project.

Beginners should start by looking through the [signac documentation](https://signac.readthedocs.io), especially the [tutorial](https://signac.readthedocs.io/en/latest/tutorial.html) and the [signac-flowdocumentation](https://signac-flow.readthedocs.io).

# Quickstart

To get, started clone or better **fork** the repository.
To execute the example workflow, follow these steps:

We start by initializing the project and a few state points with the `init.py` module.
```
python src/init.py 42
```
The number 42 is the random seed used for initialization, feel free to replace it with a different number or a text string, which will be converted into a numeric random seed.

All project-related data space operations are defined within the `src/operations.py` module.
These operations can also be executed, for example with `python src/operations.py initialize`.

The project's workflow is defined within the `src/project.py` module.
We can checkout the project's status, e.g., with:
```
python src/project.py status --detailed --parameters p
```
We use the ``--detailed`` flag to show the labels explicitly for each job.
The ``--parameters`` (``-p``) pargument specifies state point parameters that should be shown in the status overview.
In this case we specify to show the `p` variable, which stands for pressure.

The status will also show all pending operations (initialize/estimate-volume/sample).
The command
```
python src/project.py run
```
will execute the immediately pending operations for the complete data space.
You may need to execute this command multiple times to cycle through all pending operations.

Finally, we can analyze the data using a jupyter notebook, simply execute ``jupyter notebook`` within the project's root directory and open the `src/analysis.ipynb` notebook.

# Modules

The following list is a brief overview of the modules and scripts to be found within the project template.

Modules, that are usually modified by the user:

 * ``src/init.py`` - **Init**ialize the project and parameter space.
 * ``src/operations.py`` - Definition and execution of python-based data space **operations**.
 * ``src/project.py`` - Configuration, execution, and submission of the **project** work flow.

Other modules:

  * ``src/environment.py`` - Custom **environment** definitions
  * ``src/util/misc.py`` - **Misc**ellaneous utility functions
  * ``src/util/hoomd.py`` - Various utility functions to be used with **HOOMD**-blue

# Merge upstream updates

To synchronize your fork with the upstream repository, follow these steps:
```
cd your_project
git remote add upstream https://github.com/glotzerlab/signac-project-template.git
git fetch upstream
```
Then either merge
```
git merge upstream/master
```
or rebase
```
git rebase upstream/master
```
to synchronize your local master branch with the upstream master branch.

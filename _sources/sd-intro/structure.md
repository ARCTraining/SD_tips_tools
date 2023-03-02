# Laying out a coding project

Good project layout ensures:

- Integrity of the data
- Portability of the project
- Ease to pick the project back up after a break or change in personnel

There is no single way to organise a project.... but we need to take advantage
some conventions.

## Basic Structure Suggestion

Suppose you want to create a **Python** repository called `first-model`.
The most basic structure for this project should look like:

```bash
first-model
├── src
│   └── __init__.py
└── tests
|   ├── __init__.py
|   └── test_first_model.py
├── README.md
├── requirements
└── setup
```

### Modules & Packages

- Modules: code files with `.py` extension
- Packages: directory to group modules. For a folder with several modules to be
recognized as a package it is necessary to include the file `__init__.py`.

```{note}
You also can group your modules in sub-packages.
```

### Tests

It's important to ensure that the code is bug-free and returns the expected
results. Later in this course we will delve into how to properly test our code.
For the moment let's look at the test structure:

- All tests units (files and methods) must be named starting with `test_`
and placed inside a package (or subpackage) called `tests`.
- Tests can be grouped in just one folder for the entire repository (as shown in
the structure above) or they can be organized within each package/subpackage.

By organizing tests as described, you can use frameworks like
[pytest](https://pypi.org/project/pytest/) to automatically fetch all test files
in the repository and execute them.

> The pytest framework makes it easy to write small tests, yet scales to support
> complex functional testing for applications and libraries.

\- [pytest](https://pypi.org/project/pytest/)

### Requirements

Configuration file that list all required external packages for your Python project.
Two types of requirements file are quite common

- `requirements.txt`
- `environment.yml`

The `requirements.txt` file is a simple file where the content looks like:

```bash
python==3.11
numpy
tensorflow==2.3.1
```

The `environment.yml` file is a file used by `conda` to create an environment.
The content looks like:

```bash
name: envName
channels:
  - conda-forge
  - defaults
dependencies:
  - python==3.11
  - numpy
  - tensorflow==2.3.1
```

## Naming conventions

Python conventions are governed largely by a set of documents called Python
Enhancement Proposals (PEP). You can see more about PEP index in the official
[Python website](https://www.python.org/dev/peps/).

The PEP related with python coding style is the
[PEP8 -- Style Guide for Python Code](https://www.python.org/dev/peps/pep-0008/).

This file has guidance for all layout related aspects. For instance we are
interested in the [Package and Module Names](https://www.python.org/dev/peps/pep-0008/#package-and-module-names) section.

> **Modules** should have short, all-lowercase names. *Underscores can be used* in
> the module name if it improves readability. Python **packages** should also have
> short, all-lowercase names, although the use of *underscores is discouraged*.

## Creating project structure

You can create a project structure manually. But there are some automated
approaches for this.

### Conda + Cookie cutter

After create an empty repository, you can create and then activate our conda
environment.

```bash
conda create -n reproPython python=3.9
$ source activate reproPython
```

The next step is to install cookiecutter (instructions
[here](https://pypi.org/project/cookiecutter/)).

> Cookiecutter is a command-line utility that creates projects from
> cookiecutters (project templates), e.g. creating a Python package project
> from a Python package project template.

Then you must choose a project template.
A good example to be used in scientific projects can be found here:
`https://github.com/mkrapp/cookiecutter-reproducible-science.`

Now we can create the project structure by combining the Cookiecutter package
with the GitHub repository. Again from the shell:

```bash
cookiecutter gh:mkrapp/cookiecutter-reproducible-science
```

By using this method, the project structure should look like:

```bash
.
├── AUTHORS.md
├── LICENSE
├── README.md
├── bin                <- Your compiled model code can be stored here (not tracked by git)
├── config             <- Configuration files, e.g., for doxygen or for your model if needed
├── data
│   ├── external       <- Data from third party sources.
│   ├── interim        <- Intermediate data that has been transformed.
│   ├── processed      <- The final, canonical data sets for modelling.
│   └── raw            <- The original, immutable data dump.
├── docs               <- Documentation, e.g., doxygen or scientific papers (not tracked by git)
├── notebooks          <- Ipython or R notebooks
├── reports            <- For a manuscript source, e.g., LaTeX, Markdown, etc., or any project reports
│   └── figures        <- Figures for the manuscript or reports
└── src                <- Source code for this project
    ├── data           <- scripts and programs to process data
    ├── external       <- Any external source code, e.g., pull other git projects, or external libraries
    ├── models         <- Source code for your own model
    ├── tools          <- Any helper scripts go here
    └── visualization  <- Scripts for visualisation of your results, e.g., matplotlib, ggplot2 related.
```

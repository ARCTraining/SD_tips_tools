# Package managers

Package managers help you install packages. Some help you install virtual environments
as well. Better known python package managers include
[conda](https://docs.conda.io/en/latest/), [pip](https://pip.pypa.io/en/stable/),
[poetry](https://python-poetry.org/)

|                           | conda    | pip | poetry     |
|---------------------------|----------|-----|------------|
|audience                   | research | all | developers |
|manage python packages     | ✅       |  ✅ | ✅         |
|manage non-python packages | ✅       | ❌  | ❌         |
|choose python version      | ✅       | ❌  | ❌         |
|manage virtual envs        | ✅       | ❌  | ✅         |
|easy interface             | ❌       | ✅  | ❌         |
|fast                       | ❌       | ✅  | ✅         |

## Rules for choosing a package manager

1. Choose one
1. Stick with it

## Virtual Environments

> Python applications will often use packages and modules that don’t come as part of the standard library. Applications will sometimes need a specific version of a library, because the application may require that a particular bug has been fixed or the application may be written using an obsolete version of the library’s interface.

> This means it may not be possible for one Python installation to meet the requirements of every application. If application A needs version 1.0 of a particular module but application B needs version 2.0, then the requirements are in conflict and installing either version 1.0 or 2.0 will leave one application unable to run.

> The solution for this problem is to create a virtual environment, a self-contained directory tree that contains a Python installation for a particular version of Python, plus a number of additional packages.

> Different applications can then use different virtual environments. To resolve the earlier example of conflicting requirements, application A can have its own virtual environment with version 1.0 installed while application B has another virtual environment with version 2.0. If application B requires a library be upgraded to version 3.0, this will not affect application A’s environment.

\- [The Python Tutorial](https://docs.python.org/3/tutorial/venv.html#introduction)

## Environment: Conda example

There are several ways to create/manage python environments.
We chose [conda](https://docs.conda.io/en/latest/) because it is the de facto
standard in science, and because it can natively install libraries such as
[fftw](https://anaconda.org/conda-forge/fftw),
[vtk](https://anaconda.org/conda-forge/vtk), or even Python, R, and Julia
themselves.

### Create environment from a `yml` file

#### Step 1: environment.yml

The `environment.yml` file specifies the dependencies that will be installed in
your environment.

An example of content for this file type is:

```yaml
name: course
dependencies:
  - python>=3.8
  - numpy=1.13
  - matplotlib=3.*
  - pandas
```

* The first line of the `yml` file sets the new environment's name.
* By defining dependencies you can:
  * Define the version number by fixing the major and minor version numbers.
  * Use the wildcard `*` to allow the patch version vary.
  * Use `>=` to set minimum version.
  * Do not specify version.

```{seealso}
For more details see [Creating an environment file manually](https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#create-env-file-manually).
```

#### Step 2: create a new virtual environment

```bash
conda env create -f environment.yml
```

```{tip}
The option `-f` is short for `--file`.

Other options includes:

- `-n` or `--name`
- `-e` or `--envs`
- `-h` or `--help`
```

```{warning}
it is important to note that creating the environment does not automatically
activate it.
```

#### Step 3: activate the environment

```bash
conda activate course
```

```{tip}
Replace `course` with the environment name or directory path.
```

```{note}
You can also deactivate the environment at any time: 
just run `conda deactivate`.
```

```{warning}
`conda activate` and `conda deactivate` only work on conda 4.6 and later
versions (use `conda info` to check conda version).
For conda versions prior to 4.6, run:

- Windows: `activate` or `deactivate`
- Linux and macOS: `source activate` or `source deactivate`

```

### Managing packages

#### Search package

Search for a package to see if it is available to
conda install

```bash
conda search package-name
```

#### Install a new package

To install a conda package in the current environment:

```bash
conda install package-name
```

#### Update an existing package

To update a package in the current environment:

```bash
conda update package-name
```

#### Remove an existing package

To remove a package from the current environment:

```bash
conda remove package-name
```

```{note}
If you are not in the environment, you still can perform the above procedures.
To do so, it will be necessary to indicate the desired environment in the 
command, for example:

:::bash
conda install -n ENVNAME package-name
:::

```

#### List of packages

To view a list of packages in active environment:

```bash
conda list
```

### Managing environments

#### List available environments

To list all available environments:

```bash
conda env list
```

#### Remove an environment

```bash
conda remove -n ENVNAME --all
```

#### Share an environment

Create the latest `yml` environment file

```bash
conda env export --name ENVNAME > file-name.yml
```

Share the `.yml` file.

```{tip}
Note the difference between the `environment.yml` file created before with this
latest file.
```

To create a clean `yml` environment file:

```bash
conda env export --name ENVNAME --no-builds | grep -v "prefix" > file-name.yml
```

#### Clone an environment

Make an exact copy of an environment

```bash
conda create --clone ENVNAME --name NEWENV
```

```{seealso}
Check this [Conda Cheat Sheet](https://docs.conda.io/projects/conda/en/latest/_downloads/843d9e0198f2a193a3484886fa28163c/conda-cheatsheet.pdf)!
```

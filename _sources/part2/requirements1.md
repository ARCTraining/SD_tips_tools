# Git Installation Instructions

Please follow the instructions bellow to install and setting up Git.

## Linux

Check if `git` is available on your machine by running

```bash
git --version
```

The above command returns the `git` version (if available).

If `git` is not already available on your machine you can try to install it via your distribution package manager (e.g. `apt-get` or `yum`), for example:

```bash
sudo apt-get install git
```

or

```bash
sudo yum install git
```

## MacOS

The `XCode` command line tools come with `Git` so no need to do anything more, as long as you can run the following in your terminal:

```bash
git --version
```

## Windows

Install the [GitHub Desktop Client](http://windows.github.com/).
This comes with both a GUI client as well as the [Git Bash](https://gitforwindows.org/) terminal client which we will use during the course. In some instances Git Bash may need to be installed separately. In order to use conda with Git Bash follow the instructions [here](https://discuss.codecademy.com/t/setting-up-conda-in-git-bash/534473)

You'll know it has worked when you can open a Git Bash terminal (the window should have a title that starts with MINGW32) and get the Git version by running

```bash
git --version
```

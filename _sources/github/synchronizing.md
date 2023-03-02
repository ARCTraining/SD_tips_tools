# Synchronizing: Local & GitHub

To sync a local repository with a GitHub repository you need two repositories
(one local and one online) and then set up a link between them.
The two possible paths are:

- Local --> GitHub
  1. Have a local git repository (which you started with `git init`).
  2. Have an empty repository on GitHub.
  3. Make the GitHub repository a remote for the local repository.
     - `$ git remote add origin https://github.com/...`
     - The name `origin` is a local nickname for your remote repository.

- GitHub --> Local
  1. Have a repository on GitHub.
  2. Clone the GitHub repository in your local machine. (this will create a local repo)
     - `$ git clone https://github.com/...`
     - git clone copies a remote repository to create a local repository  with a remote called `origin` automatically set up.

## Finding the GitHub repo link

Each repository has an unique address composed by

- GitHub link
- GitHub user name
- GitHub repository name

You can find the complete link in the main page of the repository, under the
`code` download green button (see image bellow)

![Code Download](https://docs.github.com/assets/cb-20363/images/help/repository/code-button.png)

Then, choose one of the tabs (`HTTPS`, `SSH`, or `GitHub CLI`) and copy the address:

![Repo link](https://docs.github.com/assets/cb-33207/images/help/repository/https-url-clone-cli.png)

## Push local changes to a remote repo

This command will push the changes (git commits) from our local repository to
the repository on GitHub:

```bash
git push origin main
```

```{note}
You can push content to different branches, just change `main` for the desired
branch name in the above command
```

## Pull remote changes to a local repo

This command will pull changes from the remote repository to the local one:

```bash
git pull origin main
```

## The "-u" flag

Sometimes is useful to create a short for the `git push origin main` (or
`git pull origin main`). To do this, you need run one time the full command
with the `-u` flag:

```bash
git push -u origin main
```

After that, you can simple use `git push` or `git pull` without the `origin main`
arguments.

Please note that this works for the branch passed with the `-u` flag. If you want
to `pull/push` in other branches you should use the complete command.

## A Basic Collaborative Workflow

In practice, it is good to be sure that you have an updated version of the
repository you are collaborating on, so you should git pull before making our
changes. The basic collaborative workflow would be:

- update your local repo with `git pull origin main`,
- make your changes and stage them with `git add`,
- commit your changes with `git commit -m`, and
- upload the changes to GitHub with `git push origin main`

```{note}
You can (and should) use other branches besides main.
```

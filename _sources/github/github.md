# Github repository

```{note}
All instructions and images showed bellow are provided by GitHub [here](https://docs.github.com/en/get-started/quickstart/create-a-repo).
```

## Creating a GitHub Repository

- In the upper-right corner of any page, use the  drop-down menu, and select New repository.

![New repo dropdown](https://docs.github.com/assets/cb-11427/images/help/repository/repo-create.png)

- Type a short, memorable name for your repository.

![New repo: name](https://docs.github.com/assets/cb-25139/images/help/repository/create-repository-name.png)

- Optionally, add a description of your repository.

![New repo: description](https://docs.github.com/assets/cb-26377/images/help/repository/create-repository-desc.png)

- Choose a repository visibility.

![New repo: visibility](https://docs.github.com/assets/cb-20877/images/help/repository/create-repository-public-private.png)

- Select Initialize this repository with a README. You can also choose start with the licence and the `.gitignore` files.

![New repo: readme](https://docs.github.com/assets/cb-49938/images/help/repository/initialize-with-readme.png)

:::{note}
You should also add a **.gitignore** and a **licence**. Please see 
[here](https://arctraining.github.io/swd2_git/11-licensing/) for more
information related with Licence.

For research, it is also convenient to create a **citation** file. 
See [here](https://arctraining.github.io/swd2_git/12-citation/)
for more information related with Citation file.
:::

- Click Create repository.

![New repo: create button](https://docs.github.com/assets/cb-19887/images/help/repository/create-repository-button.png)

## Making and committing changes

- In your repository's list of files, click README.md.

![Select File](https://docs.github.com/assets/cb-44661/images/help/repository/create-commit-open-readme.png)

- Above the file's content, click in the pencil icon.
- On the Edit file tab, type some text.
  - You can preview (`Preview changes` tab) your changes before commit.
  - New content is highlighted in green
  - Removed content is highlighted in red
- At the bottom of the page, type a short, meaningful commit message that describes the change you made to the file.

![Commit](https://docs.github.com/assets/cb-9378/images/help/repository/write-commit-message-quick-pull.png)

- Below the commit message fields, decide whether to add your commit to the current branch or to a new branch.

![Branche](https://docs.github.com/assets/cb-32137/images/help/repository/choose-commit-branch.png)

- Click Propose file change

![Propose file change](https://docs.github.com/assets/cb-13681/images/help/repository/propose-file-change-quick-pull.png)

```{note}
the `git add` command is not necessary here. Github automatically put the
changed file in the staged area.
Despite simplifying the workflow for small changes, this procedure makes it impossible to add several changes to the same commit.
```

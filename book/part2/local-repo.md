# Creating a local repository

Once Git is configured, we can start using it.
Let's create a directory for our work and then move into that directory:

```bash
mkdir inflammation
cd inflammation
```

Then we tell Git to make `inflammation` a `repository` (a place where
Git can store versions of our files):

```bash
git init
```

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

```bash
ls
```

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `inflammation`
called `.git`:

```bash
ls -a
```

```bash
. .. .git
```

Git stores information about the project in this special sub-directory.

```{warning}
If we ever delete it, we will lose the project’s history.
```

## Checking our project

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

```bash
git status
```

and the output

```bash
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

```{note}
If you are using a different version of git than I am, then then the exact
wording of the output might be slightly different.
```

## Removing a local repository

If for some reason you want the repository to stop being a git repository,
just delete the hidden `.git` folder:

```bash
rm -rf .git
```

```{warning}
Be careful! Running this command in the wrong directory, will remove the entire
git-history of a project you might wanted to keep. Therefore, always check your
current directory using the command `pwd`.
```

## Example: Jane's multiple projects

Jane starts a new project, `infection`, related to her `inflammation` project.

Jane enters the following sequence of commands to create one Git repository
inside another:

```bash
cd                   # return to home directory
mkdir inflammation   # make a new directory inflammation
cd inflammation      # go into inflammation
git init             # make the inflammation directory a Git repository
mkdir infections     # make a sub-directory inflammation/infection
cd infection         # go into inflammation/infection
git init             # make the infection sub-directory a Git repository
```

(Notice here that the `inflammation` project is now also tracking the entire
`infection` repository.)

:::{dropdown} Why is it a bad idea to do this?

Git repositories can interfere with each other if they are "nested" in the
directory of another: the outer repository will try to version-control
the inner repository. Therefore, it's best to create each new Git
repository in a separate directory.

To be sure that there is no conflicting
repository in the directory, check the output of `git status`. If it looks
like the following, you are good to go to create a new repository as shown
above:

```bash
git status
```

```bash
fatal: Not a git repository (or any of the parent directories): .git
```

:::

:::{dropdown} How can Jane undo her last `git init`?

Jane can run the following command from inside the infection directory:

```bash
rm -rf .git
```

:::

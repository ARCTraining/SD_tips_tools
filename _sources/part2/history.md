# Exploring History

## Identifying files old versions

As we saw in the previous lesson, each file version is related with a commit,
and we can refer to commits by their `identifiers`.

There is more than one way to do this.

First, lets use `$ git log` to see the commits that we made:

:::{dropdown} Check the `$ git log`

```text
commit da43c773c5a022b603e3387da8ac1dbc603a3562 (HEAD -> main)
Author: Patricia Ternes <p.ternesdallagnollo@leeds.ac.uk>
Date:   Thu Mar 3 19:02:38 2022 +0000

    Add note about project responsibilities

commit cf53ab40ddc732676c7e7a65063629b5df1c96f5
Author: Patricia Ternes <p.ternesdallagnollo@leeds.ac.uk>
Date:   Thu Mar 3 18:00:28 2022 +0000

    Start notes on the patient inflammation project
```

:::

### Complete ID

We can refer to commits using those long strings of digits and letters
that `git log` displays. These are unique IDs for the changes,
and "unique" really does mean unique: every change to any set of files on
any computer has a unique 40-character identifier.

- Our first commit was given the ID `cf53ab40ddc732676c7e7a65063629b5df1c96f5`
- Our last  commit was given the ID `da43c773c5a022b603e3387da8ac1dbc603a3562`

### Short ID

Typing out random 40-character strings is annoying, so Git lets us use just the
first few characters (7 by default) as a Short ID:

- Our first commit was given the short ID `cf53ab4`
- Our last  commit was given the short ID `da43c77`

```{note}
The short commit id can be up to the shortest 4 characters long, as long as it
is unique for a commit in the same repository.
```

### HEAD ID

Note that our last commit also has a `HEAD` identification.
The HEAD ID is a simple way to refer to newest commits.

- You can refer to the most recent commit of the working directory by using the identifier `HEAD`
- You can refer to previous commits. We do that by adding `~n` to refer to the commit `n` before HEAD,(where `n = 1,2,3,...`), e.g.:
  - HEAD~1
  - HEAD~2
  - HEAD~13

In this way, we can build up a chain of commits.
The most recent end of the chain is referred to as `HEAD`;
we can refer to previous commits using the `~` notation,
so `HEAD~1` (pronounced "head minus one") means "the previous commit",
while `HEAD~123` goes back 123 commits from where we are now.

## Reviewing changes

There are two types of useful reviews:

- `git diff`: show changes between commits
- `git show`: show the commit log

```{seealso}
The above definition is naive and only addresses the use of commands with
commits. However, these commands have more options and utility, please see
more about `show` [here](https://git-scm.com/docs/git-show)
and about `diff` [here](https://git-scm.com/docs/git-diff)
```

### Using `diff`

- `$ git diff`: show you any uncommitted changes since the last commit
- `$ git diff HEAD`: show you any uncommitted changes since the last commit
- `$ git diff <commitID>`: show you any difference since the commit related with `<commitID>`
- `$ git diff <commitID1> <commitID2>`: show you any difference betwenn the commit `<commitID1>` and `<commitID2>`

See bellow two examples:

:::{dropdown} `$ git diff HEAD HEAD~1`

```text
diff --git a/project.txt b/project.txt
index c5f0d2c..36b3292 100644
--- a/project.txt
+++ b/project.txt
@@ -1,4 +1,2 @@
 Some initial data analysis to identify how inflammation changes over time after surgery.
-Jane is a Data Scientist and Samit is a statistician. We'll need to determine
-who is responsible for what in this project.
```

:::

:::{dropdown} `$ git diff HEAD~1 HEAD`

```text
diff --git a/project.txt b/project.txt
index 36b3292..c5f0d2c 100644
--- a/project.txt
+++ b/project.txt
@@ -1,2 +1,4 @@
 Some initial data analysis to identify how inflammation changes over time after surgery.
+Jane is a Data Scientist and Samit is a statistician. We'll need to determine
+who is responsible for what in this project.
```

:::

### Using `show`

For commits it shows the log message.

See the examples

:::{dropdown} `$ git show cf53ab40ddc732676c7e7a65063629b5df1c96f5`

```text
commit cf53ab40ddc732676c7e7a65063629b5df1c96f5
Author: Patricia Ternes <p.ternesdallagnollo@leeds.ac.uk>
Date:   Thu Mar 3 18:00:28 2022 +0000

    Start notes on the patient inflammation project

diff --git a/project.txt b/project.txt
new file mode 100644
index 0000000..36b3292
--- /dev/null
+++ b/project.txt
@@ -0,0 +1,2 @@
+Some initial data analysis to identify how inflammation changes over time after surgery.
+

```

:::

:::{dropdown} `$ git show da43c77`

```text
commit da43c773c5a022b603e3387da8ac1dbc603a3562 (HEAD)
Author: Patricia Ternes <p.ternesdallagnollo@leeds.ac.uk>
Date:   Thu Mar 3 19:02:38 2022 +0000

    Add note about project responsibilities

diff --git a/project.txt b/project.txt
index 36b3292..c5f0d2c 100644
--- a/project.txt
+++ b/project.txt
@@ -1,2 +1,4 @@
 Some initial data analysis to identify how inflammation changes over time after surgery.
+Jane is a Data Scientist and Samit is a statistician. We'll need to determine
+who is responsible for what in this project.
```

:::

## Recovering old versions: `checkout`

As you might guess from its name, `git checkout` checks out (i.e., restores) an
old version of a file. To use this command we need to provide two information,
the commit identifier and the file name, e.g.:

```bash
git checkout da43c77 project.txt
```

After restore an old version, you need to add and commit the change. Now see
the log! Note that even when restoring an old version, you do not overwrite/lose
commits already made.

```{warning}
`git checkout` is also used in other contexts like change branch, so be sure to
include the file name.
```

:::{dropdown} See below what happens if you use `cheackout` without include a file name
First type the checkout command:

```bash
$ git checkout da43c77
Note: switching to 'da43c77'.

You are in 'detached HEAD' state. You can look around, make experimental
changes and commit them, and you can discard any commits you make in this
state without impacting any branches by switching back to a branch.

If you want to create a new branch to retain commits you create, you may
do so (now or later) by using -c with the switch command. Example:

  git switch -c <new-branch-name>

Or undo this operation with:

  git switch -

Turn off this advice by setting config variable advice.detachedHead to false

HEAD is now at da43c77 Add note about project responsibilities
```

If you forget `project.txt` in that command, Git will tell you that "You are in
'detached HEAD' state." In this state, you shouldn't make any changes.

You can fix this by reattaching your head using `git checkout main`.

:::

# Branching

Branching is a version control concept that means you can create separate lines
of development derived from your main line.
This allows you to make changes to the code, adding functionality or making
improvements without messing up your original main code.
When working in a team this means you can separate each team members development
work allowing them to work on their problem in isolation.

Changes in one branch can be brought into another (such as back into the main
branch) through merging but by separating work between branches this merge step
becomes a specific end point that we work too at which conflicts are resolved
rather than continuously managing conflicts when everyone works on the same
branch.

To see what branches are available in your local repository you can
type `git branch`:

```bash
git branch 
```

The output should looks like:

```text
* main
```

The `main` branch is created when the repository is initialised.

## Creating new branches

You can create
new branches by using the `git branch` command followed by the name of the
branch you want to create. Let's create a new `experimental` branch.

```bash
git branch experimental
```

By checking again the available brances:

```text
  experimental
* main
```

The asterisk symbol indicates which branch we are currently on (or in git-speak
which branch we have checked out).

We can switch to a different branch by using the `git checkout` command.

```bash
git branch experimental
```

## Changes in different branches

### Changes in `experimental` branch

Lets make some changes in our branches and and see what happens.

First, you can create an `experimentalfile.txt` in your `experimental` branch.
Then add some text in this file:

```text
Our experiment is performed as follows:

1. ....
2. ....
3. ....
```

Now add and commit this change.

```bash
git add experimentalfile.txt
git commit -m "crating experiment description file"
```

### Changes in `main` branch

First go back to the main branch

```bash
git checkout main
```

```{note}
Note that your `experimentalfile.txt` file disappeared.
Don't worry, the file wasn't deleted, it's just on a different branch.
```

Now lets create a new `mainfile.txt` and add some text on it.

Now navigate around your folders and files, change branches and do the same.
What did you notice?

Although the `mainfile.txt` file was created on the main branch it also appears
on the experimental branch. This is because changes are only linked to some
branch after the git commit step. So lets fix this:

```bash
git checkout main
git add mainfile.txt
git commit -m "creating the mainfile"
```

Now navigate again around your folders and files and branches.

## Merging branches

If you are satisfied with your work on the auxiliary branch (here the
`experimental`), you can add the changes from that branch to main.
To do this:

```bash
git checkout main
git merge experimental
```

and the output:

```text
Merge made by the 'recursive' strategy.
 experimentalfile.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 experimentalfile.txt
```

Again, navigate around your folders, files and branches.
Make sure you can understand what happened.

## Conflict

In the previous example the changes performed on the `experimental` branch and the
`main` branch was unrelated and when joining the two branches we had no problem.

Now we're going to purposefully provoke a conflict. For this open the file in
the `main` branch and delete the entire last sentence.
Don't forget to commit the change.

Now switch to the `experimental` branch, open the file and instead of deleting
the sentence, just make a small change to it.
Again be sure to commit the changes

Now let's combine the changes:

```bash
git checkout main
git merge experimental
```

The output:

```text
Auto-merging project.txt
CONFLICT (content): Merge conflict in project.txt
Automatic merge failed; fix conflicts and then commit the result.
```

This process generated a conflict because you tried to change a phrase that
no longer exists. Don't worry, this is quite common.

Open your project file and see how it is

```text
Some initial data analysis to identify how inflammation changes over time after surgery.
<<<<<<< HEAD
=======
Jane is a Data Scientist and Samit is a statistician. We will need to determine
who is responsible for what in this project.
>>>>>>> experimental
```

The conflict (second sentence) is placed between `<<<<<<< >>>>>>>`. Now you just
need to fix the text, **save** and **commit** the change. The final version can be
the `main` version, the `experimental` version, or something between them. It is
entirely **up to you**.

My file after fix the conflict is:

```text
Some initial data analysis to identify how inflammation changes over time after surgery.
Jane is a Data Scientist and Samit is a statistician.
```

This type of situation is more common when different people use different branches.

## Remove unnecessary branches

It is recommended to delete any secondary branches after merging them with main.
Even if you want to make changes to a secondary branch in the future.
In that case, create a new branch at the time you decide to work on it.
This avoids using outdated branches, consequently avoiding unnecessary conflicts.

To delete the `experimental` branch:

```bash
git branch -D experimental
```

```text
Deleted branch experimental (was 3099b91).
```

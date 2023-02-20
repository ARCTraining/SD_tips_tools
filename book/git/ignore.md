# Ignoring Things

What if we have files that we do not want Git to track for us,
like backup files created by our editor
or intermediate files created during data analysis?
Let's create a few dummy files in the `inflammation` directory:

```bash
mkdir results
touch a.dat b.dat c.dat results/a.out results/b.out
```

and see what Git says:

```bash
git status
```

```text
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

 a.dat
 b.dat
 c.dat
 results/
nothing added to commit but untracked files present (use "git add" to track)
```

Putting these files under version control would be a waste of disk space.
What's worse,
having them all listed could distract us from changes that actually matter,
so let's tell Git to ignore them.

We do this by creating a file in the root directory of our project
called `.gitignore`. Inside `.gitignore` file:

```text
*.dat
results/
```

These patterns tell Git to ignore any file whose name ends in `.dat`
and everything in the `results` directory.
(If any of these files were already being tracked,
Git would continue to track them.)

:::{dropdown} Check the status!

```bash
$ git status
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)

 .gitignore
nothing added to commit but untracked files present (use "git add" to track)
```

:::

You might think we wouldn't want to track it,
but everyone we're sharing our repository with will probably want to ignore
the same things that we're ignoring.
Let's add and commit `.gitignore`:

```bash
git add .gitignore
git commit -m "Add the ignore file"
```

# Additional tips

## Code formatting

Why does formatting matter?

- Code is read more often than written
- Setting up a formatter in your editor takes 5 minutes
- Those 5 minutes are redeemed across the lifetime of the project

### Ugly formatting example

Put the following into a file `myscript.py` and save it.

```bash
x = {  'a':37,'b':42,
'c':927}
y = 'hello '+       'world'
class foo  (     object  ):
   def f    (self   ):
       return       y **2
   def g(self, x :int,
       y : int=42
       ) -> int:
       return x--y
def f  (   a ) :
   return      37+-a[42-a :  y*3]
```

### Black Code Formatter

We chose [black](https://pypi.org/project/black/) because it has very few
options with which to fiddle.

First you need to install `Black` in your environment:

```bash
conda install black
```

Then, the simplest way to use is

```bash
black myscript.py
```

The code should be automatically formatted to:

```bash
x = {"a": 37, "b": 42, "c": 927}
y = "hello " + "world"

class foo(object):
    def f(self):
        return y ** 2

    def g(self, x: int, y: int = 42) -> int:
        return x - -y
```

```{warning}
Note that `black` just fix the code layout - this code still has syntax error!
```

## Integrated development environment (IDE)

Using an Integrated development environment (IDE) will certainly save you time,
but the advantages of using an IDE go beyond that. Below are some IDE advantages

1. Syntax highlighting
2. Text autocompletion
3. Refactoring options
4. Easily Importing libraries
5. Build, compile, or run

### Visual Studio Code

You may already have a preferred IDE that you use regularly, however we strongly
suggest that you use VS Code for this course and afterwards replicate the setup
as you choose. If you already have VS Code installed please make sure it is
updated to the latest version.

To install VS Code follow the instructions [here](https://code.visualstudio.com/).

Below are some VSC advantages

1. IntelliSense: Go beyond syntax highlighting and autocomplete
2. Run & Debug: Debug code right from the editor
3. Built-in Git: Review diffs, stage files, and make commits right from the editor.
4. Extensible and customizable: Install extensions to add new languages, themes, debuggers, and to connect to additional services.


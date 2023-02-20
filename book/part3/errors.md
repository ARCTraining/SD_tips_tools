# Python Errors

There are (at least) two distinguishable kinds of errors:

- syntax errors
- exceptions

## Syntax errors

Syntax errors, also known as parsing errors, are perhaps the most common kind of complaint you get while you are still learning Python.
It is an error in the syntax or the 'grammar' of a programming language.

## Exceptions

> Even if a statement or expression is syntactically correct, it may cause an error when an attempt is made to execute it. Errors detected during execution are called exceptions and are not unconditionally fatal
Most exceptions are not handled by programs, however, and result in error messages.

\- [Python documentation](https://docs.python.org/3/tutorial/errors.html#exceptions)

### Exception example

```python
def divtwoby(a):
    return 2/a
```

Now try `divtwoby(10)` and `divtwoby(0)`. There is no syntax error in this function, so the first try should work and return the
result `0.2`, but the second should return an error message like
`ZeroDivisionError: division by zero`.

```{seealso}
If you are not sure what the error means, you can get more information in this [glossary](https://docs.python.org/3/library/exceptions.html#base-classes).
```

## Identifying errors

The code bellow has an intentional error.
Try to see whats is wrong and then, compile to see the python message.

```python
# This code has an intentional error.
def favourite_ice_cream():
    ice_creams = [
        'chocolate',
        'vanilla',
        'strawberry'
    ]
    print(ice_creams[3])

favourite_ice_cream()
```

Output

```text
    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-1-777c68a47889> in <module>
          8     print(ice_creams[3])
          9 
    ---> 10 favourite_ice_cream()
    

    <ipython-input-1-777c68a47889> in favourite_ice_cream()
          6         'strawberry'
          7     ]
    ----> 8     print(ice_creams[3])
          9 
         10 favourite_ice_cream()


    IndexError: list index out of range
```

Errors in Python have a very specific form, called a **traceback**.

:::{dropdown} Fixing

```python
# This code has an intentional error.
def favourite_ice_cream():
    ice_creams = [
        'chocolate',
        'vanilla',
        'strawberry'
    ]
    print(ice_creams[1])  # chose any index between 0 and 2 (len(ice_creams)-1).

favourite_ice_cream()
```

Output

```text
    vanilla
```

:::

### Example: Syntax errors

```python
def some_function()
    msg = 'hello, world!'
    print(msg)
     return msg
```

:::{dropdown} Output
      File "script.py", line 1
        def some_function()
                           ^
    SyntaxError: invalid syntax
:::

:::{dropdown} Fixing

- the function syntax is: `def function_name():`
- indentation is important

```python
def some_function():  # the function syntax is: `def function_name():`
    msg = 'hello, world!'
    print(msg)
    return msg  # indentation is important!
```

:::

### Example: Tabs and spaces

```python
def some_function():
 msg = 'hello, world!'
 print(msg)
        return msg
```

:::{dropdown} Output
      File "script.py", line 4
        return msg
                  ^
    TabError: inconsistent use of tabs and spaces in indentation
:::

:::{dropdown} Fixing

We can produce the correct indentation with spaces and tabs, but we
can not mixing them in the same file.

Following [PEP8](https://peps.python.org/pep-0008/#tabs-or-spaces):

- Spaces are the preferred indentation method.
- Tabs should be used solely to remain consistent with code that is already indented with tabs.

The fixed code is:

```python
def some_function():
    msg = 'hello, world!'  # change one tab for 4 spaces
    print(msg)  # change one tab for 4 spaces
    return msg  # fix indentation
```

:::

### Examples: Variable name errors

#### Define variable

```python
print(a)
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-7-bca0e2660b9f> in <module>
    ----> 1 print(a)
    

    NameError: name 'a' is not defined
```

:::

:::{dropdown} Fixing

```python
a = 10  # define the variable a
print(a)
```

Output

```text
    10
```

:::

#### Initialise a counter

```python
for number in range(10):
    count = count + number
print('The count is:', count)
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-9-64cce701dab9> in <module>
          1 for number in range(10):
    ----> 2     count = count + number
          3 print('The count is:', count)


    NameError: name 'count' is not defined
```

:::

:::{dropdown} Fixing

```python
count = 0  # initialise a counter variable
for number in range(10):
    count = count + number
print('The count is:', count)
```

Output

```text

    The count is: 45
```

:::

#### Misspelling

```python
Count = 0
for number in range(10):
    count = count + number
print('The count is:', count)
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-10-7190aa30e930> in <module>
          1 Count = 0
          2 for number in range(10):
    ----> 3     count = count + number
          4 print('The count is:', count)


    NameError: name 'count' is not defined
```

:::

:::{dropdown} Fixing

```python
count = 0  # variable names are case sensitive
for number in range(10):
    count = count + number
print('The count is:', count)
```

Output

```text
    The count is: 45
```

:::

### Example: Index errors

```python
letters = ['a', 'b', 'c']
print('Letter #1 is', letters[0])
print('Letter #2 is', letters[1])
print('Letter #3 is', letters[2])
print('Letter #4 is', letters[3])
```

:::{dropdown} Output

```text
    Letter #1 is a
    Letter #2 is b
    Letter #3 is c

    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-13-af8f97c9a1ff> in <module>
          3 print('Letter #2 is', letters[1])
          4 print('Letter #3 is', letters[2])
    ----> 5 print('Letter #4 is', letters[3])
    

    IndexError: list index out of range
```

:::

:::{dropdown} Fixing

```python
letters = ['a', 'b', 'c']
print('Letter #1 is', letters[0])
print('Letter #2 is', letters[1])
print('Letter #3 is', letters[2])
# print('Letter #4 is', letters[3])  # index from 0 up to len(letters)-1
```

Output

```text
    Letter #1 is a
    Letter #2 is b
    Letter #3 is c
```

:::

### Example: File errors

#### Open missing files

```python
file_handle = open('myfile.txt', 'r')
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------
    FileNotFoundError                         Traceback (most recent call last)
    <ipython-input-1-30deac02fc31> in <module>
    ----> 1 file_handle = open('myfile.txt', 'r')
          2 
          3 # To read (option `'r'`) a file, this file should exist.
          4 # Create a file for this code work

    FileNotFoundError: [Errno 2] No such file or directory: 'myfile.txt'
```

:::

:::{dropdown} Fixing

- To read (option `'r'`) a file, this file should exist.
- Create a file for this code work

:::

#### Wrong file operations

```python
file_handle = open('myfile.txt', 'w') # Opened a file for writing (which will create an empty file)
file_handle.read() # Try to read from it
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------

    UnsupportedOperation                      Traceback (most recent call last)

    <ipython-input-16-e31f2da4c7f8> in <module>
          1 file_handle = open('myfile.txt', 'w') # Opened a file for writing (which will create an empty file)
    ----> 2 file_handle.read() # Try to read from it
          3 
          4 # To read a file, you should open a file using the option 'r' (read)


    UnsupportedOperation: not readable
```

:::{dropdown} Fixing

- To read a file, you should open a file using the option 'r' (read)

:::

## Activity: `print_message`

Read the Python code and the resulting traceback below, and answer the following questions:  

1. How many levels does the traceback have?
2. What is the function name where the error occurred?
3. On which line number in this function did the error occur?
4. What is the type of error?
5. What is the error message?

:::{dropdown} Answers

1. 3
2. print_message
3. 13
4. KeyError
5. KeyError: 'Friday'

:::

```python
# This code has an intentional error. Do not type it directly;
# use it for reference to understand the error message below.
def print_message(day):
    messages = {
        'monday': 'Hello, world!',
        'tuesday': 'Today is Tuesday!',
        'wednesday': 'It is the middle of the week.',
        'thursday': 'Today is Donnerstag in German!',
        'friday': 'Last day of the week!',
        'saturday': 'Hooray for the weekend!',
        'sunday': 'Aw, the weekend is almost over.'
    }
    print(messages[day])

def print_friday_message():
    print_message('Friday')

print_friday_message()
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-17-fd935ca3ca2c> in <module>
         16     print_message('Friday')
         17 
    ---> 18 print_friday_message()
    

    <ipython-input-17-fd935ca3ca2c> in print_friday_message()
         14 
         15 def print_friday_message():
    ---> 16     print_message('Friday')
         17 
         18 print_friday_message()


    <ipython-input-17-fd935ca3ca2c> in print_message(day)
         11         'sunday': 'Aw, the weekend is almost over.'
         12     }
    ---> 13     print(messages[day])
         14 
         15 def print_friday_message():


    KeyError: 'Friday'
```

:::

:::{dropdown} Fixing

```python
# This code was fixed
def print_message(day):
    messages = {
        'monday': 'Hello, world!',
        'tuesday': 'Today is Tuesday!',
        'wednesday': 'It is the middle of the week.',
        'thursday': 'Today is Donnerstag in German!',
        'friday': 'Last day of the week!',
        'saturday': 'Hooray for the weekend!',
        'sunday': 'Aw, the weekend is almost over.'
    }
    print(messages[day])

def print_friday_message():
    print_message('friday')  # fix: change the key "Friday" by "friday"

print_friday_message()
```

:::

## Activity: Identifying syntax errors

1. Read the code below, and (without running it) try to identify what the errors are.
2. Run the code, and read the error message.
3. Is it a SyntaxError or an IndentationError?
4. Fix the error.

Repeat steps 2, 3, and 4 until you have fixed all the errors.

:::{dropdown} Answers

- There is a syntax error (line 1) and an indentation error (line 3)
- fix line 1: should be: `def another_function():`
- fix line 3: remove one space
:::

```python
def another_function
  print('Syntax errors are annoying.')
   print('But at least Python tells us about them!')
  print('So they are usually not too hard to fix.')
```

:::{dropdown} Output 1

```text
      File "<ipython-input-19-ee417b4e3bb6>", line 1
        def another_function
                            ^
    SyntaxError: invalid syntax
```

:::

:::{dropdown} Output 2

```text
      File "<ipython-input-2-333d41c4e2fd>", line 3
        print('But at least Python tells us about them!')
        ^
    IndentationError: unexpected indent
```

:::

:::{dropdown} Fixing

```python
def another_function():  # add `():` after `another_function`
  print('Syntax errors are annoying.')
  print('But at least Python tells us about them!')  # remove one space
  print('So they are usually not too hard to fix.')
```

:::

## Activity: Identifying variable name errors

1. Read the code below, and (without running it) try to identify what the errors are.
2. Run the code, and read the error message. What type of NameError do you think this is? In other words, is it a string with no quotes, a misspelled variable, or a variable that should have been defined but was not?
3. Fix the error.
4. Repeat steps 2 and 3, until you have fixed all the errors.

:::{dropdown} Answers

- `number` and `Number`: misspelled variable
- `message` was not defined
- `a` with no quotes
:::

```python
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (Number % 3) == 0:
        message = message + a
    else:
        message = message + 'b'
print(message)
```

:::{dropdown} Output 1

```text
    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-21-801cad40fd35> in <module>
          1 for number in range(10):
          2     # use a if the number is a multiple of 3, otherwise use b
    ----> 3     if (Number % 3) == 0:
          4         message = message + a
          5     else:


    NameError: name 'Number' is not defined
```

:::

:::{dropdown} Output 2

```text
    ---------------------------------------------------------------------------
    NameError                                 Traceback (most recent call last)
    <ipython-input-3-23edc33d497d> in <module>
          2     # use a if the number is a multiple of 3, otherwise use b
          3     if (number % 3) == 0:
    ----> 4         message = message + a
          5     else:
          6         message = message + 'b'

    NameError: name 'message' is not defined
```

:::

:::{dropdown} Output 3

```text
    ---------------------------------------------------------------------------
    NameError                                 Traceback (most recent call last)
    <ipython-input-4-7d71049d6c51> in <module>
          3     # use a if the number is a multiple of 3, otherwise use b
          4     if (number % 3) == 0:
    ----> 5         message = message + a
          6     else:
          7         message = message + 'b'

    NameError: name 'a' is not defined
```

:::

:::{dropdown} Fixing

```python
message = ''   # define the variable (here: empty string)
for number in range(10):
    # use a if the number is a multiple of 3, otherwise use b
    if (number % 3) == 0:  # fix the misspelled variable
        message = message + 'a'  # add quotes to string
    else:
        message = message + 'b'
print(message)
```

Output

```text
    abbabbabba
```

:::

## Activity: Identifying index errors

1. Read the code below, and (without running it) try to identify what the errors are.
2. Run the code, and read the error message. What type of error is it?
3. Fix the error.

:::{dropdown} Answers

- index should be between 0 and 3.
- IndexError
- change the number for something between 0 and 3.
:::

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favourite season is ', seasons[4])
```

:::{dropdown} Output

```text
    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-23-c82c08095380> in <module>
          1 seasons = ['Spring', 'Summer', 'Fall', 'Winter']
    ----> 2 print('My favourite season is ', seasons[4])
    

    IndexError: list index out of range
```

:::

:::{dropdown} Fixing

```python
seasons = ['Spring', 'Summer', 'Fall', 'Winter']
print('My favourite season is ', seasons[2])  # chose a number between 0 and 3
```

Output

```text
    My favourite season is  Fall
```

:::

:::{tip}
You can find a Jupyter Notebook to run all functions presented above in [this
link](https://github.com/ARCTraining/SD_tips_tools/tree/main/notebooks/errors.ipynb).
:::

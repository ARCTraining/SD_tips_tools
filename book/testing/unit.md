# Unit testing

Now lets use the Test-driven development methodology with `pytest` to create a
efficient `Unit Testing`.

## The Problem

For this example lets considering three functions:

- even_odd: function that returns `Even` or `Odd` for a given number.
- get_largest: function that returns the largest value between three inputs.
- dice_rolling: function that that works as a dice-rolling simulator, i.e., that randomly returns a value between 1 and 6.

**Which tests should we create for each function?**

## Project Structure

The first step is to create the proper structure for creating the main code and test units.

```bash
some-functions
├── src
│   └── __init__.py
│   └── functions.py
└── tests
│   ├── __init__.py
│   └── test_dice.py
│   └── test_evenodd.py
│   └── test_largest.py
└── environment.yml
```

## Setting the environment

For this task we are going to write some functions in `python` and then, test them
with `pytest`. Therefore we need a python environment with these packages.
We also want to use `black` to linting the code, so the `environment.yml` should
look like:

```bash
name: testing
dependencies:
  - python
  - black
  - pytest
```

To install/activate the environment:

```bash
$ conda env create -f environment.yml
$ conda activate testing
```

## Even or Odd?

Before jump to the function itself lets think about what tests we should do for
an even/odd function. Some ideas are:

- Is the output a string?
- Does the function work for a small even number?
- Does the function work for a large even number?
- Does the function work for a small odd number?
- Does the function work for a large odd number?
- Does the function work for negative number (in ever situation above)?
- Does the function work for zero?
- What the function should return for a non-integer value? >> define here >> message: "Please use an integer value"

### Even or odd test unit

Now inside the file `test_evenodd.py` write a test function for every item listed above.
Something like:

```python
import src.functions as fc


def test_output_type():
    assert isinstance(fc.even_odd(5), str)


def test_even_small():
    assert fc.even_odd(4) == "Even"


def test_even_large():
    assert fc.even_odd(178418932) == "Even"


def test_odd_small():
    assert fc.even_odd(178418931) == "Odd"


def test_odd_large():
    assert fc.even_odd(178418931) == "Odd"


def test_zero():
    assert fc.even_odd(0) == "Even"


def test_neven_small():
    assert fc.even_odd(-4) == "Even"


def test_neven_large():
    assert fc.even_odd(-178418932) == "Even"


def test_nodd_small():
    assert fc.even_odd(-178418931) == "Odd"


def test_nodd_large():
    assert fc.even_odd(-178418931) == "Odd"


def test_no_integer():
    assert fc.even_odd(1.5) == "Please use an integer value"
```

### The `even_odd` function

With the test unit in hand, you can now create the `even_odd` function.
To do this, open the file `functions.py` and type your function.

```python
def even_odd(number):
    if isinstance(number, int):
        if number % 2 == 0:
            return "Even"
        else:
            return "Odd"
    else:
        return "Please use an integer value"
```

### Testing the `even_odd` function

To test if your function is working in scenarios that you planned before,
you just need to use the `pytest` command.

```bash
$pytest
============================= test session starts =============================
platform linux -- Python 3.11.0, pytest-7.1.2, pluggy-1.0.0
rootdir: /localhome/home/earpte/Documents/RSE-support/FLUDS/testing
plugins: lazy-fixture-0.6.3
collected 11 items                                                                                                                                                                               

tests/test_evenodd.py ...........                                         [100%]

============================== 11 passed in 0.02s ==============================
```

## The largest and the dice problems

Now, do the same with the other two functions.

1. First list all scenarios and the desired outputs.
2. Write a test unit that covers all scenarios
3. Write the function
4. Test the function using `pytest`

:::{dropdown} Check the example test unit for the largest problem:

```python
import src.functions as fc


def test_first_crescent():
    assert fc.get_largest(3, 1, 2) == 3


def test_first_decrescent():
    assert fc.get_largest(3, 2, 1) == 3


def test_second_crescent():
    assert fc.get_largest(1, 3, 2) == 3


def test_second_decrescent():
    assert fc.get_largest(2, 3, 1) == 3


def test_third_crescent():
    assert fc.get_largest(1, 2, 3) == 3


def test_third_decrescent():
    assert fc.get_largest(2, 1, 3) == 3


def test_float():
    assert fc.get_largest(2.0, 1.4, 3.1) == 3.1


def test_negative():
    assert fc.get_largest(-2, -1, -3) == -1


def test_negative_positive():
    assert fc.get_largest(-2, 1, 0) == 1
```

:::

:::{dropdown} Check the example function for the largest problem:

```python
def get_largest(x, y, z):
    # use the x value as largest value
    largest = x

    # if y is large: replace the largest value by y
    if largest < y:
        largest = y

    # if z is large: replace the largest value by z
    if largest < z:
        largest = z

    # return the largest value
    return largest
```

:::

For the Dice problem some additional knowledge may be helpful.

- You can define variables to be used by `pytest` via `@pytest.fixture`
- You may have problems in verify if two float numbers are equal, try the `pytest.approx` function to set the number of decimal places to be considered.

:::{dropdown} Check the example test unit for the dice problem:

```python
import src.functions as fc
import pytest


@pytest.fixture
def N():
    return 100000


@pytest.fixture
def faces(N):
    faces = [fc.dice_rolling() for _ in range(N)]
    return faces


@pytest.fixture
def probabilities(faces, N):
    p = [faces.count(i + 1) / N for i in range(6)]
    return p


def test_type():
    assert isinstance(fc.dice_rolling(), int), "The function should return an integer"


def test_min_value(faces):
    assert all(
        face >= 1 for face in faces
    ), "The function should return a minimum value of 1"


def test_max_value(faces):
    assert all(
        face <= 6 for face in faces
    ), "The function should return a maximum value of 6"


def test_uniform_distribution(probabilities):
    assert all(pytest.approx(p, abs=1e-2) == 1 / 6 for p in probabilities)

```

:::

:::{dropdown} Check the example function for the dice problem:

```python
from random import randint

def dice_rolling():
    face = randint(1,6)
    return face
```

:::
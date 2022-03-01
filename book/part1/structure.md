# Laying out a coding project

Good project layout ensures:

- Integrity of the data
- Portability of the project
- Ease to pick the project back up after a break or change in personnel

There is no single way to organise a project.... but we need to take advantage
some conventions.

## Basic Structure Suggestion

Suppose you want to create a **Python** repository called `first-model`.
The most basic structure for this project should look like:

```bash
first-model
├── first_model
│   └── __init__.py
└── tests
|   ├── __init__.py
|   └── test_first_model.py
├── README.md
├── requirements
└── setup
```

## Modules & Packages

- Modules: code files with `.py` extension
- Packages: directory to group modules. For a folder with several modules to be
recognized as a package it is necessary to include the file `__init__.py`.

```{note}
You also can group your modules in sub-packages.
```

## Test & pytest

It's important to ensure that the code is bug-free and returns the expected
results. Later in this course we will delve into how to properly test our code.
For the moment let's look at the test structure:

- All tests units (files and methods) must be named starting with `test_`
and placed inside a package (or subpackage) called `tests`.
- Tests can be grouped in just one folder for the entire repository (as shown in
the structure above) or they can be organized within each package/subpackage.

By organizing tests as described, you can use frameworks like
[pytest](https://pypi.org/project/pytest/) to automatically fetch all test files
in the repository and execute them.

> The pytest framework makes it easy to write small tests, yet scales to support
> complex functional testing for applications and libraries.

\- [pytest](https://pypi.org/project/pytest/)

Consider the following method:

```
def inc(x):
    return x + 1
```

See the `test_sample.py` example:

```python
# content of test_sample.py
def test_answer():
    assert inc(3) == 5
```

By simple executing `pytest`:

```bash
$ pytest
============================= test session starts =============================
collected 1 items

test_sample.py F

================================== FAILURES ===================================
_________________________________ test_answer _________________________________

    def test_answer():
>       assert inc(3) == 5
E       assert 4 == 5
E        +  where 4 = inc(3)

test_sample.py:5: AssertionError
========================== 1 failed in 0.04 seconds ===========================
```


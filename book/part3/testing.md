# Testing

Testing should be a seamless part of scientific software development process.
This is analogous to experiment design in the experimental science world.

At the beginning of a new project, tests can be used to help guide the overall
design of the project. The act of writing tests can help clarify how the
software should be perform when you are done.

In fact, starting to write the tests before you even write the software might be
advisable. (as we are going to see, such a practice is called test-driven development).

## A few reasons to do testing

- testing saves time.
- tests (should) ensure code is correct
- **runnable specification:** best way to let others know what a function should do and not do.
- **reproducible debugging:** debugging that happened and is saved for later reuse
- easier to modify since results can be tested

## Tests at different scales

- **Unit Tests:** Unit tests investigate the behaviors of units of code (such as functions, classes, or data structures). By validating each software unit across the valid range of its input and output parameters, tracking down unexpected behaviors that may appear when the units are combined is made vastly simpler.
- **Regression Tests:** Regression tests defend against new bugs, or regressions, which might appear due to new software and updates.
- **Integration Tests:** Integration tests check that various pieces of the software work together as expected.

:::{tip}
Always start at the smallest scale!
:::

## Testing vocabulary

- **fixture:** input data
- **action:** function that is being tested
- **expected result:** the output that should be obtained
- **actual result:** the output that is obtained
- **coverage:** proportion of all possible paths in the code that the tests take

## Testing frameworks

Each time we make changes to a code, we would like to test it. This can be
tedious and that might prevent us from testing. We want to make testing as
easy as version control is. A testing framework can help us.

### py.test

The testing framework we will discuss today is a python library called
[`pytest`](https://pytest.org/en/7.1.x/) to automatically fetch all test files
in the repository and execute them.

> The `pytest` framework makes it easy to write small tests, yet scales to support
> complex functional testing for applications and libraries.

\- [pytest](https://pypi.org/project/pytest/)

In `pytest`, each test is a function whose name begins with the letters test.
We can group tests together in files whose names also begin with the letters test.
To execute our tests we run the command `pytest`.
This automatically searches the current directory and its subdirectories for
test files, and runs the tests they contain.

Consider the following method:

```python
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

Stepping back, the most important part of this lesson isn't the details of the
`pytest` library. It's that your time is more valuable than the computer's,
so you should spend it doing the things computers can't, like thinking of
interesting test cases and what your code is actually supposed to do.

## Debugging Steps

1. Know what it’s supposed to do:
   - “My program doesn’t work” isn’t good enough: in order to diagnose and fix problems, we need to be able to tell correct output from incorrect.
2. Make it fail every time:
   - We can only debug something when it fails, so the second step is always to find a test case that makes it fail every time.
   - The “every time” part is important because few things are more frustrating than debugging an intermittent problem.
3. Make it fail fast:
   - If it takes 20 minutes for the bug to surface, we can only do three experiments an hour.
4. Change one thing at a time:
   - Every time we make a change, however small, we should re-run our tests immediately.
   - The more things we change at once, the harder it is to know what’s responsible for what.
5. Keep track of what you’ve done:
   - Good scientists keep track of what they’ve done so that they can reproduce their work.
   - Don’t waste time repeating the same experiments or running ones whose results won’t be interesting.
6. Be humble:
   - If we can’t find a bug in 10 minutes, we should be humble and ask for help.
   - Asking for help also helps alleviate confirmation bias.
   - People who aren’t emotionally invested in the code can be more objective, which is why they’re often able to spot the simple mistakes we have overlooked.

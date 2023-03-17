# Test-driven development

An assertion checks that something is true at a particular point in the program.
The next step is to check the overall behaviour of a piece of code, i.e., to make sure that it produces the right output when it’s given a particular input.

- For example, suppose we need to find the result of a number divided by another number:

## Naive solution

- Write a function `a_div_b`.
- Call it interactively on two or three different inputs.
- If it produces the wrong answer, fix the function and re-run that test.

This clearly works — after all, thousands of scientists are doing it right now — but there’s a better way

## Test-driven development solution

- Write a short function for each test.
- Write a `a_div_b` function that should pass those tests.
- If `a_div_b` produces any wrong answers, fix it and re-run the test functions.

Writing the tests before writing the function they exercise is called **test-driven development (TDD)**.
Its advocates believe it produces better code faster because:

- If people write tests after writing the thing to be tested, they are subject to confirmation bias, i.e., they subconsciously write tests to show that their code is correct, rather than to find errors.
- Writing tests helps programmers figure out what the function is actually supposed to do.

## Possible tests: `a_div_b` example

Let's think in all possible scenarios for this problem and how we could test them.

### Bigger by smaller

Example:

- Using this range `4, 2`, the answer should be `2`.

:::{dropdown} Check the example code:

```python
assert a_div_b(4, 2) == 2
```

:::

### Smaller by bigger

Example:

- Using this range `2, 4`, the answer should be `0.5`.

:::{dropdown} Check the example code:

```python
assert a_div_b(2, 4) == 0.5
```

:::

### Negative numbers

If we pass two negative numbers, the answer should be positive.
We can do two different tests here:

:::{dropdown} Check the example code:

```python
assert a_div_b(-4, -2) == 2
```

:::

Or...

:::{dropdown} Check the example code:

```python
assert a_div_b(-4, -2) > 0
```

:::

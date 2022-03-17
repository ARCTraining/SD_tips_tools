# Assertions

The first step toward getting the right answers from our programs is to assume
that mistakes will happen and to guard against them.
This is called **defensive programming**.

The most common way to do a defensive programming is
to add **assertions** to our code so that it checks itself as
it runs. An assertion is simply a statement that something
**must be true** at a certain point in a program.

When Python sees one, it evaluates the assertion’s condition.
If it’s true, Python does nothing, but if it’s false, Python **halts** the program
immediately and **prints the error message** if one is provided.

For example, this piece of code halts as soon as the loop encounters a value that isn’t positive:

```python
numbers = [1.5, 2.3, 0.7, 0.001, 4.4]
total = 0.0

for num in numbers:
    assert num > 0.0, 'Data should only contain positive values'
    total += num
print('total is:', total)
```

Broadly speaking, assertions fall into three categories:

- A **precondition** is something that must be true at the start of a function in order for it to work correctly.
- A **postcondition** is something that the function guarantees is true when it finishes.
- An **invariant** is something that is always true at a particular point inside a piece of code.

## The rectangle example

Suppose we are representing rectangles using a tuple of **four coordinates** (x0, y0, x1, y1), representing the lower left and upper right corners of the rectangle.

In order to do some calculations, we need to **normalize the rectangle** so that the lower left corner is at the origin and the longest side is 1.0 units long. This function does that, but checks that its input is correctly formatted and that its result makes sense:

```python
def normalize_rectangle(rect):
    """Normalizes a rectangle so that it is at the origin and 1.0 units long on its longest axis.
    Input should be of the format (x0, y0, x1, y1).
    (x0, y0) and (x1, y1) define the lower left and upper right corners
    of the rectangle, respectively."""
    
    assert len(rect) == 4, 'Rectangles must contain 4 coordinates'
    x0, y0, x1, y1 = rect
    assert x0 < x1, 'Invalid X coordinates'
    assert y0 < y1, 'Invalid Y coordinates'

    dx = x1 - x0
    dy = y1 - y0
    
    if dx > dy:
        scaled = float(dx) / dy
        upper_x, upper_y = 1.0, scaled
    else:
        scaled = float(dx) / dy
        upper_x, upper_y = scaled, 1.0

    assert 0 < upper_x <= 1.0, 'Calculated upper X coordinate invalid'
    assert 0 < upper_y <= 1.0, 'Calculated upper Y coordinate invalid'

    return (0, 0, upper_x, upper_y)
```

- The preconditions on lines 7, 9, and 10 catch invalid inputs
- The post-conditions on lines 20 and 21 help us catch bugs by telling us when our calculations might have been incorrect.

Let's perform some tests.
Call `print(normalize_rectangle( values ))` and replace by:

1. (0.0, 1.0, 2.0) - missing the fourth coordinate
2. (1.0, 2.0, 4.0, 5.0) - x-axis inverted
3. (0.0, 0.0, 1.0, 5.0) - rectangle that is taller than it is wide
4. (0.0, 0.0, 5.0, 1.0) - rectangle that is wider than it is tall

Now answer:

- Can you understand all outputs?
- Is the code right? Do we need to fix something?

:::{dropdown} Answers

- 1 and 2 are warnings for wrong inputs.
- 3 is everything right
- 4 should work but it is nothing.

Fix the code block:

```python
    if dx > dy:
        scaled = float(dx) / dy # change for scaled = float(dy) / dx
        upper_x, upper_y = 1.0, scaled
```

:::

## Activity: Pre and post-conditions

Suppose you are writing a function called `average` that calculates the
average of the numbers in a list, something like:

```python
def average(values):
    return (sum(values)/len(values))
```

1. What `pre-conditions` and `post-conditions` would you write for it?
2. Compare your answer to your neighbors: can you think of a function that will pass your tests but not his/hers or vice versa?

:::{dropdown} Some ideas
Precondition:

- Is it a list?
- List length must have greater than zero values
- No stupid values (invariant)

Postcondition:

- Average is within the range of the given data
:::

## Activity: testing assertions

Consider the following function:

```python
def get_total_cars(values):
    assert len(values) > 0
    for element in values:
        assert int(element)
    values = [int(element) for element in values]
    total = sum(values)
    assert total > 0
    return total
```

Given a sequence of a number of cars, the function `get_total_cars` returns the
total number of cars. So, `get_total_cars([1, 2, 3, 4])` should return `10`.

- Explain in words what the assertions in this function check, and for each one,
give an example of input that will make that assertion fail.

:::{dropdown} Answers

- The first assertion checks that the input sequence values is not empty.
  - An empty sequence such as `[]` will make it fail.
- The second assertion checks that each value in the list can be turned into an integer.
  - Input such as `[1, 2,'c', 3]` will make it fail.
- The third assertion checks that the total of the list is greater than 0.
  - Input such as `[-10, 2, 3]` will make it fail.
:::

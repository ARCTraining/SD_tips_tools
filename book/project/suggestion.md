# Suggested solution: Monte Carlo

> Monte Carlo methods, or Monte Carlo experiments, are a broad class of
> computational algorithms that rely on repeated random sampling to obtain
> numerical results. The underlying concept is to use randomness to solve
> problems that might be deterministic in principle. They are often used in
> physical and mathematical problems and are most useful when it is difficult
> or impossible to use other approaches.
\- [Wikipedia](https://en.wikipedia.org/wiki/Monte_Carlo_method)

See this video to having some insights:

<iframe width="560" height="315" src="https://www.youtube.com/embed/g06ecTJGY7U" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Solution suggested steps

The code should:

1. Receive a radius value
2. Sort a random x-value inside a line of 2*radius size
3. Sort a random y-value inside a line of 2*radius size
4. Check if the (x,y) point is inside or outside the circle
   - If inside, add 1 to a counter
5. Determine the area by using the proportion of total sorted points and the total number of points inside the circle.
6. Determine the error between the calculated area and the theoretical area.
   - If the error is lower than the desired error, stop the code.
   - If the error is higher, repeat steps from 2 to 6.

## The main code file

If you need some ideas related with the main code, you can see my code bellow.

:::{dropdown} See the main code

```python
# `circle_area.py` file content
# you can use this file by typing: $ python circle_area.py
import numpy as np
import matplotlib.pyplot as plt


class Circle:
    def __init__(self, radius, centre, desired_error) -> None:
        # circle related variables
        self.r = radius
        self.centre = centre
        self.desired_error = desired_error

        # status lists
        self.errors = []
        self.areas = []
        self.pi = []
        self.N = []

    @staticmethod
    def get_2D_point(r, center):
        x = np.random.uniform(low=(center[0] - r), high=(center[0] + r))
        y = np.random.uniform(low=(center[1] - r), high=(center[1] + r))
        point = np.array([x, y])
        return point

    @staticmethod
    def get_area(radius, inside, total):
        area = (inside * (2.0 * radius) ** 2) / total
        return area

    @staticmethod
    def get_error(theoretical, calculated):
        error = abs(calculated * 100.0 / theoretical - 100.0)
        return error

    @staticmethod
    def get_pi(r, area):
        pi = area / r / r
        return pi

    def monte_carlo_2D_step(self, inside, total):
        # sort a random point
        point = self.get_2D_point(self.r, self.centre)

        # determine if it is inside the circle
        distance = np.linalg.norm(point - np.array(self.centre))
        if distance < self.r:
            inside += 1

        # update total
        total += 1

        return inside, total

    def get_circle_stats(self):
        try:
            # ensure that all values are valid
            self.r = abs(float(self.r))
            self.centre = [float(self.centre[0]), float(self.centre[1])]
            self.desired_error = float(self.desired_error)

            # initialize counters
            inside = 0
            total = 0

            # set necessary values
            error = self.desired_error + 1
            theoretical_area = np.pi * self.r ** 2

            # start main loop
            while error > self.desired_error:
                # update counters
                inside, total = self.monte_carlo_2D_step(inside, total)

                # determine the stats
                area = self.get_area(self.r, inside, total)
                error = self.get_error(theoretical_area, area)
                pi = self.get_pi(self.r, area)

                # add values to stats lists
                self.errors.append(error)
                self.areas.append(area)
                self.pi.append(pi)
                self.N.append(total)

            return

        except (ValueError, TypeError) as _:
            """
            This exception is raised when one or more values
            (from r, x, y, err) are not `int` or `float`.
            
            The code will return empty stats.
            """
            print("\n  You need enter valid values (int or float) \n")
            return

        except ZeroDivisionError:
            """
            This exception is raised when the radius is zero.
            
            The code will return empty stats.
            """
            print("\n  You need enter valid radius != 0 \n")
            return


if __name__ == "__main__":
    # request inputs
    radius = input("\nPlease enter the circle radius value: ")
    centreX = input("Please enter the circle centre x coordinate: ")
    centreY = input("Please enter the circle centre y coordinate: ")
    err = input("Please enter the minimum desired error: ")

    # create the circle object
    circle = Circle(radius, [centreX, centreY], err)
    # get circle stats
    circle.get_circle_stats()

    # print some info:
    if len(circle.areas) > 0:
        print("\n  The circle area is: ", circle.areas[-1])
        print("  The calculated pi is: ", circle.pi[-1])
        print("  The error is: ", circle.errors[-1], "\n")

    # You can also make some useful plots
    # Example: ploting the pi value as a function of the number of random points
    if circle.areas != []:
        plt.plot(circle.N, circle.pi, label=r"Calculated  $\pi$")
        plt.axhline(y=np.pi, color="r", label=r"Theoretical $\pi$")
        plt.legend()
        plt.show()
        # plt.save('monte_carlo_pi.png')
        plt.close()


```

:::

## The test file

If you need some ideas related with the test file, you can see my code bellow.

:::{dropdown} See the test code

```python
# `test_circle` file content
# you can use this file by typing: $ pytest
from circle_area import Circle


def test_string():
    # should replicate this test to check if it works with other wrong variables
    r = 1
    x = 2.0
    y = "a"  # wrong value
    err = 5.0
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.areas == []


def test_list():
    # should replicate this test to check if it works with other wrong variables
    r = 1
    x = [1, 2.0]
    y = 0.0  # wrong value
    err = 5.0
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.areas == []


def test_zero_radius():
    r = 0
    x = 10
    y = 10
    err = 5.0
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.areas == []


def test_negative_radius():
    # Note that I choose to use abs(radius)
    r = -1
    x = 10
    y = 10
    err = 5.0
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err


def test_zero_centre():
    r = 1
    x = 0
    y = 0
    err = 0.1
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err


def test_non_zero_centre():
    r = 1
    x = 10
    y = 23
    err = 0.1
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err


def test_negative_centre():
    r = 1
    x = -10
    y = -23
    err = 0.1
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err


def test_mix_centre():
    r = 1
    x = 10
    y = -23
    err = 0.1
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err


def test_larger_radius():
    r = 100
    x = 0
    y = 0
    err = 0.1
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err


def test_lower_error():
    r = 1
    x = 0
    y = 0
    err = 0.001
    circle = Circle(r, [x, y], err)
    circle.get_circle_stats()
    assert circle.errors[-1] <= err
```

:::

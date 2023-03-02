# Case of study

The last session of this training will consist of the execution of a project
with the objective of putting into practice the main points presented during the
training.

The aim is to practice:

- The steps of the Software Development Life Cycle, mainly the steps of:
  - Ideation
  - Requirements
  - Development
  - Testing
- Make use of good practices:
  - virtual environment (using `conda`)
  - project layout (using `cookiecutter`)
  - code formatting (using `black`)
- Use version control collaboratively:
  - git
  - GitHub
    - branches
    - pull requests
    - issues
- Test-driven development

## The Problem

Participants must develop a code that returns the area of a circle for a
given radius.

### Ideation & Requirements

Although the problem seems simple, some requirements will be added during the
**Ideation and requirements** steps.

The objective of this exercise is to show how the solution to each problem can
vary according to the research needs and that, therefore, before starting to
write the code, it is necessary to fully understand what is being requested.

The requirements:

- The main requirement is that **no** predefined value for `pi` should be used.
- The value of `pi` (from math package, for example) can, however, be used to check the accuracy of the result.
- The result can have a maximum error of 0.01% compared to standard methods (using `pi` from math package and `pi*r**2`)

Some ideas to brainstorm:

- Create a method to return the value of `pi`.
- Create a method to return the error.
  - better: make the program stop only when it reaches the desired error
- Generalize the code to allow the inclusion of the volume calculation (using the same method in 3 dimensions)
- Generalize the code to allow the inclusion of other areas related to circle, such as cylinder and cone.
- Produce some outputs plots.

*Please note that these ideas are just a starting point - participants will be free to design their project, as long as they respect the main idea and requirements.*

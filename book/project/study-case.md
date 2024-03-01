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
  - environment (using `conda`)
  - project layout
  - code formatting (using `black` and `flake8`)
- Use version control collaboratively:
  - git
  - GitHub
    - branches
    - pull requests
    - issues
- Test-driven development

## The Hypotenuse Problem

Calculating the hypotenuse

$$ c = \sqrt{a^2 + b^2} $$

General Design

- 1 squared function
- 1 sum function
- 1 square root function
- 1 hypotenuse function that uses the functions above

## Project Workflow

Ideally, this is a task to be done in pairs.

1. Install Git, Anaconda, VScode
2. Create a GitHub repository + Licence + .gitignore + Readme
3. Setup GH Action for testing (Python Application)
4. Clone GH repository in local machines
5. Brainstorm to define all necessary tasks
6. List all scenarios/tests
7. Create project structure (source (name of the package) and test folders)
8. Setup the environment
9. Develop the test unit (start with `test_`)
10. Develop the main code
11. Lint code and tests
12. Develop some documentation (you can use `autoDocstring - Python Docstring Generator on VS Code`)
13. Update the GitHub
14. Check the action: is your code linted, is your code passing the tests?

*Please note that these ideas are just a starting point - participants will be free to design their project, as long as they respect the main idea and requirements.*

## Solution

The [`swd3-demo` repository](https://github.com/ARCTraining/swd3-demo) is a demonstration of how this project can be solved.
It also includes some additional features:

- Source Code
- Test with Pytest Framework
- Documentation website with Sphinx Framework
- Installation file for local install
- GitHub Actions for Linting, testing, and create documentation
- Release

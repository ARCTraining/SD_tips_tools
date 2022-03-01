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

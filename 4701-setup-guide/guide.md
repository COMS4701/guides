# Setting up 4701 Programming Environment

### The Basics

All programming assignments will be done in Python

- Recommended setup:
    - A code / text editor of your choice (vim, emacs, vscode, etc)
    - Or… a full-blown IDE (PyCharm etc) if you can get it to work with the rest of the setup (there should be resources online specific to the IDEs of your choice)
    - Python 3.9 and running programs in the terminal

### Virtual Environment Management

Virtual environments isolate package installs for projects

We recommend that you use virtual environments

- So that our package versions don’t mess with what you have in your local setup
- To be 100% sure your submission will run without problems on our grading machines

We recommend Python’s native `virtualenv`

- But feel free to use `conda` if you already use it for your virtual environment management

### Setting up a Virtual Environment

Sample session of creating, activating, and deactivating a virtual environment:

```bash
~/Workspace/4701 > python -m venv .venv           # create a venv in .venv/
                                                                                   
~/Workspace/4701 > ls -a                          # .venv can be found 
.     ..    .venv

~/Workspace/4701 > which python                   # venv is not activated yet
/Users/chrisyoon/miniforge_x86_64/bin/python      # using host's python
                                                                                   
~/Workspace/4701 > source .venv/bin/activate      # activate our venv
                                                                              
~/Workspace/4701 > which python                   
/Users/chrisyoon/Workspace/4701/.venv/bin/python  # now using venv's python
                                                                             
~/Workspace/4701 > deactivate                     # do this to deactivate venv
                                                                                  
~/Workspace/4701 > which python                   
/Users/chrisyoon/miniforge_x86_64/bin/python      # now back to host's python 
```

Sample session of installing packages in a virtual environment:

```bash
~/Workspace/4701 > source .venv/bin/activate      # make sure venv is activated
                                                                              
~/Workspace/4701 > pip install --upgrade pip
Requirement already satisfied: pip in ./.venv/lib/python3.9/....
Collecting pip
  Using cached pip-22.3.1-py3-none-any.whl (2.1 MB)
Installing collected packages: pip
  Attempting uninstall: pip
    Found existing installation: pip 21.1.3
    Uninstalling pip-21.1.3:
      Successfully uninstalled pip-21.1.3
Successfully installed pip-22.3.1
                                                                            
~/Workspace/4701 > pip install numpy
Collecting numpy
  Using cached numpy-1.24.1-cp39-cp39-macosx_10_9_x86_64.whl (19.8 MB)
Installing collected packages: numpy
Successfully installed numpy-1.24.1
                                                                             
~/Workspace/4701 > python
Python 3.9.6 | packaged by conda-forge | ....
[Clang 11.1.0 ] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> import numpy
>>>
```

### Using Poetry for Package Management

To make sure we are all using the same packages and the same versions, we will be distributing programming homework as `poetry` projects:

![poerty1.png](Setting%20up%204701%20Programming%20Environment%20eb40f985970149c3bc727bc90bf7dec7/Screen_Shot_2023-01-26_at_12.44.48_PM.png)

![poetry2.png](Setting%20up%204701%20Programming%20Environment%20eb40f985970149c3bc727bc90bf7dec7/Screen_Shot_2023-01-26_at_12.45.07_PM.png)

As the description above says, `Poetry` is a very popular packaging and dependency management system for Python projects. 

Now, we’ll go through how to set up 4701 programming homework projects:

```bash
~/Workspace/4701/hw1-prog > ls
README.md      hw1            poetry.lock    pyproject.toml worlds
```

First, let’s create a virtual environment for the project (you only need to do this once, for every programming homework)

```bash
~/Workspace/4701/hw1-prog > python -m venv .venv
                                                                                                                                                                             base
~/Workspace/4701/hw1-prog > source .venv/bin/activate
```

`Poetry` stores all the project configurations (package dependencies and their versions, most importantly) in the `./pyptoject.toml` file. See `[tool.poetry.dependencies]`

```bash
~/Workspace/4701/hw1-prog > cat pyproject.toml
[tool.poetry]
name = "hw1"
version = "0.1.0"
description = ""
authors = ["Your Name <you@example.com>"]
readme = "README.md"
packages = [{include = "hw1"}]

[tool.poetry.dependencies]
python = "^3.9"
numpy = "^1.24.1"
black = "^22.12.0"
matplotlib = "^3.6.3"

[build-system]
requires = ["poetry-core"]
build-backend = "poetry.core.masonry.api"

[tool.poetry.scripts]
main = "hw1.main:main"
```

Now, to install the project and the dependency, just do:

```bash
~/Workspace/4701/hw1-prog > poetry install
...
Package operations: 18 installs, 0 updates, 0 removals

  • Installing numpy (1.24.1)
  • Installing six (1.16.0)
  • Installing click (8.1.3)
  • Installing contourpy (1.0.7)
  • Installing cycler (0.11.0)
  • Installing fonttools (4.38.0)
  • Installing kiwisolver (1.4.4)
  • Installing mypy-extensions (0.4.3)
  • Installing packaging (23.0)
  • Installing pathspec (0.11.0)
  • Installing pillow (9.4.0)
  • Installing platformdirs (2.6.2)
  • Installing pyparsing (3.0.9)
  • Installing python-dateutil (2.8.2)
  • Installing tomli (2.0.1)
  • Installing typing-extensions (4.4.0)
  • Installing black (22.12.0)
  • Installing matplotlib (3.6.3)

Installing the current project: hw1 (0.1.0)
```

And you should be good to go! 

While you can run python files like you would usually do in the terminal:

```bash
python hw1/main.py [params]
```

You can also use the poetry scripts we have configured (see `[tool.poetry.scripts]`):

```bash
poetry run main [params]
```

We will sometimes also provide unit-test like testcases in a `test/` directory of the project. You can run all of the tests via:

```bash
poetry run test
```

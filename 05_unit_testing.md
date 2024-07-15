# Unit testing tutorial

## 1. Introduction

We will be using the [unittest](https://docs.python.org/3/library/unittest.html) module for unit testing. The unittest module provides a rich set of tools for constructing and running tests.

## 2. Writing the tests

The tests should be written in the following manner:

* **Test file** - Each test file should be named after the file that is being tested. The test file should be placed in the same directory as the file that is being tested. The test file should be named in the following manner: `test_<file_name>.py`.

* **Test class** - Each test class should be named after the class that is being tested. The test class should be placed in the same directory as the file that is being tested. The test class should be named in the following manner: `Test<ClassName>`.

* **Test function** - Each test function should be named after the function that is being tested. The test function should be placed in the same directory as the file that is being tested. The test function should be named in the following manner: `test_<function_name>`.

### 2.1. Example

Let's say we have a file called `my_module.py` with the following content:

```python

def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

```

We want to test the `add` and `subtract` functions. We will create a folder `tests` on the root of the project which contains a file called `test_my_module.py` with the following content:

```python

import unittest
from my_module import add, subtract

class TestMyModule(unittest.TestCase):

    def test_add(self):
        self.assertEqual(add(1, 2), 3)
        self.assertEqual(add(1, -1), 0)
        self.assertEqual(add(1, 0), 1)

    def test_subtract(self):
        self.assertEqual(subtract(1, 2), -1)
        self.assertEqual(subtract(1, -1), 2)
        self.assertEqual(subtract(1, 0), 1)

```

In order to run the tests, you need to run the following command:

```bash

python -m unittest discover -s tests -p "test_*.py"

```

The output should be similar to the following:

```bash
$ python -m unittest discover -s tests -p "test_*.py"

----------------------------------------------------------------------
Ran 2 tests in 0.000s

OK

```

You can also simplify the command and use `pytest`:
```bash
$ pytest <directory_to_tests>
```

Some more examples can be found in the library consmodel [here](https://github.com/blazdob/consmodel).

## 3. Running the tests

### 3.1. VSCODE

In order to run the tests in vscode, you need to install the [Python Test Explorer for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=LittleFoxTeam.vscode-python-test-adapter) extension.

You should have Testing tab in the left side of the screen. If you don't have it, you can open it by pressing `Ctrl+Shift+P` and typing `Python: Show Test Output`.

In order to run the tests, you need to click on the `Run all tests` button. The shoul be configured to run all the tests in the project.


### 3.2. Command line

In order to run the tests from the command line, you need to run the following command:

```bash
python -m unittest discover -s <path_to_tests_directory> -p "test_*.py"
```


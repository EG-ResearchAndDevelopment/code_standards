# Code Formatting

## 1. General Formatting

Initially this document was created for the **Python** programming language. It describes the coding style that we use in our projects. The coding style is based on the [PEP-8](https://www.python.org/dev/peps/pep-0008/) coding style guide. The document is divided into two parts. The first part describes the code formatting tools that we use and the second part describes the coding style itself.

Python is the main dynamic language used at EG R&D. This style guide is a list of dos and don'ts for Python programs.

### 2. CODE FORMATTER of choice

Code formatting is the process of transforming source code into a more readable form. It is a common practice to format code before committing it to a shared repository. This ensures that all team members are using the same code style and makes it easier to spot any changes made to the code.

We are using the **YAPF** code formatter for Python. YAPF by default uses PEP-8 code style. In order to use it, you need to install it first:

```bash
pip install yapf
```
As well as using the extension for your IDE of choice.

In order to use the YAPF formatter, you need to run the following command in the root directory of your project:

```bash
yapf -i -r .
```
This command will run the YAPF formatter recursively on all files in the current directory and its subdirectories.
This commit should be done as often as possible, preferably after every change to the code.

### **This formatter is only a helpfull tool, it does not replace the need for a good coding style.**

### 3. Imports

Imports should be grouped in the following order:

1. Standard library imports.
2. Related third party imports.
3. Local application/library specific imports.

Import each module using the full pathname location of the module.
    
    ```python
    import os
    import sys

    from foo.bar import baz
    from foo.bar import Quux

    from foo.bar.yourmodule import yourfunction
    ```

### 4. Line length

Limit all lines to a maximum of 100 characters.

The following examptions are allowed:
1. Lines where exceeding the limit improves readability and does not hide any information.
2. Long URLs.
3. Long paths.

e.g.
    
    ```python
    # No: Aligned with opening delimiter.
    foo = long_function_name(var_one, var_two,
                             var_three, var_four)
                            
    # Yes: Add 4 spaces (an extra level of indentation) to distinguish arguments from the rest.
    def long_function_name(
            var_one,
            var_two,
            var_three,
            var_four
        ):
        print(var_one)

### 5. Indentation

Use 4 spaces per indentation level. (This is fixed in YAPF)

### 6. Definitions

#### 6.1. Variables definition

Variables definitions should have the following format:

    ```python
    # No:
    a, b, c = 1, 2, 3

    # Yes:
    a = 1
    b = 2
    c = 3
    ```

#### 6.2 Function definition

Function definitions should have the following format:

    ```python
    def function_name(arg1: int, arg2: str,) -> None:
        """One-line description of what this function does.

        Longer description of the function.

        Args:
        ----------
            arg1: int
                Description of arg1.
            arg2: str:
                Description of arg2.

        Returns:
        ----------
            Description of return value.
        """
        # ...
        return None
    ```

When the function is a `__init__` then the `Args:` should be renamed to `Attributes:`.

**Be careful of the last comma in the argument list. as it is required for YAPF to work properly.**
If the function has many arguments, you can split the arguments into multiple lines. In this case, the closing parenthesis should be on a separate line.

    ```python
    def function_name(
        arg1: int,
        arg2: str,
        arg3: float,
        arg4: bool,
    ) -> None:
    """
    ....
    """
        # ...
        return None
    ```

#### 6.3. Class definition

All classes should have the following format:

    ```python
    class ClassName:
        """One-line description of what this class does.

        Longer description of the class.
        """

        def __init__(self, arg1: int, arg2: str,) -> None:
            """
            Attributes:
            ----------
                arg1: int
                    Description of arg1.
                arg2: str
                    Description of arg2.
            """
            # ...

        @setter
        def attr1(self, value: int) -> None:
            # ...
        
        @getter
        def attr1(self) -> int:
            # ...
            return None
        
        @setter
        def attr2(self, value: str) -> None:
            # ...
        
        @getter
        def attr2(self) -> str:
            # ...
            return None
        
        def method_name(self, arg1: int, arg2: str,) -> None:
            """One-line description of what this function does.

            Longer description of the function.

            Args:
            ----------
                arg1: int
                    Description of arg1.
                arg2: str
                    Description of arg2.

            Returns:
            ----------
                Description of return value.
            """
            # ...

        @classmethod
        def class_method_name(cls, arg1: int, arg2: str,) -> str:
            """One-line description of what this function does.

            Longer description of the function.

            Args:
            ----------
                arg1: Description of arg1.
                arg2: Description of arg2.

            Returns:
            ----------
                Description of return value.
            """
            # ...
            return "None"
    ```


### 7. Type annotations

You can annotate Python code with type hints according to **PEP-484**, and type-check the code at build time with a type checking tool like pytype.

We strongly encourage the use of type annotations. They are a great way to document the expected types of variables, arguments, and return values. They can also help you find bugs at compile time. We recommend using type annotations for all public APIs and for functions or methods that are complex enough to warrant type annotations.

While type annotations are a great tool, they are not required 100% of the time. If you are writing a simple function that doesn't require type annotations, you don't need to add them (but you still should). 

**Output type annotation is not required but is recommended.**

### 8. Comments

#### 8.1. Function comments

All functions should have a comment that describes what the function does. The comment should be placed right below the function definition and should have the following format:

    ```python
    def function_name(arg1: int, arg2: str,) -> None:
        """One-line description of what this function does.

        Longer description of the function.

        Args:
        ----------
            arg1: Description of arg1.
            arg2: Description of arg2.

        Returns:
        ----------
            Description of return value.
        """
        # ...
        return None
    ```

#### 8.2. Line comments

Line comments should be used sparingly. They should be used only when it is not possible to describe the code with a function comment or with the code naming convention itself. Line comments should have the following format:

    ```python
    # This is a comment.
    ```

If they are longer they should be split into multiple lines:

    ```python
    # This is a comment that is too long to fit on a single line.
    # so it has been split into multiple lines.
    ```

### 8.3 Return statements

If a function returns a value, it should have a return statement. If the function does not return a value, it should have a `return None` statement at the end. In this case, the function should have a comment that describes what the function does.

    ```python
    def function_name(arg1: int, arg2: str,) -> None:
        """One-line description of what this function does.

        Longer description of the function.

        Args:
        ----------
            arg1: Description of arg1.
            arg2: Description of arg2.
        """
        # ...
        return None
    ```

### 9. True and False evaluation

Do not use the `==` and `!=` operators to compare a value to `True` or `False`.

    ```python
    # No:
    if greeting == True:
        # ...
    
    # Yes:
    if greeting:
        # ...
    
    # No:
    if greeting != True:
        # ...
    
    # Yes:
    if not greeting:
        # ...
    ```

### 10. Parentheses

Do not use parentheses around the condition of an `if` statement.

    ```python
    # No:
    if (x > 0):
        # ...
    
    # Yes:
    if x > 0:
        # ...
    ```
Do not use parantheses around return values.

    ```python
    # Yes:
    return x
    return x, y
    return (x, y)

    # No:
    return (x)
    ```

### 11. Whitespace

**White spaces should automatically be handled by YAPF.**

#### 11.1. Blank lines

Separate top-level function or class definition with two blank lines. And the rest of the code with one blank line.

    ```python

    #START OF THE FILE
    import os
    import sys


    def function1():
        # ...
        return None

    def function2():
        # ...
        return None
    ```

#### 11.2. Blank spaces

Do not use blank spaces around the following:

1. Immediately inside parentheses, brackets or braces.
2. Immediately before a comma, semicolon, or colon.
3. Immediately before the open parenthesis that starts the argument list of a function call.
4. Immediately before the open parenthesis that starts an indexing or slicing.
5. Immediately before the open parenthesis that starts a tuple.
6. Immediately before the open parenthesis that starts a dictionary.
7. Immediately before the open parenthesis that starts an argument list, indexing, slicing, or tuple.


    ```python
    # No:
    spam( ham[ 1 ], { eggs: 2 } )

    # Yes:
    spam(ham[1], {eggs: 2})
    ```

Surround binary operators with a single space on either side for assignment (`=`), comparisons (`==, <, >, !=, <>, <=, >=, in, not in, is, is not`), and Booleans (`and, or, not`). Use your better judgment for the insertion of spaces around arithmetic operators (`+, -, *, /, //, %, **, @`). **We prefer to put a single space around these operators as well.**


    ```python
    # No:
    x=y+1

    # Yes:
    x = y + 1
    ```

There should be no trailing whitespace at the end of a line. **This should be automatically handled by YAPF.**


### 12. Strings

#### 12.1. Single quotes

Use single quotes (`'`) for strings.

    ```python
    # No:
    string = "This is a string."

    # Yes:
    string = 'This is a string.'
    ```

#### 12.2. String concatenation

Use the `+` operator for string concatenation.

    ```python
    # No:
    string = 'This is a string.' 'This is another string.'

    # Yes:
    string = 'This is a string.' + 'This is another string.'
    ```

#### 12.3. String formatting

Use the `f-string` for string formatting.

    ```python
    Yes: x = f'name: {name}; score: {n}'
         x = '{}, {}'.format(first, second)

     
    No: x = first + ', ' + second
        x = 'name: ' + name + '; score: ' + str(n)
         x = '%s, %s!' % (imperative, expletive)
         x = 'name: %s; score: %d' % (name, n)
         x = 'name: %(name)s; score: %(score)d' % {'name':name, 'score':n}
         x = a + b

    ```

### TODO - Any more formatting questions or rules that you would like to add?
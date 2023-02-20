---
title: "Code Quality"
teaching: 15
exercises: 25
questions:
- "How can I make my programs more readable?"
- "How can programs check their own operation?"
- "How can I document my code?"
- "How can I make my code more reproducibility?"

objectives:
- "Use Python community coding standards (PEP-8)."
- "Use assertions to check for internal errors"
- "Use docstrings to provide online help"
- "Print the version number of imported libraries"

keypoints:
- "Follow standard Python style in your code."
- "Use assertions to check for internal errors"
- "Use docstrings to provide online help."
- "Use `__version__` to increase code reproducibility."
---

## Follow standard Python style in your code.

Coding style helps us to understand the code better. It helps to maintain and change the code.
Python relies strongly on coding style, as we may notice by the indentation we apply to lines to define different blocks of code.
Python proposes a standard style through one of its first Python Enhancement Proposals (PEP), [PEP8](https://www.python.org/dev/peps/pep-0008), and highlights the importance of readability in the [Zen of Python](https://www.python.org/dev/peps/pep-0020).

We may highlight some points:
*   use clear, meaningful variable names
*   use white-space, *not* tabs, to indent lines
*   consistency is key

Adhering to PEP8 makes it easier for other Python developers to read and understand your code,
and to understand what their contributions should look like.
The [PEP8 application and Python library](https://pypi.python.org/pypi/pep8)
can check your code for compliance with PEP8.

## Use assertions to check for internal errors.

Assertions are a simple, but powerful method for making sure that the context in which your code is executing is as you expect.

~~~
def calc_bulk_density(mass, volume):  
    assert volume > 0, "Volume is less than zero (unphysical)"
    return mass / volume
~~~
{: .python}

If the assertion is `False`, the Python interpreter raises an `AssertionError` runtime exception. The source code for the expression that failed will be displayed as part of the error message. To ignore assertions in your code run the interpreter with the '-O' (optimize) switch. Assertions should contain only simple checks and never change the state of the program. For example, an assertion should never contain an assignment.

## Use docstrings to provide help.

*   If the first thing in a function is a character string
    that is not assigned to a variable,
    Python attaches it to the function as the help documentation.
*   Called a *docstring* (short for "documentation string").

~~~
def calc_bulk_density(mass, volume): 
    "Return dry bulk density = powder mass / powder volume."
    assert volume > 0
    return mass / volume
~~~
{: .python}
~~~
Help on function calc_bulk_density in module __main__:

calc_bulk_density(mass, volume)
    Return dry bulk density = powder mass / powder volume.
~~~
{: .output}

## Use `__version__` to increase code reproducibility


*   Code reproducibility (running the same code twice to give the same output) is more complex and difficult than you might think.
*   One straight-forward thing you can do is print the version number for each package you import using `print(packagename.__version__)`.

> ## Multiline Strings
>
> Often use *multiline strings* for documentation.
> These start and end with three quote characters (either single or double)
> and end with three matching characters.
>
> ~~~
> """This string spans
> multiple lines.
>
> Blank lines are allowed."""
> ~~~
> {: .python}
{: .callout}

> ## What Will Be Shown?
>
> Highlight the lines in the code below that will be available as online help.
> Are there lines that should be made available, but won't be?
> Will any lines produce a syntax error or a runtime error?
>
> ~~~
> "Find maximum edit distance between multiple sequences."
> # This finds the maximum distance between all sequences.
>
> def overall_max(sequences):
>     '''Determine overall maximum edit distance.'''
>
>     highest = 0
>     for left in sequences:
>         for right in sequences:
>             '''Avoid checking sequence against itself.'''
>             if left != right:
>                 this = edit_distance(left, right)
>                 highest = max(highest, this)
>
>     # Report.
>     return highest
> ~~~
> {: .python}
{: .challenge}

> ## Document This
>
> Turn the comment on the following function into a docstring
> and check that `help` displays it properly.
>
> ~~~
> def middle(a, b, c):
>     # Return the middle value of three.
>     # Assumes the values can actually be compared.
>     values = [a, b, c]
>     values.sort()
>     return values[1]
> ~~~
> {: .python}
> > ## Solution
> >
> > ~~~
> > def middle(a, b, c):
> >     '''Return the middle value of three.
> >     Assumes the values can actually be compared.'''
> >     values = [a, b, c]
> >     values.sort()
> >     return values[1]
> > ~~~
> > {: .python}
> {: .solution}
{: .challenge}

> ## Improve the Code Quality I
>
> 1. Read the [Code Quality criteria](../files/CodeQuality.pdf) for the course assessment.
> 2. Read the code below and predict what it does
> 3. Run the code and inspect the output
> 3. Refactor the program to improve the Code Quality. There are six edits (or more!) that can be made.
>    Remember to run the program after each edit to ensure its behavior hasn't changed.
> 4. Compare your rewrite with your neighbor's.
>    What did you do the same?
>    What did you do differently, and why?
>
> ~~~
> import math
> import numpy
> 
> spring_constant = [3.1,7.2,2.7]
> for x,y in enumerate(spring_constant):
>                 mass = 10
>                 k=y
>                 
>                 print("The angular frqency is", numpy.sqrt(k/mass))
> ~~~
> {: .python}
>
> > ## Hints
> >
> > There are a number of ways to improve this code. Some hints are given below, and will be discussed in more
> > detail in class.
> > 1. Mis-spelling
> > 2. Redundant code
> > 3. Inconsistent whitespace
> > 4. Unhelpful variable names
> > 5. Repeated variable assignment
> > 6. Lack of documentation
> > 7. Lack of reproducibility
> {: .solution}
{: .challenge}

> ## Improve the Code Quality II
>
> 1. Read this short program and try to predict what it does.
> 2. Run it: how accurate was your prediction?
> 3. Refactor the program to make it more readable.
>    Remember to run it after each change to ensure its behavior hasn't changed.
> 4. Compare your rewrite with your neighbor's.
>    What did you do the same?
>    What did you do differently, and why?
>
> ~~~
> n = 10
> s = 'et cetera'
> print(s)
> i = 0
> while i < n:
>     # print('at', j)
>     new = ''
>     for j in range(len(s)):
>         left = j-1
>         right = (j+1)%len(s)
>         if s[left]==s[right]: new += '-'
>         else: new += '*'
>     s=''.join(new)
>     print(s)
>     i += 1
> ~~~
> {: .python}
>
> > ## Solution
> >
> > Here's one solution.
> >
> > ~~~
> > def string_machine(input_string, iterations):
> >     """
> >     Takes input_string and generates a new string with -'s and *'s
> >     corresponding to characters that have identical adjacent characters
> >     or not, respectively.  Iterates through this procedure with the resultant
> >     strings for the supplied number of iterations.
> >     """
> >     print(input_string)
> >     old = input_string
> >     for i in range(iterations):
> >         new = ''
> >         # iterate through characters in previous string
> >         for j in range(len(input_string)):
> >             left = j-1
> >             right = (j+1)%len(input_string) # ensure right index wraps around
> >             if old[left]==old[right]:
> >                 new += '-'
> >             else:
> >                 new += '*'
> >         print(new)
> >         # store new string as old
> >         old = new
> >
> > string_machine('et cetera', 10)
> > ~~~
> > {: .python}
> > 
> > ~~~
> > et cetera
> > *****-***
> > ----*-*--
> > ---*---*-
> > --*-*-*-*
> > **-------
> > ***-----*
> > --**---**
> > *****-***
> > ----*-*--
> > ---*---*-
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

![](https://i.imgur.com/iywjz8s.png)

# Collaborative Document

2022-05-30 Data Carpentry with Python (day 2)

Welcome to The Workshop Collaborative Document.

This Document is synchronized as you type, so that everyone viewing this page sees the same text. This allows you to collaborate seamlessly on documents.

## 👮Code of Conduct

Participants are expected to follow these guidelines:
* Use welcoming and inclusive language.
* Be respectful of different viewpoints and experiences.
* Gracefully accept constructive criticism.
* Focus on what is best for the community.
* Show courtesy and respect towards other community members.

## ⚖️ License

All content is publicly available under the Creative Commons Attribution License: [creativecommons.org/licenses/by/4.0/](https://creativecommons.org/licenses/by/4.0/).

## 🙋Getting help

To ask a question, type `/hand` in the chat window.

To get help, type `/help` in the chat window.

You can ask questions in the document or chat window and helpers will try to help you.

## 🖥 Workshop information

:computer:[Workshop website](https://esciencecenter-digital-skills.github.io/2022-05-30-dc-socsci-python-nlesc/)

🛠 [Setup](https://esciencecenter-digital-skills.github.io/2022-05-30-dc-socsci-python-nlesc/#setup)

:arrow_down: Download the following files and place them in a single, easily findable folder:
- [SAFI_clean.csv](https://ndownloader.figshare.com/files/11492171)
- [SAFI_messy.xlsx](https://ndownloader.figshare.com/files/11502824)
- [SAFI_dates.xlsx](https://ndownloader.figshare.com/files/11502827)
- [SAFI_openrefine.csv](https://ndownloader.figshare.com/files/11502815)


## 🗓️ Agenda
| Time  | Topic                                    |
|------:|:-----------------------------------------|
| 9:00  | Welcome, recap of day 1, code of conduct |
| 9:15  | Python basics                            |
| 10:15 | Coffee break                             |
| 10:30 | Python control structures                |
| 11:30 | Coffee break                             |
| 11:45	| Creating reusable code                   |
| 12:45 | Day 2 wrap-up                            |
| 13:00 | END                                      |


## 🔧 Exercises

### Exercise: Arithmetic and printing
Create a new cell and paste the code from the example into it:
```python=
print("a =", a, "and b =", b)
print(a + 2*b)
print(a + (2*b))
print((a + b)*2)
```
1. Remove all of the calls to the print function so you only have the expressions that were to be printed and run the code. What is returned?
2. Now remove all but the first line (with the 4 items in it) and run the cell again. How does this output differ from when we used the print function?

Bonus if you are done early:
* Practice assigning values to variables using as many different operators as you can think of.
* Create some expressions to be evaluated using parentheses to enforce the order of mathematical operations that you require

### Exercise: List indexing
1. Create a cell with the code below.
```python=
num_list = [4,5,6,11]
```
2. Select the 1st element from this list. (Your code should return `4`)
3. Select the last element from this list. (Your code should return `11`)
4. Make a new list with the second and fourth element in this list. (Your code should return `[5,11]`)

### Exercise: if-statements

1. Start with the following code:
```python=
apple_cost = 0.5
bread_cost = 2.5
money = 2
```
2. Write an `if`-statement, replacing the ____ in the code below, that checks whether you can buy a bread with your money:
```python=
if ___
    print("I can buy bread!")
```

3. Add an `elif` to your statement, where you check if you can buy an apple instead.
```python=
elif _________
    print("At least I can buy an apple!")
```

4. Bonus: write a final `else` for the tragic scenario where you can buy neither bread nor apple.

### Exercise: for-loop
Suppose that we have a string containing a set of 4 different types of values separated by , like this:
```python=
variablelist = "01/01/2010,34.5,Yellow,True"
```
Research the `split()` method and write a for-loop that prints each of the 4 components of `variablelist`

### Exercise: Creating functions
1. Write a function definition to calculate the volume of a cuboid. The function will use three parameters h, w and l and return the volume.
2. Supposing that in addition to the volume I also wanted to calculate the surface area and the sum of all of the edges. Would I (or should I) have three separate functions or could I write a single function to provide all three values together?


## 🧠 Collaborative Notes

### Questions from day 1:
1. Why is OpenRefine used, should we use it instead of R/Python, and if so, in what situation?
2. The faceting function seems like a nice tool for data cleaning. Not clear to me is what to do with sorted/filtered data- is this to select a subset of data for analysis?
3. Is there a guide for when to use "custom text facet" and when not?

Answers:
1. OpenRefine is particularly interesting if you are not familiar (enough) with R or Python to do data cleaning in those languages.
2. Not really for analysis, but for data cleaning it is useful to get insight in your data, sorting and filtering helps with that. We will see how to do selection and filtering in Python for the analysis part
3. If your faceting doesn't fit to the predefined facets, you can use the custom one.

### Introduction to Python

Python’s main advantages:

* Open source software, supported by Python Software Foundation
* Available on all major platforms (Windows, macOS, Linux)
* Easy to learn with a straightforward, object-oriented style
* Well-structured, which aids readability
* Supported by a large community

Start jupyter lab by either:
* using anaconda navigator (windows, mac)
* typing `jupyter lab` in your terminal or anaconda prompt

Create a new notebook and rename it to something like `python_day1.ipynb`. Everything you write will be (automatically) stored in the notebook. Notebooks are not the only way to write python codefor i in variablelist.split(","):
    print(i), but it useful for learning.

Notebooks can have different types of cells:
* code (python, in our case). For example, type:
```python=
a = 3
b = 5
a * b
```
Use SHIFT+Enter to run the code in your current cell. If you hit `ESC` your cell is unactive and there is a bunch of shortcuts to manage cells (d for delete, a for add, etc).

* Markdown: (same as in this HackMD document) to write formatted text. If you run the cell, the data will

if you type:
```python=
c = 5
d = 7
```
We see no output. But something happened: a new variable is assigned the value 7. but if we put in our cell:
```python=
d
```
it shows the value of d.

But if we type:
```python=
a
b
c
d
```
it only gives the output of the last line.

If we want to output the values explicitely, need the `print` command:
```python=
print(a)
print(b)
print(c)
print(d)
```

We can also assign a string to a variable (different type of data than number):
```python=
e = "Hello world"

print(e)
```

We can check the type of a variable:
```python=
type(a)
```

`a` is an integer, `e` a string. We also have *floats* for decimal numbers:
```python=
pi = 3.14
type(pi)
```

We can combine them in operations, this will return a float
```python=
print(a*pi) # multiplication
print(a+b) # Addition
print(a/b) # Division
```
Note that text preceded with `#` are comments and are not run as part of the code.

If we try to add a string to a number we get an error:
```python=
print(e+b)
```

But we can use the `+` operator also for strings:
```python=
f = "Greetings. "
print(e+f)
```

Question: when do you add spaces around the operators? Answer: it doesn't matter for the execution of the code, but there are style guides for this (see resources).

We can convert the type of a variable:
```python=
print(e + str(b))
```

We have seen several built-in function, such as `str` and `print`. If we type the fucntion and hit SHIFT+tab, it gives us the *docstring*, so information on what the function does and what are the arguments.
Or run the `help` command to print out the docstring:
```python=
help(print)
```

We have some functions specifically for strings. To list all operations possible on the data type that we have (string, in this case):
```python=
dir(e)
```
For example, to lowercase a string:
```python=
e.lower()
```
Similar, `e.upper()` gives uppercase.

Question: do we first need to load a package to use these functions? No, we used built-in functions so far, and the `upper` and `lower` functions are specific to the (built-in) string data type.

To check whether string is lower case:
```python=
e.islower()
```

This gives `False`, which is a *boolean*  data type.

We can concatenate functions:
```python=
e.lower().islower()
```
Oother way around gives an error, because `e.lower()` gives an boolean. To fix that:
```python=
str(e.islower()).lower()
```

To structure our data, we will use a list:
```python=
mylist = [1, 2, 3, 6, 9]
print(mylist)
```

To take the first element of our list, note that indices in python start at 0. So to take the first element:
```python=
mylist[0]
```

Can also start indexing in reverse, to take the last element:
```python=
mylist[-1]
```

to make a list with the second and fourth element:
```python=
[mylist[1], mylist[3]]
```

If we want to avoid repetition, we can also use a trick called *list comprehension*:
```python=
[mylist[i] for i in [1,3]]
```

For R-users: Python lists are comparable to R lists, not to R vectors. They can contain all sorts of things, even lists:
```python=
[mylist, [mylist], mylist[3]]
```

Q: can we do `mylist[1::2]`? This gives the same answer but does something different: it takes every uneven element from the list.

We can use the `range` function to create a list with a range of numbers:
```python=
mylist = list(range(10))
```
this list starts at 0 and ends at 9. Then we can take elements starting at the first item, with steps of 2:
```python=
mylist[1::2]
```

We can also give a start number to `range`:
```python=
list(range(2, 10))
```

And we can give it a step size:
```python=
list(range(1, 15, 3))
```
 Q: this is difficult to read, why are they just seperated by comma? We can understand this from the documentation, run `help(range)`. Unfortunatly, they are not named keywords (as we have in some other functions)


### Control structures
#### If statements
We can use a `if` statement to check if a condition is true:
```python=
if a > 1:
    print("The value is larger than 1!")
```
Note that `a > 1` returns a boolean.

We can extend the statement with additional conditions:
```python=
if a < 1:
    print("The value is smaller than 1!")
elif a > 1: # Only checked if the first "if" gives false
    print("the value is larger than 1")
```

Now it won't do anything if `a` is equal to one. We can also use the `<=` operator to check "smaller or equal to".

We can add a 'default' option, where you get to if all if / elif statements are not true:
```python=
if a < 1:
    print("The value is smaller than 1!")
elif a > 1: # Only checked if the first "if" gives false
    print("the value is larger than 1")
else:
    print("a is probably 1")
```

Note that `else` does *not* need a condition (it will give a syntax error if you try).

#### for loops
Suppose we want to multiply every item of our list with 4:
```python=
for i in mylist:
    print("My i is ", i, "and times 4 this is", i * 4)
```

We can also use *list comprehension*, to put all items in a new list:
```python=
mylist_4 = [i*4 for i in mylist]
print(mylist_4)
```

Another string function we can use to create a list is `split`:
```python=
e.split()
```

Note that for strings, we can use both single quotes or double quotes.

Solution to the exercise:
```python=
variablelist = "01/01/2010,34.5,Yellow,True"
items = variablelist.split(",")
for i in items:
    print(i)
```

We can use the function `enumerate` to also get the index of your item:
```python=
for i, item in enumerate(items):
    print(i)
```

Q: is the name `items` standard? A: the name of the variable we can choose ourselves. Note that the variable is kept after the loop.

### Creating reusable code
Two things you can do to make your code reusable:
1. Writing your own functions
2. Using functions that others have written (thus: importing libraries)

#### Functions
You already know functions like `print()`. This is a so-called built-in function, which exists in your environment when you run python.
You can write your own functions, not just because you want to reuse the code, but it also increases the readability of your code. It is a good practice.

You can also include input parameters in your function, so you can reuse the function in different ways.

```python=
items_owned = "bicycle;television;solar_panel;table"
```
We are going to create a function that splits the items by the semicolon and counts them.
This function includes a comment that describes what the function does (a docstring).
```python=
def get_item_count(items_str, sep):
    """
    This function counts the number of items in a string.
    """
    items_list = items_str.split(sep)
    num_items = len(items_list)
    return num_items
```
![](https://i.imgur.com/Vd9g06Q.png)

Now we want to use the function:
```python=
get_item_count(items_owned, ";")
```
This should return 4. We can asign this to a new variable:
```python=
number_of_items = get_item_count(items_owned, ";")
```
Q: Can you use the `print()` statement inside the function?
A: `print()` will not return the value, just print the output. This way you can not use the output and assign it to a new variable.

```python=
get_item_count(items_owned)
```
this gives an error, because the separator argument is missing. We can however use defaults for arguments, so we can leave them out when calling the function.
```python=
def get_item_count(items_str, sep=";"):
    """
    This function counts the number of items in a string.
    """
    items_list = items_str.split(sep)
    num_items = len(items_list)
    return num_items
```
Now this should work, because `sep` has a default:
```python=
get_item_count(items_owned)
```
We can still use the argument though!

```python=
get_item_count(items_owned, ";")
```

We can also specify the name of the arguments:
```python=
get_item_count(items_str=items_owned, sep=";")
```

Q: can we specify the type of the arguments of the function? A: yes, that is possible with type checking, but unfortunatly beyond the scope of this workshop (see resources).

Note that we can retrieve the doc string that we created:
```python=
help(get_item_count)
```

Q: can we also return a string describing what we return?
A: we could for example:
```python=
def test_function(a):
    return "a is", a

test_function(1)
```
This returns a *tuple* which is a specific python structure, similar to a list. You can index it like this:
```python=
result[0]
```

Q: can you have a function without `return` statement? Yes, but the function will still return something: namely the special `None` object. e.g:
```python=
def function_without_return(a):
    print(a)

value = function_without_return(1)

print(value)
```

`None` is a special object to represent missing values.

Q: what is `yield`? A: This is a more advanced topic, it is similar to `return` but in an iterator.


#### Libraries
So far we have use built-in function, but there are additional functions that come in library, or *package*. Anaconda installation includes already a large number of pre-installed libraries. For example, tomorrow we will use pandas. We import it as follows:
```python=
import pandas

# Now we can use the read_csv function from pandas
pandas.read_csv()
```

Often, we use aliases for packages to have to do less typing:
```python=
import pandas as pd # This is the 'standard' alias for pandas
import matplotlib.pyplot as plt # Library for plotting

pd.read_csv()
```

Q: do we need to both load and install? A: the `import` statements loads them. Anaconda already comes with a lot of packages so we don't need to install them for this course. But for other packages, you can install them in a terminal window.
To install a package (for example pandas) in Jupyter lab, you can open a Terminal from the launcher. Then type:
```bash=
pip install pandas
```
This retrieves package from Pypi (see resources) and also installs dependencies.

Q: do we need to install anything for tomorrow? A: no we have everything installed. But make sure to have all the data downloaded! (see line 51 of this document)

Q: are there lists of standard packages for a specific field? A: different fields do this in different ways. Pypi has all the packages so only useful if you already know what you need. Anaconda includes all the most common packages for data analysis. You can also search for `awesome list <topic>`. Be aware that lists may be outdated!


## 📚 Resources
[Python documentation: built in functions](https://docs.python.org/3/library/functions.html)

[Jupyter notebook navigation commands](https://jupyter-notebook.readthedocs.io/en/stable/examples/Notebook/Notebook%20Basics.html)

[PEP-8 python style guide](https://peps.python.org/pep-0008/)

[Type hints in python](https://docs.python.org/3/library/typing.html)
[Extensive article on typing in Python](https://realpython.com/python-type-checking/)

[Pypi repository for Python packages](https://pypi.org/)
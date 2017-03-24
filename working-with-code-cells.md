
# Working with code cells

In this notebook you'll get some experience working with code cells.

First, run the cell below. As I mentioned before, you can run the cell by selecting it the click the "run cell" button above. However, it's easier to run it by pressing **Shift + Enter** so you don't have to take your hands away from the keyboard.


```python
# Select the cell, then press Shift + Enter
3**2
```




    9



Shift + Enter runs the cell then selects the next cell or creates a new one if necessary. You can run a cell without changing the selected cell by pressing **Control + Enter**.

The output shows up below the cell. It's printing out the result just like in a normal Python shell. Only the very last result in a cell will be printed though. Otherwise, you'll need to use `print()` print out any variables. 

> **Exercise:** Run the next two cells to test this out. Think about what you expect to happen, then try it.


```python
3**2
4**2
```




    16




```python
print(3**2)
4**2
```

    9
    




    16



Now try assigning a value to a variable.


```python
mindset = 'growth'
```

There is no output, `'growth'` has been assigned to the variable `mindset`. All variables, functions, and classes created in a cell are available in every other cell in the notebook.

What do you think the output will be when you run the next cell? Feel free to play around with this a bit to get used to how it works.


```python
mindset[:4]
```




    'grow'



## Code completion

When you're writing code, you'll often be using a variable or function often and can save time by using code completion. That is, you only need to type part of the name, then press **tab**.

> **Exercise:** Place the cursor at the end of `mind` in the next cell and press **tab**


```python
mindset
```




    'growth'



Here, completing `mind` writes out the full variable name `mindset`. If there are multiple names that start the same, you'll get a menu, see below.


```python
# Run this cell
mindful = True
```


```python
# Complete the name here again, choose one from the menu
mindful
```




    True



Remember that variables assigned in one cell are available in all cells. This includes cells that you've previously run and cells that are above where the variable was assigned. Try doing the code completion on the cell third up from here.

Code completion also comes in handy if you're using a module but don't quite remember which function you're looking for or what the available functions are. I'll show you how this works with the [random](https://docs.python.org/3/library/random.html) module. This module provides functions for generating random numbers, often useful for making fake data or picking random items from lists.


```python
# Run this
import random
```

> **Exercise:** In the cell below, place the cursor after `random.` then press **tab** to bring up the code completion menu for the module. Choose `random.randint` from the list, you can move through the menu with the up and down arrow keys.


```python
random.
```

Above you should have seen all the functions available from the random module. Maybe you're looking to draw random numbers from a [Gaussian distribution](https://en.wikipedia.org/wiki/Normal_distribution), also known as the normal distribution or the "bell curve". 

## Tooltips

You see there is the function `random.gauss` but how do you use it? You could check out the [documentation](https://docs.python.org/3/library/random.html), or just look up the documentation in the notebook itself.

> **Exercise:** In the cell below, place the cursor after `random.gauss` the press **shift + tab** to bring up the tooltip.


```python
random.gauss
```

You should have seen some simple documentation like this:

    Signature: random.gauss(mu, sigma)
    Docstring:
    Gaussian distribution.
    
The function takes two arguments, `mu` and `sigma`. These are the standard symbols for the mean and the standard deviation, respectively, of the Gaussian distribution. Maybe you're not familiar with this though, and you need to know what the parameters actually mean. This will happen often, you'll find some function, but you need more information. You can show more information by pressing **shift + tab** twice.

> **Exercise:** In the cell below, show the full help documentation by pressing **shift + tab** twice.


```python
random.gauss
```

You should see more help text like this:

    mu is the mean, and sigma is the standard deviation.  This is
    slightly faster than the normalvariate() function.


```python
%pdb
```

    Automatic pdb calling has been turned ON
    


```python
numbers = [2,3]
sum(numbers)
```




    5



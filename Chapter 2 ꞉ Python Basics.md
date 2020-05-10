---
tags: [Data Science/Anaconda, Data Science/Python, Notebooks/Data Science from Scratch]
title: 'Chapter 2 : Python Basics'
created: '2020-05-09T06:52:23.908Z'
modified: '2020-05-10T08:26:12.877Z'
---

# Chapter 2 : Python Basics

### Anaconda Virtual Environments

Create a Python 3.6 environment named "dsfs"  
`conda create -n env_name packages`

Activate environment
`conda activate env_name`

Deactivate environment
`conda deactivate`

Installing IPython
`python -m pip install ipython`

### Whitespace Formatting

* Always use spaces
* Use `%paste` when pasting code into IPython

### Functions

* We can assign variables to functions and pass the variable into another function
* Short anonymous functions (lambda) [x - argument , : return ___] 
[](@search/lambda)

  ```python
  def apply_to_one(f):
    return f(1)

  y = apply_to_one(lambda x : x + 4)   # equals 5
  ```

* Function parameters can be given default arguments

```python
def my_message(message = "default message") :
  print(message)
```

### Strings
* To read backlashes,, use raw strings: r" "
* Create multi-line strings using three double quotes: """
* 3 Methods to combine strings
  1. \+ symbol : ` full = "s1" + " " + "s2" `
  2. string.format: `full = "{0} {1}".format(first, last)`
  3. **f-string**: `full = f"{first} {last}"`

### Data Structures in Python

Refer to : [Data Structures in Python](@note/Data Structures in Python.md)

### Control Flow

1. if-else

```python
if boolean:
  ...
elif boolean:
  ...
else boolean:
  ...
```

2. ternary if-then-else

```python
value = "v1" if boolean else "v2"
```

3. for loops
* `continue` and `break` to adjust loop iteration

```python
# x is arbitrary. range(n) produces 0, 1, ..., n-1  
for x in range(10)
  print x
```     


### Truthiness

#### Falsy
    - False
    - None
    - []
    - {}
    - ""
    - set()
    - 0 
    - 0.0
Everything else is `True`

* `all(iterable)` : Returns `True` if all values are True.
* `any(iterable)` : Returns `True` if at least one item is True.

### Sorting

Default sort is by **ascending** order.
Optional arguments: 
    - `key = function_name` >> sorts by the value returned by function
    - `reverse = True`
* `.sort()`
* `sorted(x)` (does not change the list)

### List Comprehension

Syntax: 
```python
 return_expression for x in iterable_list if boolean
 ```

### Automated Testing and assert
To test wheter our code runs as expected. 
Raises `AssertionError` if not truthy.
```python
def smallest_item(x):
  return min(x)

assert smallest_item([0, 1, 2]) == 0
```

### Object Oriented Programming

```python
class Node:

  def __init__(self, prev_node = None, element = None, next_node = None):
    self.prev_node = prev_node
    self.data = data
    self.next_node = next_node
```
* `___init__` is the constructor. The parameters are class variables.
* Methods with double underscores are _private methods_.
* Inheritance example
```python
class Subclass(Class):
  def override_method(self):
    return ...
```

### Iterables and Generators




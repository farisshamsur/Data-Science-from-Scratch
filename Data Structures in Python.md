---
tags: [Data Science/Python/Data Structures]
title: Data Structures in Python
created: '2020-05-10T06:31:43.676Z'
modified: '2020-05-10T08:46:17.779Z'
---

# Data Structures in Python

### 1. List (array)

 Syntax: `list = [x, y, z]`

* Lists can contain different types of data (even another list)
* list[-1] -> _Pythonic_ for accesing the last element and so on
* List slicing: list[i : j] -> indexes the list from [i, j) 
* Optional slicing argument: step (increment) -> `list[<start> : <end> : <step>]`

1. Universal methods
  - len(x) -> returns the number of elements in the list
  - sum(x) -> sums all elements in the list
2. List methods
  - extend(list2) -> combines two lists
  - append(element) -> adds element to end of the list
3. Additional tricks
  - x in list -> returns True if list contains x. O(n)
  - x, y = [1,2] -> sets x to 1 and y to 2.

### 2. Tuples

Syntax: `tuples = (x, y, z)`
        `tuples = x, y, z`

* Same as lists but tuples are **Immutable** (cannot be edited/changed)
* Pythonic way to swap variables:
```python
x, y = 1, 2   # set x to 1, y to 2
x, y = y, x   # x is now 2, y is now 1
```

### 3. Dictionaries

Syntax: `dict = {item}`

* Elements (Items) are key-value pairs. 
  Element -> `key : value`  
  **keys must be unique and immutable!**

* Offers fast look-up times.
* Often used as a frequency table

* Accessing value:
  ` dict[key]` -> Returns value

* `key in dict` -> Returns True if dict contains key
  Fast checks even for large data sets

* Assign key-value pairs using square brackets. Adds key-value pair if key does not exist in dict.
  `dict[key] = value`

1. dict Methods
  - `.keys()` -> Iterable for the keys
  - `.values()` -> Iterable for the values
  - `.items()` -> Iterable for the (key, value) tuples
  - `.get(key, value)` -> returns the value. if key does not exist, returns the specified value in the argument

#### defaultdict
    
    Syntax: `Syntax: defaultdict(default_function)`

    * Essentially still a dictionary _but_ doesn't return a KeyError if key doesn't exist.
    * Uses the function given in the argument to give the default value
```python
from collections import defaultdict

word_counts = defaultdict(int) # int() produces 0
for word in document:
  word_counts[word] += 1   # On the first encounter, key : 0 + 1
``` 
Now we move on to Counters.  
    
#### Counters

* Turns a sequence of values into a defaultdict(int) ie: {keys : count}
* `.mostcommon(n)` -> Returns the n<sup>th</sup> most common keys

   ```python
    from collections import Counter
    c = Counter([0, 1, 2, 0])

    # >> c = {0:2, 1:1, 2:1}
  ```

### 4. Sets

Syntax: `set = {}`

* A collection of **distinct** elements.
* Constructor -> `set()`
    - Accepts lists as argument
* Why use sets ? 
    - `in` is very fast for sets
    - to find _distinct_ items
















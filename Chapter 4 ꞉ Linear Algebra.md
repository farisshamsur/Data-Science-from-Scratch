---
tags: [Notebooks/Data Science from Scratch]
title: 'Chapter 4 : Linear Algebra'
created: '2020-05-13T09:04:36.203Z'
modified: '2020-05-13T23:20:49.998Z'
---

# Chapter 4 : Linear Algebra

## Vectors

```python
height_weight_age = [162,
                      60,
                      20]
```
Python interprets this as a list. We want to use it as a vector. Hence we will build the tools necessary.

* Defining a Vector in Python
```python
from typing import List
Vector = List[float]
```

### Vector addition

* Use zip and list comprehension

```python
def add(v: Vector, w: Vector) -> Vector:
    assert len(v) == len(w)
    return [v_i + w_i for v_i, w_i in zip(v,w)]
```
### Vector Subtraction

```python
def subtract(v: Vector, w: Vector) -> Vector:
  assert len(v) == len(w)
  return [v_i - w_i for v_i, w_i in zip(v,w)]
```
### (Component-wise) Sum a **list** of vectors

```python
def vector_sum(vectors: List[Vector]) -> Vector:
  # Check that vectors is not empty
  assert vectors, "no vectors provided!"

  # Check the size of all vectors are equal
  num_elements = len(vectors[0])
  assert all(len(v) == num_elements for v in vectors), "different sizes!"

  return [sum(vector[i] for vector in vectors)
          for i in range(num_elements)]
```

### Scalar Multiplication

```python
def scalar_multiply(c: float, v: Vector) -> Vector:
  return [c*v_i for v_i in v]
```

### (Component-wise) Mean of a Vector

```python
def vector_mean(vectors: List[Vector]) -> Vector:
  n = len(vectors)
  return scalar_multiply(1/n, vector_sum(vectors))
```

### Dot Product
* The length of a vector, v when projected onto a vector w.

```python
def dot(v: Vector, w: Vector) -> float: 
  """Computes v_1*w_1 + v_2*w_2 + ... + v_n*w_n"""
  assert len(v) == len(w)
  return sum(v_i*w_i for v_i, w_i in zip(v,w))
```

### Sum of Squares

```python
def sum_of_squares(v: Vector) -> float:
  return dot(v, v)
```

### Magnitude of a Vector

* Distance from origin
```python
import math

def magnitude(v: Vector) -> float:
  return math.sqrt(sum_of_squares(v))
```
### Distance between two vectors

```python
import math

def squared_distance(v: Vector, w: Vector) -> float:
    return sum_of_squares(subtract(v,w))

def distance(v: Vector, w: Vector) -> float:
  return math.sqrt(squared_distance(v,w))

# OR 

def distance(v: Vector, w: Vector) -> float:
  return magnitude(subtract(v,w))
```

> Note: Using lists as vectors is great for exposition, _but_ **terrible for performance**. Use `NumPy` in the real-world.

## Matrices

* Defining a Matrix in Python
```python
from typing import List

Matrix = List[List[float]]

# Example
A = [[1, 2, 3], 
      [4, 5, 6]]
```
### Shape of a matrix
* Shape: A <sub>n x m<sub>
```python
from typing import Tuple

def shape(A: Matrix) -> Tuple[int, int]:
   n_rows = len(A)
   n_columns = len(A[0]) if A else 0
   return n_rows, n_columns
```

### Get Row and Get Column

```python
def get_row(A: Matrix, i: int) -> Vector:
  """Returns the i-th row of a Matrix"""
  return A[i]

def get_column(A: Matrix, j: int) -> Vector:
  """Return the j-th column of a Matrix"""
  return [v[j] for v in A]
```

### Create a Matrix
Create a Matrix given a **Shape** and a **function**.
```python
from typing import Callable

def create_matrix(n_rows: int, 
                  n_columns: int,
                  entry_fn: Callable[[int, int], float]) -> Matrix:
      
    return [[entry_fn(i,j) # Given i, create [entry_fn(i,0), ...]
            for j in range(n_columns)]
            for i in range(n_rows)]
```
### Identity Matrix
Create an n x n Identity Matrix
```python
def identity_matrix(n: int) -> Matrix:
  return create_matrix(n, n, lambda i, j: 1 if i == j else 0)
```

## Why use Matrices ?
* Can be used to represent a dataset (columns represent variables/features)
* A n x m Matrix can be used to represent a linear function that maps m-dim to n-dim.
* Represent binary relationships. (Adjacency Matrix)

> Note: Indexing element `i, j` (index) -> `A[i][j]`





















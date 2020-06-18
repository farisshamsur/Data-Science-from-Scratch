---
tags: [Data Science/Statistics/Basics, Notebooks/Data Science from Scratch]
title: 'Chapter 5 : Statistics'
created: '2020-05-13T23:23:39.587Z'
modified: '2020-05-15T06:38:18.667Z'
---

# Chapter 5 : Statistics

## Central Tendencies

### Mean
> $\bar{x} = \frac{sum(x)}{count(x)}$

```python
def mean(xs: List[float]) -> float:
  return sum(xs) / len(xs)
```
#### Coded Mean
> $$\bar{x} = \frac{\sum_{x=1}^n (x - a)}{n} + a$$

### Median

* Middle-most value. Not affected by outliers.
* If len(x) is odd , return the middle element.
* If len(x) is even, return the average of two middle-most value.
> Use on **sorted data** !

```python
def __median_odd(xs: List[float]) -> float:
  return sorted(xs)[(len(xs)) // 2]

def __median_even(xs: List[float]) -> float:
  sorted_xs = sorted(xs)
  hi = len(xs) // 2
  lo = hi - 1
  return (sorted_xs[lo] + sorted_xs[hi]) / 2

def median(v: List[float]) -> float:
  return __median_odd(v) if len(v) % 2 != 0 else __median_even(v)
```
> Reminder: Index stars with `0` ! 

### Quantile

* This is a more generalised version of the median. (Median is the 0.5th percentile)

```python
def quantile(xs: List[float], p:float) -> float:
  """Returns the p-th percentile value in x"""
  p_index = int(len(xs)*p)
  return sorted(xs)[p_index]
```

### Mode

* The most common value

```python
def mode(xs: List[float]) -> List[float]:
  """Returns a list, since there might be more than one mode"""
  counts = Counter(xs)
  max_count = max(counts.values())
  return [x_i for x_i, count in counts.items()
          if count == max_count]
```
## Dispersion

Refers to the measures of how _spread out_ our data is.

### `data_range`
* The difference between the largest and smallest value
```python
def data_range(xs: List[float]) -> float:
  return max(xs) - min(xs)
```

### Variance

The formula for sample variance, s^2^:
> $$s^2 = \frac{\sum(x_{i} - \bar{x})^2}{n-1}$$

```python
from scratch.linear_algebra import sum_of_squares

def de_mean(xs: List[float]) -> List[float]:
  """Translate xs by subtracting its mean (so adjusted list has mean 0)"""
  x_bar = mean(xs)
  return [x - x_bar for x in xs]

def variance(xs: List[float]) -> float:
  assert len(xs) >= 2 , "variance requires at least 2 elements"

  n = len(xs)
  deviations = de_mean(xs)
  return sum_of_squares(deviations) / (n - 1)   # n - 1 if data set is from a sample
```
### Standard Deviation
* The square root of variance
```python
import math

def standard_deviation(xs: List[float]) -> float:
  return math.sqrt(variance(xs))
```

### Interquartile Range

```python
def interquartile_range(xs: List[float]) -> float:
  """Returns the difference between the 75%-ile and the 25%-ile"""
  return quantile(xs, 0.75) - quantile(xs, 0.25)
```

## Correlation

* Studying whether two variables are related.

### Covariance

* Measures how two variables vary in tandem from their means

_Excerpt from Quora:_

The covariance between two variables is **positive when they tend to move in the same direction** and **negative if they tend to move in opposite directions**.

To see how we arrive at the definition, first think about two variables each with mean zero. That is, each variable could be positive or negative but is on average zero. To summarize whether the two variables move together, we can look at the product:

When both variables have the same sign, it's positive;
When they have opposite signs, it's negative;
When they are both large and have the same sign, you get a big positive number;
When they are both large and have opposite signs, you get a big negative number;

Sample Covariance, Cov(x,y):
> $$Cov(x,y) = \frac{\sum (x_{i}-\bar{x})(y_{i}-\bar{y})}{n - 1}$$

```python
from scratch.linear_algebra import dot

def covariance(xs: List[float], ys: List[float]) -> float:
  assert len(xs) == len(ys)
  return dot(de_mean(xs), de_mean(ys)) / (len(xs) - 1)
```
* Difficulties in interpreting covariance
    - The unit is: unit~x~ * unit~y~ (maybe hard to interpret)
    - Hard to say how "large" is considered large

## Correlation

* Alternative solution to covariance. 

Correlation formula:
> $$r_{xy} = \frac{Cov(x,y)}{\sigma_{x}\sigma_{y}}$$
> $$r_{xy} = \frac{\sum (x_{i} - \bar{x}) (y_{i} - \bar{y}) }{\sqrt[2] {\sum (x_{i} - \bar{x})^2 \sum(y_{i} - \bar{y})^2}}$$

```python
def correlation(xs: List[float], ys: List[float]) -> float:
  stdev_x = standard_deviation(xs)
  stdev_y = standard_deviation(ys)

  if stdev_x > 0 and stdev_y > 0:
      return covariance(xs, ys) / stdev_x / stdev_y
  else:
      return 0
```
* Properties of Correlation:
    - Unit-less.
    - Always lies between -1 and 1.

## Simpspn's Paradox

* Correlations can be misleading when *confounding variables* are ignored.
* Taking a closer look at the data will reveal that some buckets skew more heavily. 
* Issue: Correlation measures the relationship between two variables, **all else being equal**.

## Correlation and Causation

> Correlation $\neq$ Causation

To feel confident about causality, conduct *randomised trials*.
1. Randomly split users into two groups.
2. Give one group a slightly different experience.











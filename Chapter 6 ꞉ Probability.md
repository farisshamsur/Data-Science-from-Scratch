---
tags: [Notebooks/Data Science from Scratch]
title: 'Chapter 6 : Probability'
created: '2020-05-15T06:39:02.133Z'
modified: '2020-05-15T10:08:08.386Z'
---

# Chapter 6 : Probability

## Independent Events

> $$\Rho(E \cap F) = \Rho(E)\Rho(F)$$

## Conditional Probability

> $$\Rho(E \mid F) = \frac{\Rho(E \cap F)}{\Rho(F)}$$

## Bayes Theorem

> $$\Rho(A_{i} \mid B) = \frac{\Rho(B \mid A_{i})\Rho(A_{i})}{\Rho(B)}$$
> $$\Rho(A_{i} \mid B) = \frac{\Rho(B \mid A_{i})\Rho(A_{i})}{\sum_{j=1} ^ n \Rho(B \mid A_{j}) \Rho(A_{j})}$$
* Choose a specific case, $i$,  and sum for all cases of A.
Refer: [Bayes Theorem](@mlfromscratch.com/probability-theory-bayes-theorem/#/)

## Continuous Distribution

### Uniform Distribution

```python
def uniform_pdf(x: float) -> float: 
  return 1 if x >= 0 and x < 1 else 0

def uniform_cdf(x: float) -> float:
  if x < 0: return 0
  elif x < 1: return x
  else: return 1
 ```
### Normal Distribution

PDF of Normal distribution:
> $$f(x \mid \mu , \sigma) = \frac{1}{\sqrt{2\pi}\sigma}\exp(-\frac{(x - \mu)^2}{2 \sigma ^2})$$

```python
import math
SQRT_TWO_PI = math.sqrt(2*math.pi)

def normal_pdf(x: float, mu: float = 0, sigma: float = 1) -> float:
  return (math.exp(-(x - mu)**2 / 2 / sigma**2) / (SQRT_TWO_PI * sigma))
```

If $Z$ is a standard normal distribution ($\mu = 0, \sigma = 1$), then so is $X = \sigma Z + \mu$





















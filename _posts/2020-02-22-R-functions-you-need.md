---
layout: post
title:  "Bend R functions to your will "
---

# Bend R functions to your will

In this post, I will mention a few R functions that are very useful to manipulate other functions or objects. If you are not acquainted with them, I hope that they open a whole world of possibilities in the R code you develop, as they did for me.

### 1. Ellipsis

Ellipsis may be placed in the definition of a function to substitute multiple values that are given as arguments to that function and are not captured by other argument variables.

The expression `...` may then be used in the body of the function in lieu of writing the values that is substituting.

As an example take the following function that returns the sum of the arguments other than `a`.

```
> sum_rest <- function(a, ...) return(sum(...))
> sum_rest(1, 2, 3)
[1] 5
> sum_rest(1, a = 2, 3)
[1] 4
```

Note that in the first calculation the value returned is `sum(2, 3)` whereas the vlue in the second calculation is `sum(1, 3)` since the second argument is declared as a keyword argument that matches the first variable.


### 2. do.call


### 3. formals



`list(bquote())`

### 4. get


### 5. Performance of C or Fortran implementations





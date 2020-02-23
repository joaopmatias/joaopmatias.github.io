---
layout: post
title:  "Bend R functions to your will "
---

# Bend R functions to your will

In this post, I will mention a few R functions that are very useful to manipulate other functions or objects. If you are not acquainted with them, I hope that they open a whole world of possibilities in the R code you develop, as they did for me.

### 1. Ellipsis

Ellipsis (`...`) may be placed in the definition of a function to substitute multiple values that are given as arguments to that function and are not captured by other argument variables.

The expression `...` may then be used in the body of the function in lieu of writing the values that is substituting.

As an example take the following function that returns the sum of the arguments other than `a`.

```
> sum_rest <- function(a, ...) return(sum(...))
> sum_rest(1, 2, 3)
[1] 5
> sum_rest(1, a = 2, 3)
[1] 4
```

Note that in the first calculation the value returned is `sum(2, 3)` whereas the value in the second calculation is `sum(1, 3)` since the second argument is declared as a keyword argument that matches the first variable.


### 2. do.call

`do.call` executes a function using the values in a given list as arguments. Furthermore, in the case the list used is a named list, each element in the list is matched with a keyword arguments according to its key (or name).

This function is specially useful to execute a function with an unknown number of arguments.

In the following example, the value of one of the arguments is returned.

```
> return_a <- function(a, b, c) return(a)
> do.call(return_a, list(1, 2, 3))
[1] 1
> do.call(return_a, list(b = 1, a = 2, c = 3))
[1] 2
```

Finally, if the function uses ellipsis in its definition, then the list provided may have more values than the number of arguments of the function.

```
> return_a <- function(a, b, c, ...) return(a)
> do.call(return_a, list(1, 2, 3, 4, 5))
[1] 1
```


### 3. formals

`list(bquote())`

### 4. get







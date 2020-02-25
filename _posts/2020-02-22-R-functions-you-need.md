---
layout: post
title:  "Bend R functions to your will "
---

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

`do.call` executes a function using the values in a given list as arguments. Furthermore, in the case that the list used is a named list, each element in the list is matched with a keyword arguments according to its key (or name).

This function is specially useful to execute a function with an unknown number of arguments.

In the following example, the value of one of the arguments is returned.

```
> return_a <- function(a, b, c) return(a)
> do.call(return_a, list(1, 2, 3))
[1] 1
> do.call(return_a, list("b" = 1, "a" = 2, "c" = 3))
[1] 2
```

Finally, if the function uses ellipsis in its definition, then the list provided may have more values than the number of arguments of the function.

```
> return_a <- function(a, b, c, ...) return(a)
> do.call(return_a, list(1, 2, 3, 4, 5))
[1] 1
```


### 3. formals

`formals` allows to manipulate the keyword arguments of a function. It takes as argument a function and returns a named list with each key (or name) matching one of the arguments of the function and the corresponding value matching the default value of that argument. Changing the object returned by `formals` also affects the keyword arguments, their default values or the order of the keyword arguments.

Let us look at an example where the argument variable of a function is changed.

```
> dummy <- function(x = 0) return(0)
> formals(dummy)
$x
[1] 0
> formals(dummy) <- list("y" = 0)
> dummy
function(y = 0)
return(0)
```

In the example above, the change does not affect the values returned by the function, but that may not be the case if the result depends on positional arguments.

```
> dummy <- function(x = 0, y = 0) return(x)
> dummy(1, 2)
[1] 1
> formals(dummy) <- list("y" = 0, "x" = 0)
> dummy
function(y = 0, x = 0)
return(x)
> dummy(1, 2)
[1] 2
```

In combination with `bquote()` we may also remove the default values, by creating a list with elements that have a key and no values.

```
> dummy <- function(x = 0, y = 0) return(x)
> formals(dummy) <- list("y" = bquote(), "x" = bquote(), "..." = bquote())
> dummy
function(y, x, ...)
return(x)
```

### 4. get

Finally, an alternative way to evaluate a variable is using the `get` function.

```
> x <- 1
> get("x")
[1] 1
> string <- "x"
> get(string)
[1] 1
```

### Conclusion

I hope you find this post useful and share your favorite tricks of the R language, too!

---
layout: post
title:  "Lightweight alternatives to stream video on the browser"
---

Like many other programmers, I often enjoy having youtube or twitch videos playing on the brackround while doing other tasks on the computer. However, the typical method of have the videos playing in a tab of the browser as some disadvantages like the computer memory consumption or the nuisance of having more open tabs. Because of that I searched for some alternatives to playing video on the browser and would like share my setup with more people.







that may be reduced if we consider some alternatives methods.





Did you ever ask yourself what would happen if you tweaked some functions in an R package? Recently, I found myself in a situation where I would like to perform and test some changes to an R package and started looking for ways to easily and clearly register some findings. This pursuit eventually led me to learn more about R environment, after all, whenever you install a package in your system you also add a number of environments associated with that package.

Let me add that one advantage of working with R packages is that most source code (if not all!) is available somewhere and may be dissected by the user, so one can easily download whatever package they want, apply the desired changes, load the package and test the changes. However, this may be a bit cumbersome since you need all the source of the package (not just the functions you wish to alter), it may not be easy to track all the changes you are doing in different files (although `git` may provide a huge help) and tracking and sharing the results of different sets of changes may also be difficult (for example, I like to share my results as `rmarkdown` notebook).

As usual, check the R documentation on the subject and, in particular, the following functions:

* `search`
* `environment`
* `attach`
* `detach`
* `new.env`
* `$` operator
* `list2env`

Let me show one example below

```
my.env <- new.env()
list2env(lapply(as.list(asNamespace("testthat")),
                function(fcn) {
                    environment(fcn) <- my.env
                    fcn
                }),
         my.env)

```

The above code generates a new environment containing all the functions in the package `testthat`. The expression `environment(fcn) <- my.env` here guarantees that the copies of the functions are attached to the environment `my.env` that they are found whenever called from inside other functions. Then, we may modify the function `test_file`, for example.

```
my.env$test_file <- function(...) print("Test yourself!")
environment(my.env$test_file) <- my.env

```

After executing the following command in a file of your choosing a number of times, you may see a familiar quote from this post.

```
my.env$test_package("path-to-package")

```

**Disclaimer** 

This approach may not work with all packages. In particular, if they use features of R packages other than traditional functions.

### References
* [Advance R](https://adv-r.hadley.nz/environments.html)
* [Stackoverflow](https://stackoverflow.com/questions/9965577/r-copy-move-one-environment-to-another#9966441)

Thank you for reading and do not hesitate to share your comments!

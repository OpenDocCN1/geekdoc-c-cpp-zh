# 210 CREATING CLASSES AND METHODS IN R

Let us now apply some of what we have learned about creating generic methods to our regr regrFit classes of the previous section. Our first illustration will use the S4 function show that can be used either explicitly or implicitly to print out information about an object. It is called implicitly when an object's name is entered on the command line.

At present, a default version of show would be applied to regr objects that employs appropriate versions of show for the objects that occupy its slot. For large data sets this is likely much more output than necessary, for example the entire X matrix and response vector would exhibited. As a result, it is probably worthwhile to extend show to regr objects in a way that produces sincinct and interpretable output.

To create a new method for show the arguments must be known for its parent or hub generic function that will be used for method dispatch. To discover this information function name can be entered on the command line as the beginning of the section. If there are R manual pages for the function these will also provide argument details. Still another option is use of the args function as in

```
args(show)
function(object)
NULL
```

This tells us that show has a single named object. With this knowledge in hand, a (very) terse show method for regr objects

```
show.regr <- function(object){
cat("An object of class regr with,\ ncol(object@X),
"predictors", "\n")
}
```

that uses the function as described in Section 5.2 for printing output. This is installed as a new method function

+   * setMethod("show", signature("regr"), show.regr)

Then,

+   * regrCar
Object of class regr with 3 predictors
* regrFit
Object of class regr with 3 predictors

which demonstrates that the new version of show is now being used for regr objects. As regrFit is a derived class of regr, this version of show will also work for regrFit objects.

In some cases it is of interest to perform a transformation on the dependent variable when conducting regression analysis. Numeric objects are raised to a power in R with the ^ operator. A check with generics reveals that ^ is an S4 function in the base package that is loaded whenever an R session is started. An application of args produces

+   * args("")
function(e1, e2)

Thus, new method functions may be defined that have the arguments e1 and e2. A new method function that will produce a regr object with a power transformed variable is to be

+   * setMethod("-", signature("regr", "numeric"), function(e1, e2)
+ regr(e1@X, e1@y^e2)

[1]
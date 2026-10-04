
You see that regardless of the data type, class reports the structure of the object itself—all matrices. The same is true for other object structures, like arrays, lists, and data frames.

## Multiple Classes

Certain objects have multiple classes. A variant on a standard form of an object, as an ordered factor vector, will inherit the usual class and also contain the additional ordered class. Both are returned if you use the class function.

```
R ordfac.vec <- factor(x=c("Small","Large","Large","Regular","Small"),
                              levels=c("Small","Regular","Large"),
                              ordered=TRUE)
```

```
R ordfac.vec
[1] Small Large Regular Small
Levels: Small < Regular < Large
R class(ordfac.vec)
[1] "ordered" "factor"
```

Earlier, fac.vec was identified as "factor" only, but the class of ordfac.vec has two components. It's still identified as "factor", but it also includes "ordered", which identifies the variant of the "factor" class also present in the object. Here, you can think of "ordered" as a subclass of "factor". In other words, it is a special class that inherits from, and therefore behaves like, a "factor". For further details on R subclasses, I recommend Chapter 9 of The Art of R Programming by Matloff (2011).

> NOTE I have focused on the class function here because it's directly relevant to the object-oriented programming style exercised in this text, especially in Part II. There are other functions that show some of the complexities of R's class rules. For example, the function typeof reports the type of data contained within an object, not just for vectors but for matrices and arrays. Note, however, that the terminology in the output of typeof doesn't always match the output of class. See the help ?typeof for details on what it returns.

To summarize, an object's class is first and foremost a descriptor of the data structure, for simple vectors, the class function reports the type of data stored. If the vector entries are exclusively numbers, then R classes the vector as "integer", whereas "numeric" is used to label a vector with floating-point numbers.

## 6.2.3 Is-Dot-Object-Checking Functions

Identifying the class of an object is essential for functions that operate on stored objects, especially those that behave differently depending on the class of the object. To check whether the object is a specific class or data type, you use the *is-dot functions on the object and it will return a TRUE or FALSE logical value.

Is-dot functions exist for almost any sensible check you can think of. For example, consider once more the num.veci vector from Section 6.2.2 and the following checks:

```
R num.veci <- 1:4
R num.veci
[1] 1 2 3 4
R is.integer(num.veci)
[1] TRUE
R is.numeric(num.veci)
[1] TRUE
R is.matrix(num.veci)
[1] FALSE
R is.data.frame(num.veci)
[1] FALSE
R is.vector(num.veci)
[1] TRUE
R is.logical(num.veci)
[1] FALSE
```

The first, second, and sixth is-dot functions check the kind of data stored in the object, while the others check the structure of the object itself. The results are as expected: num.veci is an "integer" (and is a "vector"). It's not a matrix or a data frame, nor is it logical.

Briefly, it's worth noting that these checks use more general categories than the formal classes identified with class. Recall that num.veci identified solely as "integer" in Section 6.2.2, but using is.numeric here returns TRUE. In the num.veci with integer data is generalized to "numeric". Similarly, for a data frame, an object of class "data.frame" will return TRUE for is.data.frame and is.list because a data frame is intuitively generalised to a list.

There's a difference between the object-dot functions detailed here and functions such as is.na discussed in Section 6.1. The functions to check for the special values NA should be thought of as a check for equality; they exist because not legal syntax to write something like foo=NA. Those functions from Section 6.1 operate in R's element-wise fashion, whereas the object is-dot functions inspect the object itself, returning only a single logical value.

## 6.2.4 As-Dot Coercion Functions

You've seen ways to modify an object after it's been created—by accessing and overwriting elements, for example. But what about the structure of the object itself and the type of data contained within?

Converting from one object to another is referred to as coercion. Like other features of R you've met so far, coercion is performed either implicitly or explicitly. Implicit coercion occurs automatically when

elements need to be converted to another type in order for an operation to complete. In fact, you've come across this behavior already, in Section 4.1.4, for example, you used numeric values for logical values. Remember that logical values can be thought of as integers—one for TRUE and zero for FALSE. Implicit coercion of logical values to their numeric counterparts occurs in lines of code like this:

```
R> 1:4+(T,F,F,T)
[1] 2 2 3 5
```

In this operation, R recognizes that you're attempting an arithmetic calculation with +, so it expects numeric quantities. The logical vector is not in this form, the software internally coerces it to one and zeros before completing the task.

Another example of implicit coercion is when paste and cat are used to glue together strings, as explored in Section 4.2.2. Non-character entries are automatically coerced to strings before the concatenation takes place. Here's an example:

```
R foo <- 34
R bar <- T
R paste("Definitely foo: ",foo,"; definitely bar: ",bar,sep="")
[1] "Definitely foo: 34; definitely bar: TRUE."
```

Here, the integer 34 and the logical T are implicitly coerced to characters since R knows the output of paste must be a string.
In other situations, coercion won't happen automatically and must be carried out by the user. This explicit coercion can be achieved with the as-dot functions. Like is-dot functions, as-dot functions exist for most typical R types and object classes. The previous two examples can be coerced explicitly:

```
R as.numeric(c(T,F,F,T))
[1] 1 0 0 1
R> 1:4+as.numeric(c(T,F,F,T))
[1] 2 2 3 5
R foo <- 34
R foo.ch <- as.character(foo)
R foo.ch
[1] "34"
R bar <- T
R bar.ch <- as.character(bar)
R bar.ch
[1] "TRUE"
R paste("Definitely foo: ",foo.ch,"; definitely bar: ",bar.ch,".",sep="")
[1] "Definitely foo: 34; definitely bar: TRUE."
```

Coercions are possible in most cases that "make sense." For example, it's easy to see why R is able to read something like this:

```
R> as.numeric("32.4")
[1] 32.4
```

However, the following conversion makes no sense:

```
R> as.numeric("g'day mate")
[1] NA
Warning message:
NAs introduced by coercion
```

Since there is no way to translate "g'day mate" into numbers, the entry is returned as NA (in this case, R has also issued a warning message). This means that in certain cases, multiple coercions are needed to attain the final result. Suppose, for example, you have the character vector("1","0","1","0","0") and you want to coerce it to a logical-valued vector. Direct coercion to logical is not possible, even if all the character strings contained numbers, there is no guarantee in general that they will be ones and zeros.

```
R> as.numeric("1","0","1","0","0")
[1] NA NA NA NA NA
```

However you know that character string numbers can be converted to a numeric data type, and you know that zeros are easily coerced to logics. So, you can perform the coercion in two steps, as follows:

```
R> as.logical(as.numeric("1","0","1","0","0"))
[1] TRUE FALSE TRUE FALSE FALSE
```

Not all data-type coercion is entirely straightforward. Factors, for example, R treats the levels as integers. In other words, regardless of how the levels of a given factor are actually labeled, the software will refer to them internally as level 1, level 2, and so on. This is clear if you try to coerce a factor to a numeric data type.

```
R> baz <- factor(c("male","male","female","male"))
R> baz
[1] male male female male
Levels: female male
R> as.numeric(baz)
[1] 2 2 1 2
```

Here we see that R has assigned the numeric representation of the factor stored in the order of the factor labels (alphabetic by default). Level 1 refers to female, and level 2 refers to male. This example is simple enough,

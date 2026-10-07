# 208 CREATING CLASSES AND METHODS IN R

for cases object1 is of type character and object2 is numeric. The first method function will compute the product of its two arguments while the second prints out values. An application of func will now produce results as

```
func(2,3)
[1] 6
func("Hi ya'll!", 3)
[1] "Hi ya'll!" 3
func(as.character(2), 3)
[1] "2" 3
func("Hi", ya'll")
```

```
Error in function (classes, fdef, mtable) :
unable to find an inherited method for function "func"
for signature "character", "character"
```

Thus, the hub method for func matches the data types for the arguments that are supplied to func with its method signatures to determine (if any) are appropriate and invokes the most appropriate one to "answer" the call to func. If there are no method functions with signatures that can match the given arguments, an error message is generated.

Method dispatch cannot be based on additional arguments that come in the ellipse. This is illustrated by

```
func(2,3)
[1] 6
setMethod("func", signature("numeric", "numeric"),nfunc(object1, object2, object3) object1*object2*object3)
[1] "func"
func(2,3)
Error in object1 * object2 * object3 : 'object3' is missing
func(2, 3, 4)
[1] 24
```

Initially the func function with two numeric arguments is used. Then, a three-argument method function with numeric data types for object1 and object2 is introduced to replace the two-argument version. The conclusion is that only the types of the non-ellipsis arguments can serve as a means to distinguish between different method functions.

It is possible to have missing arguments by specifying them to be of type missing. In order for functions with missing arguments to be called, one of three things needs to be true:

+   - they are explicitly missing; e.g., a comma separated empty argument is present,
- the nonmissing arguments are specified by name or
- only trailing arguments from func's list are missing.

The opposite effect from using missing is achieved by specifying an argument as data type ANY. In this latter an object from any class can be provided as the argument's value. An illustration of this is provided in the R output below.

```
setMethod("func", signature("missing", "numeric"),nfunction(object1, object2) print("missing and numeric")
[1] "func"
setMethod("func", signature("ANY", "numeric"),nfunction(object1, object2) print("ANY and numeric")
[1] "func"
func("a")
```
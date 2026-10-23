We will not try to understand what this gives us in any great detail, but there is one significant thing to realize from this. The expressions 1 to 10 and 0 until 10 give us back values that actually are collections. These are instances of the Range type.

The Range type in Scala gives us a simple way to use the for-each style loop that Scala provides to do the counting operations that most programmers are used to using with the for loop to accomplish. You can use to and until with other integer types including the Char type. So the expression 'a' to 'z' will give you a collection of all of the lowercase letter.

What if you want to count down? The Range type has an operation by defined on it that will allow you to specify the step between elements in the Range. So if you want to go from 10 down to 1 you can use 10 to 1 by -1. We can use this to get a version of the polynomial evaluation function the uses the index counting, but does not require math.pow and instead keeps track of the exponent of x.

```
```scala
def evalPolyCountDown(coefs:Array[Double],x:Double):Double = {
  var ret=0.0
  var power=1.0
  for(i <- coefs.length-1 to 0 by -1) {
    ret+=coefs(i)*power
    power*=x
  }
  ret
}
```
```

This version has most of the advantages of both of the previous versions. It does not have to reverse the Array, nor does it require the use of math.pow. The one downside is that it still would not translate well to a List.

If you use by, you can also use Ranges of the Double type. Other, less standard, numeric types like BigInt will also work nicely with the Range type. The fact that the Range type is really a collection means that all of the methods that were discussed in the last chapter are available for them. That leads to a concise way of expressing factorial.

```
```scala
scala> (1 to 5).product
res21: Int = 120
```
```

In addition to product and sum, you can also apply map, filter, or other operations to instances of the Range type.

There are sometimes when you want to count through the indices of a collection like an Array. You could do this with code like the following assuming that you have an Array called a.

```
```scala
for(i <- 0 until a.length) ...
```
```

You can also use the indices method on the collection. Calling a.indices will give you a Range that goes from the first index to the last one. So this loop could also be expressed in this way.

```
```scala
for(i <- a.indices) ...
```
```

Not only is this shorter, it is slightly less error prone in that you can not accidentally start at 1 instead of 0, nor can you accidentally use to instead of until.
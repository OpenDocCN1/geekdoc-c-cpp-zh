```
def isSorted(a:Array[Double]):Boolean = {
  (a,a.view.tail).zipped.forall(_ <= _)
}
```

This code is a bit shorter, but significantly more advanced. In fact, it uses advanced topics from sections 8.5 and 10.4. The approach here is to make a tuple that contains the original elements first and everything but the first element second. If we zipped these two collections with the zip method, the result would be a sequence of tuples with each element and the one after it in a tuple and the first and last element appear only once in the first and last tuples. That zipped collection could then be dealt with using foreach. Such a solution would be very inefficient however, as it would actually construct a lot of new objects and do a lot of copying. The advanced topics are used to make it more efficient.

The first advanced topic is the view from section 8.5. A view is a representation of a collection that does not make a full copy unless forced to do so. In this code, taking a tail of a normal Array would produce a whole new Array and copy a lot of data over into it. However, the tail of the view is just a small object that will interact with code the same way the tail would, but through logic instead of making a real copy.

The second advanced topic is the use of the tuple zipped method from section 10.4. This is a method of the 2-and 3-tuple types that allows you to more efficiently run common functions that need to go through two or three collections at the same time. Instead of making a whole new zipped collection of tuples, this gives you back an object that has methods like map, filter, and forall declared so they take as many arguments as are in the tuple. So we get a version of forall, which needs a function of two arguments we can easily provide using the shorthand syntax.

Whichever approach you choose, you can test a particular sort with code like the following.

```
val nums=Array.fill(args(0).toInt)(math.random)
flaggedBubbleSort(nums)
assert(isSorted(nums))
```

This code creates an Array of random Doubles with a length determined by a command-line argument. It then calls a sort on that Array and then uses the assert function to make sure it is true. Assert is a standard function in Scala that can be called with one or two arguments. The first argument is a Boolean that should be true. If it is not true, an error results terminating the program. A second argument can be provided that is passed by-name and should provide a useful message if the assert fails.

The assert function can be used generally in your code. There is also a require function that performs similarly, but should be used for argument values. So at the top of a function, if the function will only work on certain argument values, you can use a call to require to make it so the code fails in an informative manner when bad arguments are passed in.

# 13.1.5 Sort Visualization

It can help you understand sorts if you get to see them in action. There are many different websites that have animations that will show you how these and other sorts work. One advantage of having already studied graphics is that we can write our own code to visualize what the sorts are doing. This is part of why the sorts above were set up to work with the Double type. It makes it easy to generate with the call to math.random and to draw because the random numbers are uniformly distributed between 0.0 and 1.0.

To set things up for the visualization, we will use the nums Array from above and put in some other code before the sort is called. We will start with the basics.
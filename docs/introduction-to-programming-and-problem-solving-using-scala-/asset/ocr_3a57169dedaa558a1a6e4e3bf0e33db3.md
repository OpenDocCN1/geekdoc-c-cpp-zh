# Arrays and Lists in Scala

the name refer to it, but to do that you create a completely new Array, you do not alter the size of the old one.³

When you are accessing the array, if you try to use an index value that is either negative or too large, Scala will give you an error message saying that you have gone outside the bounds of the Array. We can see what that looks like here with attempts to access and index out of bounds.

```
scala array(100)
java.lang.ArrayIndexOutOfBoundsException: 100
  at .init()()<console>:7)
  at <init>($console>
  at RequestResult$.<init>(<console>:9)
  at RequestResult$.<clinit>(<console>
  at RequestResult$.scala_repl_result(<console>
  at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method
at sun...
```

```
scala array(100)
java.lang.ArrayIndexOutOfBoundsException: 100
  at .init()()<console>:7)
  at <clinit>(<init>(<console>:9)
  at RequestResult$.<clinit>(<console>
  at RequestResult$.scala_repl_result(<console>
  at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method
at sun...
```

Now that we know the rules for using Arrays, we can write functions that take advantage of them in a useful way. In the last chapter we used recursion to read in a set of numbers that we could do operations on. One motivation was using recursion for collections that was previously too costly to store the values up to two or more operations on them. Two useful functions might have to be one that fills an Array from user input and another that does the types of operations we did before, but this time on the Array.

We will start with the function to fill the Array from user input. This function needs to be passed the Array that it will fill. When we are using an Array, it will be easiest to use the style where we begin by how many numbers are to read. This is because Arrays knows its size that information does not need to be passed. What needs to be passed is the index that the next number will be beyond the end of the Array. The function to do might look like this:

```
def fillArray(arr:Array[Int], index:Int):Unit = {
if (index < arr.length) {
  arr(index) = readInt()
  fillArray(arr, index+1)
}
```

This function is straightforward, but it is worth noting that it does not produce a result. The fact that Arrays are mutable that we can pass in an Array and have the function

> Note that you are not likely to notice this issue in the REPL because you can declare a new val that replaces a pre-existing one. However, in a script, you cannot have two things with the same name in the same scope, so it is important to understand this restriction.
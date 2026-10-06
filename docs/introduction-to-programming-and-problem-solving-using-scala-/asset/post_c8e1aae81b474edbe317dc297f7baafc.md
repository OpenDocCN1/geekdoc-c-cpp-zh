
# Introduction to Programming and Problem-Solving Using Scala

![](img/06d4e84f27a8884ea40ba6182ec7c778_206_0.png)

**FIGURE 7.4:** Simple image of memory layout for a few variables. The objects on the right side are overly simplified, especially the list, but this portrays sufficient detail for understanding what is happening at this point.

fer names to the same object. To understand this, we need to refine our view of what is happening in the memory of the computer. Consider the following variable declarations.

```
var i1 = 5
var d1 = 5.9
var s1 = "Scala is fun!"
var l1 = List(1,2,3,4)
var a1 = Array(1,2,3,4)
```

All of these have made as vars just to give us the option of altering them below. Normally we would want to use a val unless we explicitly found a reason why we had to change them. In this case the reason is just for illustration.

The memory layout looks like something is shown in figure 7.4. This is an idealized representation. In reality memory is all linear and has structure to it will be discussed in chapter 13. For now, this view is sufficient. On the left are boxes that represent the variables. In Scala the best picture is to see the variables as boxes that refer to values.

What happens if we change the value of two of the variables? For example, say now we execute these two lines of code.

```
i1=8
s1="New string."
```

The first one changes i1 so that it references the value 8 instead of 5. The second one changes the s1 so that it references this alternate String. What would this look like in memory?

> In some situations Scala will put the actual values in the boxes, but that is an optimization that you do not really have control over, and it will not alter the behavior; so, it is good to picture the memory like this.

# Type Basics and Argument Passing

![](img/06d4e84f27a8884ea40ba6182ec7c778_207_0.png)

**FIGURE 7.5:** Modified view of the memory after two variables have been assigned different values.

The 5 and the String "Scala is fun!" have not been changed. They remain in memory just like before. Because no exception references them, these objects will be collected and disposed of automatically by the GARBAGE COLLECTOR, a part of the system that is responsible for freeing up memory that is no longer in use. What has changed the references in i1 and s1. Both the Int and String types are immutable. They now point to new objects in chunks of memory that hold these new values. As a result, the objects are created, nothing can change. They do not allow any operations that would alter their values. If we had these variables val we would not be able to change where the arrows point either.

Indeed, of all the types one where we are immutable with the exception of the Array. So Array we can change the value in the box on the right. To see how this can matter we will consider only the List and the Array variables and add two more lines of code to the picture.

```
val i12 = i1
val a2 = a1
```

This gives us slightly different picture that is shown in figure 7.6. Now we have two different variables that point to each of the List and Array objects. These second references to the same object are often called aliases. Aliasing is where mutability often starts to cause problems. If you have not figured out why, well perhaps this code will make it clear.

```
scala> a2(3) = 99

scala> a1
res1: Array[Int] = Array(1, 2, 3, 99)
```

# Introduction to Programming and Problem-Solving Using Scala

![](img/06d4e84f27a8884ea40ba6182ec7c778_208_0.png)

In the first line we change the value in the last slot in a2. On the next line we look at the value of a1. Note that it is changed. We did not explicitly do anything with a1, but the value is changed because a2 is an alias of a1. You cannot do this with i12 because the List is immutable, the assignment statement will not compile for the List.

There are times when the ability to make an alias and change it is great. However, if you lose track of what is going on and what names are other names you run into serious problems.

At this point it might be easy to think that all you have to do is avoiding aliases. If you do not write lines like a2 = a1 then you would be fine, right? While type of aliasing might be avoidable, the next section shows why it is pretty much impossible to avoid aliasing all together.

# 7.7 Basic Argument Passing

Now that we have looked at the memory is organized for variable declarations and the aliasing issue, we should take another look at what happens when you call a function. The two are actually very similar. When you pass values into a function, the function has local vars with the argument names, but they reference the same objects that the outside variables reference. Consider the following code from a script.

```
def getAndClear(arr: Array[Int],index:Int):Int = {
  val ret = arr(index)
  arr(index) = 0
  ret
}

val numbers = Array(7,4,9,8,5,3,2,6,1)
val place = 5
val value = getAndClear(numbers,place)
```

# Type Basics and Argument Passing

In top level of script:

![](img/06d4e84f27a8884ea40ba6182ec7c778_209_0.png)

InGetAndClear:

**FIGURE 7.7:** The memory layout from the getAndClear script. The arguments passed into the function become aliases for the objects created at the top level of the script.

The function is passed an Array of Ints and an index for a location in array. It is supposed to return the value at that location and also "clear" that location. The meaning of "clear" is to store a zero at that location. To see how this works look at figure 7.7 which shows the arrangement of memory. The function is defined and the variables numbers and place are declared and initialized. We get new objects for them to reference.
When the getAndClear function is called, numbers and place are passed to the values of the arguments arr and index. While the code is in getAndClear, arr is an alias for the object referred to by numbers and index is an alias for the object referred to by place. This is significant because the getAndClear method has a side effect. It modifies the values stored in the Array that is passed. When the code goes down to "Other stuff", the memory looks a bit different as shown in figure 7.8. At that point, the function has finished so local variables are no longer needed. In addition, the 6th element in the array numbers has been changed. The function managed to change the value for the Array as seen outside. With a name like getAndClear you could probably figure that this type of side effect might happen. However, when you pass any mutable value into a function, you need to be aware that the function could change your value, even if you do not want it to.

How would this be different with a List? Well, the List is immutable, so it would be impossible to change. We return a new List. We will quickly go through a few ways to do this.

# Introduction to Programming and Problem-Solving Using Scala

In top level after getAndClear:

![](img/06d4e84f27a8884ea40ba6182ec7778_210_0.png)

FIGURE 7.8: The configuration of memory after getAndClear has executed.

```
def getAndClear(lst:List[Int],index:Int):(Int,List[Int]) = {
  lst(index), lst.zipWithIndex.map( tuple =>
    val (n,i) = tuple
    if (i == index) 0 else n
  })
}
```

There is only one exception in this function, the tuple to return. The first element in the tuple is (index). It looks up the proper value and uses it there. Remember that looking things this way on a List is not efficient, but we have to do so. The second part of the tuple is a bit more complex. It calls the method zipWithIndex on lst. Substituting for a value in a List is a common enough that the API calls a method to do it for us. So we can create a simpler version of getAndClear for a List that uses the updated.

```
def getAndClear(lst:List[Int],index:Int):(Int,List[Int]) = {
  lst(index), lst.updated(index,0)
}
```

Another approach would be to pull off the elements before and after the index and then stick them together with a 0 between them.

```
def getAndClear(lst:List[Int],index:Int):(Int,List[Int]) = {
  lst(index), lst.take(index)::lst.drop(index+1)
}
```

This version uses the cons operator, ::, which we saw before. It adds one new element to the front of a List and gives it back. It is an operator that we have not seen previously,

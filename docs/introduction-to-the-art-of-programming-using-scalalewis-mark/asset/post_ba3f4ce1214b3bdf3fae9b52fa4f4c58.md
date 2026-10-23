
Each of these deserves a fair bit of discussion. We will also talk about how they compare to one another and the way in which they impact programmers.

When you are first learning to program, the errors that you likely run into the most are syntax errors. These can be as simple as typos or misspellings. They can also be more complex like type mismatch errors or calling functions or methods with the wrong number of arguments. The common element that makes something a syntax error is that it is discovered by the compiler when it is trying to translate the human written code into a format that is more computer friendly. Different programming languages do different amounts of checking for errors at compile time. This is often called STATIC CHECKING because it can be done without actually running the program.

Scala does a significant amount of static checking for errors.10 The way we have been running our programs in the REPL or with scripts, the compile stage is not clearly separated from the running of the program. The Scala system is running a compiler in the background and then executing the results of the compile. The syntax errors display a message like the following:

```
timing.scala:5: error: not found: value This
This line will not compile
_
one error found
```

They tell you the name of the file along with a line number. Then they describe the error and show the line and where on the line the error occurred.

The second type of bug is a runtime error. This type of error occurs when everything is syntactically correct and the program compiles and runs. However, during the run this error causes the program to crash. In Scala a runtime error will produce a message that looks similar to the following:

```
java.lang.ArrayIndexOutOfBoundsException: -1
    at Main$$anon$1.<init>(timing.scala:5)
    at Main$.main(timing.scala:1)
    at Main$.main(timing.scala)
...
```

This message tells you what went wrong and then prints a stack trace that includes line numbers. In this simple example, the code failed on line 5.

There are many different reasons why runtime errors happen, and it might be dependent on user input. So a runtime error might not be found from running the program once or twice. To reduce the number of runtime errors in a program you have to run it with multiple different input test inputs as was discussed in section 8.5. In a general sense, it is impossible to prove that code has no runtime errors.

The last type of error is a logic error. An error is a logic error if the code compiles and runs to normal termination, but provides an incorrect output or behaves incorrectly in some other manner. These errors can come in all types of forms and there is no message that tells you there is a problem. You know there is a problem by checking the output or behavior of the program to see if it matches expectations. Like runtime errors, logic errors might not occur for all inputs. There might be only specific inputs that trigger the error.

If you have a choice, you want errors of types higher on the list. As a novice programmer you probably get tired of dealing with syntax errors and find them frustrating. However, the reality is that syntax errors are by far the best type of error. This is because syntax errors give you the most information on how to fix them and are detected by the compiler

## 13.5 Memory Layout

The memory of the computer is basically like a huge array of bytes. It is shared between the operating system and many different programs. Different parts of memory can be allocated for different things or associated with different devices. Scala hides most of the intricacies of memory from you. It is not a language designed for doing low-level system programming. At some point in your Computer Science training you should learn about the details of computer memory. For our purposes here, we will only care about the organization of memory inside of the allocation of a single program.

The memory for a program is broken into two broad pieces, the STACK and the HEAP. These terms were chosen intentionally and the images they invoke in your mind are probably fairly accurate. A stack is orderly with one item placed on top of the previous one. A heap is much less organized with items placed almost at random. Local variables and function arguments are allocated on the stack. As was discussed in section 7.8, the memory model in Scala is such that the variables are references and they refer to objects. In this memory model, the objects are allocated on the heap. Every time a new function is called, the memory for the arguments and the local variables, along with some memory for bookkeeping, is allocated in a block that is referred to as the STACK FRAME. If that function calls another, then another frame is allocated on top of it. When a function returns, the stack frame for that function is freed up. That same memory will be used later for another function.

This should help explain the output from a runtime error. The stack implicitly keeps track of where you are in each function when it calls the next. You can picture each of those functions stacked on top of the one that called it. That is what gets printed in the stack trace. Each line tells you what function has been called followed by the file name and line number.

The objects on the heap are allocated in free spaces. The memory for objects is freed up automatically when the object is no longer in use. The automatic freeing of heap memory is accomplished by a process called GARBAGE COLLECTION. An object can be collected if it can no longer be reached by following references that start on the stack. Not all languages include garbage collectors. In those that do not, the programmer is responsible for freeing memory that was allocated on the heap.

## 13.6 Sorting/Searching with case classes

In the sorts and searches that we have looked at, we were working with numeric types. More generally, the code that was written will work with any type that works with the comparison operators. As such, our code would have worked with Array[Char] or Array[String] if you simply altered the type that was passed into the sort. The case classes we have written do not meet this requirement. As such, we need to make other alterations to the code beyond the type if we want to sort a case class. Fortunately, these alterations are not all that significant.

We will work with the following case class.

```
case class Weather(id:String,year:Int,month:Int,precip:Double,tmax:Double,
  tmean:Double,tmin:Double)
```

This **case class** was created to store historical weather data. It was used to represent records for monthly data on temperature and precipitation. You would load an entire file of these records into an **Array**. If you want to see the hottest ten months you could sort the array by the high temperatures. Code for such a sort is shown here.

```
def bubbleSortWeatherHighTemps (a:Array[Weather]) {
for (j <- 0 until a.length-1) {
for (i <- 0 until a.length-1-j) {
if (a(i).tmax > a(i+1).tmax) {
val tmp=a(i)
a(i)=a(i+1)
a(i+1)=tmp
}
}
}
}
```

A bubble sort was picked because of the simplicity of the sort. It is very easy to see what was changed. The only changes are the type in the parameter for the **Array** that is passed in and the fact that the comparison is done between fields of the **Array** elements. After applying this sort to the **Array** you can use **take** or **takeRight** to pull off the elements at one end or the other.

**case classes** also present another alternative that we did not really get with single values, the ability to have the comparison based on more than one field. For the weather data, it is likely to be stored in the data file in chronological order. Proper chronological order is a combination of both the year and month fields. If you wanted to have the ability to search for entries by time you might want to have a binary search that can look for a particular year and month. Code for doing that, is listed here.

```
def binarySearchWeather (a: Array [Weather], year: Int, month: Int): Int = {
var start=0
var end=a.length
var mid=(end+start)/2
while (end>start && (a (mid).year!=year || a(mid).month!=month)) {
if (year < a(mid).year || (year=a(mid).year && month < a(mid).month)) {
end=mid
}
else {
start=mid+1
}
}
mid=(end+start)/2
}
if (end <= start) -1 else mid
}
```

Note that the comparison has become significantly more complex. It has to compare the year first and then if there is a tie, break that tie with the month.

Unfortunately, when written in this way, we have to write a completely separate sort or search for each ordering we might want on the **case class**. For example, if you wanted wettest months instead of hottest months, you would need a separate sort. You might feel that copying a whole sort or search function only to make such small changes is not very efficient and that there should be a way to make a sort or search that works more generally. We can help improve these functions for **case** classes here. Later, in chapter 19, we will gain the ability to abstract these ideas so that the function works with multiple types, not just different sort orders on a single type.

# 13.5 Memory Layout

The memory of the computer is basically like a huge array of bytes. It is shared between the operating system and many different programs. Different parts of memory can be allocated for different things or associated with different devices. Scala hides most of the intricacies of memory from you. It is not a language designed for doing low-level system programming. At some point in your Computer Science training you should learn about the details of computer memory. For our purposes here, we will only care about the organization of memory inside of the allocation of a single program.

The memory for a program is broken into two broad pieces, the STACK and the HEAP. These terms were chosen intentionally and the images they invoke in your mind are probably fairly accurate. A stack is orderly with one item placed on top of the previous one. A heap is much less organized with items placed almost at random. Local variables and function arguments are allocated on the stack. As was discussed in section 7.8, the memory model in Scala is such that the variables are references and they refer to objects. In this memory model, the objects are allocated on the heap. Every time a new function is called, the memory for the arguments and the local variables, along with some memory for bookkeeping, is allocated in a block that is referred to as the STACK FRAME. If that function calls another, then another frame is allocated on top of it. When a function returns, the stack frame for that function is freed up. That same memory will be used later for another function.

This should help explain the output from a runtime error. The stack implicitly keeps track of where you are in each function when it calls the next. You can picture each of those functions stacked on top of the one that called it. That is what gets printed in the stack trace. Each line tells you what function has been called followed by the file name and line number.

The objects on the heap are allocated in free spaces. The memory for objects is freed up automatically when the object is no longer in use. The automatic freeing of heap memory is accomplished by a process called GARBAGE COLLECTION. An object can be collected if it can no longer be reached by following references that start on the stack. Not all languages include garbage collectors. In those that do not, the programmer is responsible for freeing memory that was allocated on the heap.

# 13.6 Sorting/Searching with case classes

In the sorts and searches that we have looked at, we were working with numeric types. More generally, the code that was written will work with any type that works with the comparison operators. As such, our code would have worked with Array[Char] or Array[String] if you simply altered the type that was passed into the sort. The case classes we have written do not meet this requirement. As such, we need to make other alterations to the code beyond the type if we want to sort a case class. Fortunately, these alterations are not all that significant.

We will work with the following case class.

```
```scala
case class Weather(id:String,year:Int,month:Int,precip:Double,tmax:Double,
  tmean:Double,tmin:Double)
```
```
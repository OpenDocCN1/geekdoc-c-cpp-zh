```
Console.WriteLine("The value of i is: " + i);
}
```

The output from this program is

```
The value of i is: 0
```

As the output verifies, i is initialized to zero. Remember, without the use of new, i would be uninitialized, and it would cause an error to attempt to use it in the WriteLine() statement without explicitly giving it a value first.

In general, invoking new for a value type invokes the default constructor for that type. It does not, however, dynamically allocate memory. Frankly, most programmers do not use new with the value types.

# Garbage Collection and Destructors

As you have seen, objects are dynamically allocated from a pool of free memory by using the new operator. Of course, memory is not infinite, and the free memory can be exhausted. Thus, it is possible for new to fail because there is insufficient free memory to create the desired object. For this reason, one of the key components of any dynamic allocation scheme is the recovery of free memory from unused objects, making that memory available for subsequent reallocation. In many programming languages, the release of previously allocated memory is handled manually. For example, in C++, the delete operator is used to free memory that was allocated. However, C# uses a different, more trouble-free approach: garbage collection.

C#'s garbage collection system reclaims objects automatically—occurring transparently, behind the scenes, without any programmer intervention. It works like this: When no references to an object exist, that object is assumed to be no longer needed, and the memory occupied by the object is eventually released and collected. This recycled memory can then be used for a subsequent allocation.

Garbage collection occurs only sporadically during the execution of your program. It will not occur simply because one or more objects exist that are no longer used. Thus, you can't know, or make assumptions about, precisely when garbage collection will take place.

# Destructors

It is possible to define a method that will be called just prior to an object's final destruction by the garbage collector. This method is called a destructor, and it can be used in some highly specialized situations to ensure that an object terminates cleanly. For example, you might use a destructor to ensure that a system resource owned by an object is released. It must be stated at the outset that destructors are a very advanced feature that are applicable only to certain rare cases. They are not normally needed. They are briefly described here for completeness.

Destructors have this general form:

```
~class-name() {
    // destruction code
}
```
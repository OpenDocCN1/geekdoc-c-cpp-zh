
If the programmer does not want to replace this code with the exception-based code, then new(nothrow) must be used instead of new. The example will now be

```
include <new>
...
int* PointToArrayOfInt = new(nothrow) int[5];
if(!PointerToArrayOfInt)
cout << "error!";
```

> Note The new(nothrow) operator does not throw an exception if memory is not allocated but returns null pointer, similar to malloc(). It is advisable, though, to write a new code using exception handling. Error handling using exception is cleaner and more readable. The header file <new> should be included for using the new operator.

Consider the following statements:

```
int* PointerToArrayOfInt2 = (int*) new int[4][3];
and
int* PointerToArrayOfInt3 = (int*) new int[FirstDimension][3];
```

Both statements are correct. Here, FirstDimension is a variable and is initialized before a call to new is made. (This is possible because the call to new is made at run-time.) The second argument, however, must be a constant. The statement

```
int SecondDimension = 5;
int* PointerToArrayOfInt4 = (int*) new int[FirstDimension][SecondDimension];
```

is wrong and is not acceptable because subsequent dimensions after the first dimension cannot be variables.

Consider the last two lines of the program. The delete operator is applied to pointer variables. It is analogous to the free() function of C. These variables were earlier initialized using new. The delete operation performs the job of releasing the memory. Thus, the memory allocated using new is deallocated using delete. It should be noted that the array version of delete uses [] before the variable name. So delete[]PointToArrayOfInt is valid, but delete PointToArrayOfInt[] is invalid.

If memory is allocated using malloc() and deallocated using delete, or allocated using new and deallocated using free(), then the results can be surprising. The standard says that the result is undefined, which means that a specific compiler may take any action it deems fit. It may even crash the program.

![](img/0da15892b2796544fb447dc5727e9ab4_86_0.png)

## 2.9.3 Placement new

Some ways in which the new operator can be used are as follows:

- 1. int* p = new int;
  // Normal new call
- 2. int* p = new(nothrow) int;
  /* Does not throw exception in case memory is not allocated and returns the pointer value as null */
- 3. int* p = (int*) new int[3][4];

```
// For allocating memory to arrays
4. int* p = new int(3);
// For initializing the variable at the time of memory allocation
```

The `placement new` is a variant of new. It works in the following manner:

```
int* p = new int;    // normal new
int* q = new(p) int; // placement new
```

Here, no memory is allocated for the variable q; its address is the same as p. It is useful in some special cases. Suppose images from somewhere are being read and displayed one after the other. Assume that the images are stored in an object of class image one after the other and that a pointer is pointing to the area of memory that holds the image, known as position. Now, when the first image is loaded, the following is written:

```
position = new Image(FirstImage);
```

This will create a new object, allocate memory for it, and initialize the memory with FirstImage. For all subsequent images, the code will be

```
position = new(FirstImage) SecondImage
...
position = new(SecondImage) ThirdImage
...
```

thereby storing every image at the same location where the first image had been stored. Readers may question the need for using placement new in this case, instead of writing a simple assignment such as *position = SecondImage.

If both the images, FirstImage and SecondImage, are of the same size, then this statement is acceptable. If they are of different sizes, placement new is the only option available as it calls the destructor of FirstImage first and then it calls the constructor of SecondImage.

> **Note** Placement new is useful when we want another pointer to occupy the memory given to an earlier pointer. Unlike normal copy operation, placement new calls the destructor of the previous object and the constructor of the new object replacing it, thus avoiding any unwanted consequences. For example, suppose the pointer points to images and the second image is smaller than the first one. Merely copying the values will lead to the second image occupying some part and the remaining part containing the older image. It is advisable to use placement new if such effects are to be avoided.

## 2.9.4 new vs malloc()

Some of the advantages of new over malloc() are as follows:

- 1. The syntax of new is simpler than that of malloc(). No size, no void pointer, and no casting are required for the new operator.
- 2. new is an operator, whereas malloc() is a function. Operators execute faster than functions. Context switching can be avoided with operators as they are not functions. Their equivalent assembly code should be directly pasted by the compiler at the time of compilation.
- 3. new has various forms as discussed in Section 2.9.3. malloc() does not have such facilities.
- 4. new is class-aware. It is possible to change the meaning of new to suit the need of a user-defined class. This is known as operator overloading.

## Notes

- 1. It is possible to have an operator implemented as a function in C++. In that case, there will be no advantage if the function is not defined inline.
- 2. Unlike malloc(), new can be overloaded such that class objects can be given memory as per the need and at the place the user wants it. When new is overloaded for any class, calling new with the object of that class follows the process defined by the developer of that class and not by the conventional memory management defined by C++.

## 2.9.5 Significance of delete Operator

The delete operation does not seem to be important when used in programs. The use of delete is not important in places where the machine is shut down at the end of the day, for example, an educational institute. However, there are places where the machine is not shut down daily and the programs continue to run without any halt for a very long period, for example, web servers and related components. In such cases, the memory space occupied by the new variables will continue to increase while the program is running unless they are deleted periodically. At some point of time, the memory will be exhausted and the program will crash. On the other hand, if the machine is shut down, the space occupied is released automatically and there will be no problem of insufficient memory.

# Note

Web servers run for long periods. In such programs, if the objects introduced by new do not have a corresponding delete to be used when they go out of scope, the memory occupied by such objects is not regained and the program crashes when the memory is full. C++11, obviously inspired by Java, added garbage collection; it is a process by which the memory wasted by such objects that have gone out of scope can be reclaimed and problems such as mentioned here can be avoided.

## 2.9.6 New Casting Operators, typeid, and throw

C++ has new function-like castings as well as old C-style castings. To convert an int variable into a float in C, FloatVar = (float) IntVar; is used. However, in C++, this is written as

```
FloatVar = float(IntVar);
```

which is more readable. The old C-style casting is still available and is very popular among programmers.

Four new casting operators have been recently added by the C++ Standardization Committee for providing better casting operations than that offered by the old C-style casting. These are dynamic cast, reinterpret cast, static cast, and const cast. The old C-style cast is still valid in C++, though using new casting operators is recommended. These are discussed in Sections 11.2–11.5 in Chapter 11. typeid also is used in the context of RTTI and throw is used when exception handling is used to trap errors in C++.

The following code illustrates how try, throw, and catch can be used in a given circumstance. The block covered by try is monitored by C++ during the execution of the program. When a throw statement is encountered, the control gets permanently transferred to the corresponding catch statement. In the following case, if throw error1 is executed, the control gets transferred to catch(ErrorType1 er), and if throw error2 is executed, the control gets transferred to catch(ErrorType2 er) block.

```
try
{
    ErrorType1 error1;
```


The effect of the recursion can be seen much better from the call graph, where the entry for calc_sum_rec() reads as follows:

```
---------------------------------
                167166000                calc_sum_rec [4]
0.01    0.00    1000/501500              main [1]
4.27    0.00    500500/501500            all1 [2]
[4] 15.0  4.28    0.00    501500+167166000  calc_sum_rec [4]
                167166000                calc_sum_rec [4]
---------------------------------
```

The number of recursive calls appears here three times: in the first line, where calc_sum_rec() is a parent of itself; in the fourth line where both the number of non-recursive and of recursive calls (the latter behind the + symbol) are shown; and in the fifth line, where calc_sum_rec() is shown as child. For more complex structures of recursive calls like fA() calls fB() and fB() calls fA(), these numbers might be different for the different entries.

In some cases, only parts of the program are (fully) profiled. This can happen, if the final program is linked from several object code files, where some had not been compiled with the -pg option. Also, one can choose some functions explicitly to be analyzed. Using (multiple times) the option -p and/or -q followed by a function name will show only the entries which involve the listed functions.

Finally, note that you can build in your own timing measurements into your program. This is useful to measure the timing of some critical part of your program during all simulations, and including the timing results in your standard log files. For this purpose, the C standard library function times can be used, declared in sys/times.h. It measures the time in units of clock ticks, hence with the highest possible resolution. More information on the usage of the function can be found in the UNIX man page via typing "man 2 times" in a shell.

## Chapter 5 Object-oriented Software Development

In recent years, *object-oriented* programming languages like C++, Smalltalk or Eiffel became very popular. These programming languages are usually used to implement programs which are designed in an object-oriented way. But, *using an object-oriented language and designing a* simulation program in an object-oriented style are not necessarily the same. For example, you can set up your whole project by applying object-oriented methods even when using a traditional *procedural* programming language like C, Pascal or Fortran. In general, taking an object-oriented viewpoint facilitates the analysis of problems and the development of suitable programs.

An introduction to object-oriented software development can be found for example in Refs. [Rumbaugh et al. (1991); Johnsonbaugh and Kalin (1994); Skansholm (1997)]. The first section of this chapter gives an introduction to object-oriented concepts.

As already mentioned, the implementation of an object-oriented design is still possible with a procedural language. This is shown in Sec. 5.2, where *histograms* (see Sec. 8.3.3) are implemented in C.

In the final section of this chapter, the histograms are implemented again, but now using C++. This section also serves as an introduction to C++, which is basically an object-oriented extension of C. Furthermore, C++ offers *templates*, which allow to implement algorithms for unspecified, i.e. arbitrary, data types. This will be covered in another chapter (see Sec. 7.2). In general, the advantage of C++ is that it helps you to organize your programs in terms of objects, but still you have the flexibility to do it in a non-object-oriented way as well.

![](img/0dfb82b7d27bdfebb8b65cb33de3626a_155_0.png)

Fig. 5.1 An example of objects. There are objects of different types, here "atoms", "containers" and solvent "water". Each object has internal states or variables and interacts with the other objects via defined access interfaces. For example, in a simulation of proteins dissolved in water, an atom has a position and a velocity, which are influenced via forces from other atoms, the solvent and the container.

The object-oriented and the procedural world, depending on the actual problem. In modern programming, usually only the basic functionality is implemented as methods, while many algorithms are implemented via standard subroutines.

- **Data capsuling**

    When using a computer, you do not care about the implementation. When you press a key on the keyboard, you would like to see the result on the screen. You are not interested in how the key converts your keystroke into an electrical signal, how this signal is sent to the input ports of the chips, how the algorithm treats the signal and so on. Similarly, a main principle of object-oriented programming is to hide the actual implementation of the objects. Access to them is only allowed via given interfaces, i.e. via methods. The internal data structures are hidden, this is called **private** in C++. The data capsuling has several advantages:

    - You do not have to remember the implementation of your objects.

      When using them later on, they just appear as a black box fulfilling

Charged atoms as well. A similar form of hierarchical organization of objects works the other way round: Higher level objects can be defined in terms of lower level objects. This is called a composition [Meyers (2005)]. For example, a book is composed of many objects belonging to the class "page". Each page can be regarded as a collection of many "letter" objects. For the physical example above, when modeling chemical systems, you can have "atoms" as basic objects and use them to define "molecules". Another level up would be the "system" object, which is a collection of molecules.

- **Function/operator overloading**

    The inheritance of methods (i.e. functions in C++) to lower level classes is an example of operator overloading. It just means that you can have methods for different classes having the same name, sometimes the same code applies to several classes. This can happen also for classes, which are not connected by inheritance. For example, you can define how to add integers, real numbers, complex numbers or larger objects like lists, graphs or documents. In languages like C or Pascal, you can define subroutines to add numbers and subroutines to add graphs as well, but they must have different names. In C++, you can define the operator "+" for many different classes (see one example in Sec. 5.3). Hence, the operator-overloading mechanism of object-oriented languages is just a tool to make the code more readable and clearly structured.

- **Software reuse**

    Once you have an idea of how to build a chair, you can do it several times. Because you have a blueprint, the tools and the experience, building another chair is an easy task.

    This is true for building programs as well: Both data capsuling and inheritance facilitate the reuse of software. For instance, once you have written your class for treating lists, you can include the lists in other programs as well. This is easy, because later on you do not have to care about the implementation. With a class designed in a flexible way, much time can be saved when realizing new software projects.

### 5.2 A sample using C

As mentioned before, when programming in an object-oriented way, you do not necessarily have to use an object-oriented language. It is true that they are helpful for the implementation and the resulting programs will look slightly more elegant and clearer, but you can program everything with a language like C as well. In C, an object-oriented style can be achieved very easily. As an example, a "class" histo implementing histograms is outlined next. Histograms are needed for almost all types of computer simulations as evaluation and analysis tools. Formally, histograms are introduced in Sec. 8.3.3.

Initially, you have to think about the data you would like to store. The histogram itself is an array table of bins. Each bin just counts the number of events which fall into a small interval of the corresponding histogram range. To achieve a high degree of flexibility, the range and the number of bins must be variable. It is assumed here for simplicity that all bins have the same width. Thus, the width delta of each bin can be calculated easily. For convenience delta is stored as well. To count the number of events which are outside the range of the table, the entries low and high are introduced. Furthermore, statistical quantities like mean and variance should be available quickly and with high accuracy. Thus, several accumulated moments sum[] of the distribution are stored separately as well. Here, the number of moments _HISTO_NOM_ is defined as a macro, converting this macro to variable would be straightforward. Altogether, this leads to the following C data structure:

| GET SOURCE CODE |
|---|
| DIR: oop |
| FILE(S): histo.h |

```c
#define _HISTO_NOM_ 9  /* No. of (statistical) moments */

typedef struct
{
    double      from, to;  /* range of histogram */
    double      delta;     /* width of bins */
    int         n_bins;    /* number of bins */
    double      *table;    /* bins */
    int         low, high; /* No. of data out of range */
    double      sum[_HISTO_NOM_]; /* sum of 1s, numbers, numbers^2 ...*/
} histo_t;
```

Here, the postfix _t is used to stress the fact that the name histo_t denotes a type. The bins are variables of type double, which allows for more general applications. Please note that it is still possible to access the internal structures from outside, but it is not necessary and not recommended. In C++, you could prevent this by declaring the internal variables

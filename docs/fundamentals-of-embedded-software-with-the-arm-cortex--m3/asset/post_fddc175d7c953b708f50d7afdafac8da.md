
## 11.5 STATIC ALLOCATION

Static objects are allocated (and possibly initialized) *once* when the program is first loaded into memory. Their location in memory never changes during the entire execution of the program, and thus static objects are not destroyed until the program terminates.

The *advantage* of static allocation is persistence of values. Unlike objects that use automatic allocation, a value stored in a static object will remain from one execution of a function to another.

The *disadvantage* of static allocation is the inability to reclaim the memory for other purposes once the object is no longer needed. Extensive use of static objects can thus result in programs that require lots of memory. An inexperienced programmer's attempt to avoid dealing with scope restrictions by declaring all objects global will ultimately produce very "fat" programs.

Every global object inherently uses static allocation. Inexperienced programmers will sometimes make an object global just to retain its value from one invocation of a function to the next. However, a better way to accomplish the same thing without global *scope* may be to simply add the keyword `static` to the declaration of a local object, as shown in Figure 11-4.

| Bad | Good |
| :--- | :--- |
| /\* These two objects are \*/<br>/\* global to this file! \*/<br><br>unsigned total = 0 ;<br>unsigned count = 0 ;<br><br>void Enter_Score(unsigned score)<br>{<br> total += score ;<br> count++ ;<br> printf("average score = %u\n",<br> total / count ) ;<br> } | void Enter_Score(unsigned score)<br>{<br> /\* These two objects are \*/<br> /\* local to this function! \*/<br> static unsigned total = 0 ;<br> static unsigned count = 0 ;<br><br> total += score ;<br> count++ ;<br> printf("average score = %u\n",<br> total / count ) ;<br> } |

FIGURE 11-4 Good and bad ways to retain a value.

Problems can occur, however, when static objects are modified by more than one thread. It is natural to be concerned about this possibility when the object is global. However, moving them into the local scope of a function does not prevent it. If you are not used to using static locals, you may be tempted to keep your static objects global rather than learning why restricting their scope does not help. But the real problem has nothing to do with their scope; rather, it is the fact that they are static. Thus, the first priority should be to try to change their allocation method to automatic or dynamic if possible.

## 11.6 THREE PROGRAMS TO DISTINGUISH STATIC FROM AUTOMATIC

Sometimes it is easier to understand something that you have seen in action. The output from the three programs shown in Example 11-2 provides a bit of insight into how static and automatic object allocation differ with respect to creation, initialization, and destruction of objects.

![](img/f0b8aa873b11dc585ed698a10d04e7a7_214_0.png)

### 11.6.1 Object Creation

Example 11-2 is intended to provide some insight into how object creation differs between objects with automatic allocation and those with static allocation. The program consists of functions main, f1, and f2. Function f1 declares two integer objects: one called “a” with automatic allocation. Another called “s” with static allocation. Function f1 is called three times: first by the main program, then by f2 (which is called by main), and then from main again.

In all three cases, the address of the static object “s” remains unchanged, which indicates that there is a single instance of “s” whose location in memory remains fixed throughout the entire execution of the program.

The address of the automatic object “a”, however, changes when f1 is called indirectly by f2 as opposed to when it is called directly by the main program. Therefore, its location clearly does not remain fixed, which indicates that it is created (and destroyed) several times during the execution of the program.

### 11.6.2 Object Initialization

Example 11-3 is intended to provide some insight into how object initialization differs between objects with automatic allocation and those with static allocation. The program consists of functions main, f1, f2, f3, and f4.

In functions f1 and f2, the allocation method used for the integer object has no effect on the function behavior. In both functions, the integer is reset to zero each time the function is invoked by an executable statement in the body of the function.

```c
#include <stdio.h>

int f1() { auto int a ; a = 0; return ++a ; }
int f2() { static int s ; s = 0; return ++s ; }

int f3() { auto int a = 0 ; return ++a ; }
int f4() { static int s = 0 ; return ++s ; }

int main()
{
    printf("f1(): %d %d %d\n", f1(), f1(), f1()) ;
    printf("f2(): %d %d %d\n", f2(), f2(), f2()) ;
    printf("f3(): %d %d %d\n", f3(), f3(), f3()) ;
    printf("f4(): %d %d %d\n", f4(), f4(), f4()) ;

    return 0 ;
}

Program Output:
f1(): 1 1 1
f2(): 1 1 1
f3(): 1 1 1
f4(): 3 2 1
```

## EXAMPLE 11-3 Initialization of automatic versus static objects.

Functions f3 and f4 are similar except that the initial value of the integer is specified in its declaration. This kind of initialization is performed at the time of object creation; whether object creation happens when the function is invoked or when the program is first loaded into memory (i.e., before execution) depends on the memory-allocation method used by the object.

Automatic objects are created each time execution enters their containing block and are destroyed on its exit from the block. This means that the integer "a" in function f3 is created and reinitialized each time f3 is called, as evidenced by constant return value of 1.

Static objects, however, are created (and initialized) only once, when the program is first loaded into memory. Thus, the first invocation of f4 returns 1, the second returns 2, and so on.

### 11.6.3 Object Destruction

Example 11-4 is intended to provide some insight into how object destruction differs between objects with automatic allocation and those with static allocation. Unfortunately, the term "object destruction" is a bit misleading. What actually happens when an object is "destroyed" is that its memory is made available for other uses; the object's data may continue to reside in that memory for some time until the memory is allocated for some other purpose and then written into.

3 The C programming language allows the order in which function parameters are evaluated to vary from one compiler to another. Although the sequence of values shown in the fourth line of output in Example 11-3 indicates that the parameters were processed right to left, other compilers may process them left to right, causing the values to appear in the opposite order.

```c
#include <stdio.h>

int *f1()
{
    static int s = 12345 ;
    return &s ;
}

int *f2()
{
    auto int a = 12345 ;
    return &a ;
}

void Demo(int *(*f)())
{
    int *p = (*f)() ;
    printf("Address=%08X, Contents=%d\n", p, *p) ;
    printf("Address=%08X, Contents=%d\n", p, *p) ;
    printf("\n") ;
}

int main() { Demo(f1) ; Demo(f2) ; return 0 ; }
```

## EXAMPLE 11-4 Destruction of automatic versus static objects.

The program shown in Example 11-4 consists of functions main, f1, f2, and Demo. Functions f1 and f2 each create an integer object, initialize it to the value 12345, and return the object's address; the only difference is that the object created by f1 uses static allocation, while the one created by f2 uses automatic allocation.

Function Demo stores the object's address returned by either f1 or f2 in pointer "p" and accesses the contents of that location by dereferencing the pointer. Then the address and contents are displayed using a call to library function printf. Note that there are two identical calls to printf within Demo. When Demo uses f1, the two printf calls display identical values for the address (p) and its contents (*p). However, when Demo uses f2, the first and second printf calls display different values for the content.

The automatic object in f2 is released (destroyed) and its memory made available for other purposes when f2 returns. The memory has not yet been reallocated or its value overwritten when it is retrieved (*p) as a parameter to be passed to the first printf call.4 However, during the execution of printf, that memory is reused, as evidenced by the modified value displayed by the second printf. The static object, however, does not get released until the program terminates, and thus its value remains unaffected.

4 Although unlikely, it is possible that the memory released on return from f2 might be reallocated and overwritten by a hardware-interrupt service routine that happens to be triggered just before calling printf.


> Note An operator used in C can have a new meaning in C++. One can use it in a context different from the one in which they are defined to work.

## 2.9.1 Scope Resolution Operator

In C, if a variable is defined globally and a local variable with the same name is also defined in the same program, then the global variable is not available in the local variable’s context. However, in C++, the scope resolution operator helps in the visualization of a global variable in the context of the local variable with the same name. Consider Program 2.5 to understand this better.

### PROGRAM 2.5 Scope resolution operator

```
//ScopeRes.cpp
#include <iostream>
using namespace std;

int Variable = 10;  // The global variable
void main()
{
    do
    {
        int Variable;   // The local variable
        // The context of local variable starts from here
        cin >> Variable;
        cout << Variable << '\n';
        cout << "Global variable value is";

        // The following will work only in C++
        cout << ::Variable; // Prints the global variable
        cout << "\n";

        if(Variable == 0)
            break;

        /* The if condition checks for the local variable and the context of local variable ends here. If this line is commented, the program will not come out of the loop because the following while statement checks for the global variable */
    } while(Variable);
    // Global variable being tested
    cout << "The global value outside the loop is";
    cout << Variable;  // Prints the global variable, i.e., 10
}
```

### How the Program Works

It can be observed that there are two variables of the same name Variable in this program. One is global and the other is local, defined in the while block. Consider the following statement:
cout << ::Variable
This statement prints the global variable’s value. This is because if only Variable is written, it is assumed to be a local variable as in C, but if it is preceded by the :: operator, that is, ::Variable, the C++ compiler understands it to be a global variable. Thus, it is possible to access the global variable even when a local

> The scope resolution operator makes it possible for a programmer to use both global and local variables with the same name.

variable is in effect. The :: operator, which indicates the global variable, is known as the scope resolution operator. Thus, TheVariable will be a local variable, whereas ::TheVariable will be a global variable. There is no such operator in C, and hence, it is not possible to access any global variable when a local variable of the same name is in effect.

> Note A local variable is said to be in effect and holds meaning only in the block in which it is defined. The area in which the variable holds its meaning is known as the scope of the local variable.

The next three operators in Table 2.2, the member-pointer, pointer-to-member-using object, and pointer-to-member-using-pointer-to-object operators, need the understanding of the class construct and are discussed in Chapter 3.

## 2.9.2 new and delete Operators

In C, malloc() and free() are normal functions for allocating and deallocating memory. However, C++ has a better mechanism for this. It uses operators that provide the advantage of better efficiency. The malloc() and free() function calls involve the context switching operation (placing the context of the calling function on the stack and executing malloc() or free()). Context switching operation, which is explained in Exhibit 2.2, is costly in terms of time and resources.

### Exhibit 2.2 Context switching

Whenever a function is called in either C or C++, the current state of the calling function must be stored and the called function's context must be brought in. As soon as the function call is over, the called function's context must vanish and it must be restored to the original status. This is known as context switching.

For example, when the program control enters the called function, the called function's variables are not accessible. When the control comes back, they are again made available. This operation requires loading the called function's variables and a few other details (such as values of those variables at the time when the function is called and the address where the program control should go after the function call gets over) on a stack, at the time of calling the function, and removing them when control returns to the called function. It involves a lot of work. Such overheads are not present for operators because the code related to operators is built-in, that is, it is inserted by the C++ compiler while compiling. The use of operators does not involve the costly operation of context switching.

Though most C++ compilers implement new and delete operators in terms of function operators malloc() and free(), this is not mandatory by the standard. Thus, the advantage of efficiency may not be available for some C++ compilers.

The operator new is used for allocation of memory. The syntax of new is very simple. To get memory for an integer and assign the address of the allocated memory to pointer p, the following is written:

```
int *p = new int
```

Casting or size specification is not necessary here as in malloc(). However, a pointer variable should be used only after memory allocation. (This is also true for a pointer getting memory using malloc().) Consider Program 2.6 to see the use of new and how the pointer variable can be wrongly manipulated without assigning memory to it.

### PROGRAM 2.6 new and delete operators

```
#include <iostream>
using namespace std;

void main()
{
    // Look at the use of new;
    int *PointerToInt = new int;
    *PointerToInt = 10;
    int *DangerousPointerToInt;
    /* DangerousPointerToInt is a variable that is defined as pointer but is not yet initialized to anything and contains garbage */
    *DangerousPointerToInt = 10;
    int *PointToArrayOfInt = new int[5];
    /* Defines an array of five integers and allocates memory for the same */
    PointToArrayOfInt[2] = 5;
    // Assigns the third element a value 5
    int *PointToInt3 = new int(3);
    // Initializes the content of PointToInt3 to 3 after allocating memory
    cout <<"Explicitly initialized value "<< PointToArrayOfInt[2];
    cout << "\n implicitly initialized at the time of definition" << *PointToInt3;
    int *PointerToArrayOfInt2 = (int *) new int[4][3];
    int FirstDimension = 4;
    int *PointerToArrayOfInt3 = (int *) new int[FirstDimension][3];
    delete PointerToInt;
    delete[]PointToArrayOfInt;
}
```

### How the Program Works

It is necessary to pay attention to some statements of this program. The first one is int *PointerToInt = new int;

This statement allocates sufficient memory for holding an integer value and then the address of that memory location is stored in PointerToInt variable, which, as the name suggests, is a pointer to integer. Next is the following statement:

```
*PointerToInt = 10;
```

The memory to which PointerToInt points to is allocated by a heap manager, which allocates memory from a memory area called heap. Therefore, it is safe to write in that memory area. Now, look at the following statement:

```
*DangerousPointerToInt = 10;
```

This line of code assigns 10 to the content of DangerousPointerToInt. The place at which 10 is written depends on the value of the address pointed to by DangerousPointerToInt.

At the moment, DangerousPointerToInt contains uncertain bits of information, generated from the last usage of the memory area and one cannot be sure of its value. It may be an address of some place in the operating system (OS), a user area, or any place in the memory.

C++ differentiates between a pointer to an array and a pointer to a data type. When a programmer needs to change their usage, casting is required.

If the address belongs to the memory area occupied by the OS, running this program will try to write in a protected area of the OS, which will then crash the program or itself (DOS is known to crash because of such reasons whereas Windows shows a blue screen instead).

If the address belongs to a user area, it leads to two possibilities. It may try to write at a place that is already occupied by something (usually, a variable). The other possibility is that nothing is stored at the place to which the dangerous pointer is currently pointing.

In the first case, when our code inadvertently changes the value of a variable, it generates the wrong output. Though it is a hard error to crack, a clever and experienced developer can debug such an error.

In the second case, when the dangerous pointer points to an area that is empty, nothing wrong happens at the moment, and hence, there is no visual feedback to the programmer that there is something wrong. It is, however, more serious and frustrating because, if something is written later at this area (e.g., when the array size is increased), it may produce strange results. If a compiler initializes the value of such non-initialized pointers to null, there may be a run-time error because the program is trying to write at an undefined or illegal address.

> Note When a pointer is not initialized, it may have strange consequences. For example, variables may start changing their values between assignment statements or the program may behave properly at one instance while not in another. Sometimes such errors crash the program and the programmer gets immediate notification, but it does not happen every time.

Now, have a look at following statements:

```
int *PointerToArrayOfInt2 = (int *) new int[4][3];
int *PointerToArrayOfInt3 = (int *) new int[FirstDimension][3];
```

These are examples of multidimensional arrays being constructed using dynamic allocation. Here, the pointer returned by new needs to be typecast because it returns the pointer to an array of two dimensions, which is different from the pointer to integer in C++.

You can notice the simplicity of the new operator compared to malloc(). It is not necessary to provide the explicit size or the number of bytes; new takes care of both. Typecasting is also not needed because new does return the type of pointer one wants unlike the void pointer returned from malloc(). As shown in Program 2.6, new can also be used to get memory for the whole array and to initialize the value of the content.

```
int* PointToArrayOfInt = new int[5];
/* Getting memory for the whole array */
int * PointToInt3 = new int(3);
/* Initializing the content of PointToInt3 to 3 after allocating memory */
```

The syntax uses array notation [ ] for allocating memory for arrays and uses () for initializing the variable immediately after acquiring memory.

If an old program is being modified, malloc() cannot be replaced with new. This is because unlike malloc(), new does not return null pointer if the memory is not allocated but throws an exception. If a C program has a malloc() function, the function call will have a subsequent test for checking null value.

Unlike malloc(), new does not return null when allocation cannot be performed.

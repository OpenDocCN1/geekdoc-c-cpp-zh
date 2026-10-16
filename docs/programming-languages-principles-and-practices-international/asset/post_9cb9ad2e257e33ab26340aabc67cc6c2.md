
address that cannot be the address of any allocated object, and various C libraries give the name NULL to 0, so that one can write in C:

```
int* x = NULL;
```

Other languages generally reserve a special symbol for this address (null in Java and Ada, nil in Pascal), so that it cannot be used as an identifier.16 With this initialization, x can be tested to see if it points to an allocated object:

```
if (x != NULL) *x = 2;
```

For x to point to an allocated object, we must manually allocate it by the use of an allocation routine. Again, C is unusual in that there is no built-in allocation routine specified by the language, but the stdlib library module contains several functions to allocate and deallocate memory. The most commonly used of these are the malloc (for memory allocation) and free functions. Thus,

```
x = (int*) malloc(sizeof(int));
```

allocates a new integer variable and at the same time assigns its location to be the value of x. The malloc function returns the location it allocates and must be given the size of the data for which it is to allocate space. This can be given in implementation-independent form using the built-in sizeof function, which is given a data type and returns its (implementation-dependent) size. The malloc function must also be cast to the data type of the variable to which its result is being assigned, by putting the data type in parentheses before the function, since the address it returns is an anonymous pointer (a void* in C). (Casts and anonymous pointers are explained in Chapter 8.)

Once x has been assigned the address of an allocated integer variable, this new integer object can be accessed by using the expression *x. The variable x is said to be dereferenced using the unary * operator.17 We can then assign integer values to *x and refer to those values as we would with an ordinary variable, as in:

```
*x = 2;
printf("%d\n",*x);
```

*x can also be deallocated by calling the free procedure, as in:

```
free(x);
```

(Note that dereferencing is not used here, although it is *x that is being freed, not x itself.)

C++ simplifies the dynamic allocation of C by adding built-in operators new and delete, which are reserved names. Thus, the previous code in C++ would become:

```
int* x = new int; // C++
*x = 2;
cout << *x << endl; // output in C++
delete x;
```

16 Though technically, null is a literal, in practice there is little difference between this literal use and that of a reserved word.
17 While this use of * is made to look similar to the way x is defined, this is an entirely different use of the * symbol from its purpose in a declaration.

Note the special syntax in this code—new and delete are used as unary operators, rather than functions, since no parentheses are required. Pascal is similar to C++, only the delete procedure is called dispose.

To allow for arbitrary allocation and deallocation using new and delete (or malloc and free), the environment must have an area in memory from which locations can be allocated in response to calls to new, and to which locations can be returned in response to calls to delete. Such an area is traditionally called a heap (although it has nothing to do with the heap data structure). Allocation on the heap is usually referred to as dynamic allocation, even though allocation of local variables is also dynamic, as we have seen. To distinguish these two forms of dynamic allocation, allocation of local variables according to the stack-based scheme described earlier is sometimes called stack-based or automatic, since it occurs automatically under control of the runtime system. (A more appropriate term for pointer allocation using new and delete might be manual allocation, since it occurs under programmer control.)

In a typical implementation of the environment, the stack (for automatic allocation) and the heap (for dynamic allocation) are kept in different sections of memory, and global variables are also allocated in a separate, static area. Although these three memory sections could be placed anywhere in memory, a common strategy is to place the three adjacent to each other, with the global area first, the stack next, and the heap last, with the heap and stack growing in opposite directions (to avoid stack/heap collisions in case there is no fixed boundary between them). This is usually depicted as shown in Figure 7.32.

![](img/062750ade02e28185b1fb8e8cf6dc89e_300_0.png)

Figure 7.32 Structure of a typical environment with a stack and a heap

```
-- see Chapter 8
(6)    x: Intptr := new Integer;
(7) begin
(8)    x.all := 2;
(9)    put(x.all); new_line;
(10) delete_int(x);
(11) end;
```

Figure 7.33 Ada code showing manual dynamic deallocation

Note how the keyword access is used in Figure 7.33 (line 2) to indicate a pointer, and the dereference operator (line 8 of Figure 7.33) is .all. This comes from the expectation of Ada (as with Java) that heap allocation will be used primarily for record (class) structures. The .all refers to all fields (in our case, there are no fields, only an integer, but one must still use the dereferencer). Unlike Java, Ada does not require x to be a record, however.

To summarize, in a block-structured language with heap allocation, there are three kinds of allocation in the environment: static (for global variables), automatic (for local variables), and dynamic (for heap allocation). These categories are also referred to as the storage class of the variable. Some languages, such as C, allow a declaration to specify a storage class as well as a data type. Typically, this is used in C to change the allocation of a local variable to static:

```
int f(){
static int x;
...
}
```

Now x is allocated only once, and it has the same meaning (and value) in all calls to f. This combination of local scope with global lifetime can be used to preserve local state across calls to f, while at the same time preventing code outside the function from changing this state. For example, Figure 7.34 shows the code for a function in C that returns the number of times it has been called, together with some interesting main program code.

```
(1)  int p(){
(2)    static int p_count = 0;
(3)    /* initialized only once - not each call! */
(4)    p_count += 1;
(5)    return p_count;
(6) }

(7) main(){
(8)    int i;
(9)    for (i = 0; i < 10; i++){
(10)   if (p() % 3) printf("%d\n",p());
(11) }
(12)   return 0;
(13) }
```

Figure 7.34 C program demonstrating the use of a local static variable

## 7.6 Variables and Constants

Although references to variables and constants look the same in many programming languages, their roles and semantics in a program are very different. This section clarifies and distinguishes their basic semantics.

### 7.6.1 Variables

A variable is an object whose stored value can change during execution. A variable can be thought of as being completely specified by its attributes, which include its name, its location, its value, and other attributes such as data type and size of memory storage. A schematic representation of a variable can be drawn as shown in Figure 7.35.

![](img/062750ade02e28185b1fb8e8cf6dc89e_303_0.png)

Figure 7.35 Schematic representation of a variable and its attributes

This picture singles out the name, location, and value of a variable as being its principal attributes. Often we will want to concentrate on these alone, and then we picture a variable in the diagram shown in Figure 7.36, which is known as a box-and-circle diagram.

![](img/062750ade02e28185b1fb8e8cf6dc89e_303_1.png)

Figure 7.36 Schematic representation of a variable, its value, and its location

In a box-and-circle diagram, the line between the name and the location box represents the binding of the name to the location by the environment. The circle inside the box represents the value bound by the memory—that is, the value stored at that location.

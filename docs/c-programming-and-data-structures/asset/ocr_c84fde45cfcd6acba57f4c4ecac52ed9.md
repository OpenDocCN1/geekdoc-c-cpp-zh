# 5.2 Computer Programming

2. The length of a source program can be reduced by using functions at appropriate places. This factor is particularly critical where microcomputers where memory space is limited.

3. It is easy to locate and isolate a faulty function for further investigations.

4. A function may be used by many other programs. This means that a C programmer can build on what others have already done, instead of starting all over again from scratch.

Fig. 5.1 Top—down modular programming using functions

![](bbox=[0.52, 0.55, 0.95, 0.82])

# 5.3 A MULTI-FUNCTION PROGRAM

A function is a self-contained block of code that performs a particular task. Once a function has been designed and packed, it can be treated as a 'black box' that takes some data from the main program and returns a value. The inner details of operation is invisible to the rest of the program. All that the program knows about a function is: What goes in and what comes out. Every C program can be designed using a collection of these black boxes known as functions.

Consider a set of statements as shown below:

```
```c
void printline(void)
{
    int i;
    for (i=1; i<40; i++)
        printf(" ");
    printf("\n");
}
```
```

The above set of statements defines a function called printline, which could print a line of 39-character length. This function can be used in a program as follows:

```
```c
void print (void) /* declaration */
main ()
{
    printline();
    printf("This illustrates the use of C functions\n");
    printline();
}

void printline(void)
{
    int i;
    for(i=1; i<40; i++)
        printf(" ");
    printf("\n");
}
```
```
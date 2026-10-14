item in memory (on the heap or on the stack). A special syntax is used to identify a variable as a pointer. For example, the following statement declares the variable pi as a pointer to an integer:

```
int *pi;
```

Although the variable pi is declared as a pointer, it does not actually point anywhere until you initialize it. For example, to use pi to point to the integer variable i, you can use the following statements and the address-of operator (&), which returns the address of a variable:

```
int *pi;
int i = 99;
...
pi = &i;
```

You can access and modify the value held in the variable i through the pointer variable pi like this:

```
*pi = 100;
```

This code updates the value of the variable i to 100 because pi points to the same memory location as the variable i.

One of the main problems that developers learning C and C++ encounter is understanding the syntax used by pointers. The * operator has at least two meanings (in addition to being the arithmetic multiplication operator), and there is often great confusion about when to use & rather than *. The other issue with pointers is that it is easy to point somewhere invalid, or to forget to point somewhere at all, and then try to reference the data pointed to. The result will be either garbage or a program that fails with an error because the operating system detects an attempt to access an illegal address in memory. There is also a whole range of security flaws in many existing systems resulting from the mismanagement of pointers; some environments (not Windows) fail to enforce checks that a pointer does not refer to memory that belongs to another process, opening up the possibility that confidential data could be compromised.

Reference variables were added to C# to avoid all these problems. If you really want to, you can continue to use pointers in C#, but you must mark the code as unsafe. The unsafe keyword can be used to mark a block of code or an entire method, as shown here:

Click here to view code image

```
public static void Main(string [] args)
{
    int x = 99, y = 100;
    unsafe
    {
```
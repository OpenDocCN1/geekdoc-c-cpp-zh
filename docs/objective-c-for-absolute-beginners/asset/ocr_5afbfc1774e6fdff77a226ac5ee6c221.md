# Allocating Memory

Modern operating systems, the program allocates memory, and the operating system complies by returning a pointer to the requested memory. In C and Objective-C, a pointer is declared by preceding the variable name with an asterisk (*), as shown in the following example:

```
char *theData;
NSString *theString;
```

Don't confused the asterisk here with the **dereference operator**. Only when declaring a variable does the asterisk identify the variable as a pointer.

Here are some more examples of requesting memory:

+   1. char data1[100];
2. char *data2 = malloc(100);
3. NSString *myString = [[NSString alloc] init];

In example 1, memory is allocated in the form of an array declaration. The program now has an array (data1) which **points** to 100 bytes of memory. In C, it's easier to remember that any variable that is declared as an array is **referenced** as an array even though it's not declared as one.

Example 2 is a little more complex. data2 is declared as a pointer to a char data type. A pointer is declared using an asterisk preceding the line the next part of the line is malloc(100), which is a standard C library function call. This function allocates the requested memory and returns a pointer to it. In our example, malloc is passed the value 100. This requests that 100 bytes be allocated. When the function returns, data2 contains a **pointer to** the 100 bytes of memory.

Example 3 is a more traditional Objective-C type memory allocation. First, the program declares a pointer to an NSString class named myString. Next, the following code executes: [[NSString alloc] init]; This will allocate the necessary memory for the object and return a pointer to it.

In all these examples, memory is requested from the operating system and returned to the program via a pointer, even example 1—example is just a little different from the rest.

# Working with Automatic Variables and Pointers

Any variable created within a function or block is considered an **automatic variable**, or **auto-variable**. In our previous examples, example 1 allocates 100 characters as an array. It does so so automatically, as you learned, all variables are auto-variables by default. Because we define the space up front via an array declaration, all this memory is managed automatically for us. Examples 2 and 3 are also auto-variables, but they allocate just enough space to hold a pointer to memory—that's all. Recall that a pointer is just a variable that holds an address to memory; it's not the memory itself. So,
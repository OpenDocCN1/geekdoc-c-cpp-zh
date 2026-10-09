
We already know how to define a function:

```
returnType FunctionName(type parameter1, type parameter2 ...){
        statements that define the function
}
```

To declare a function we simply leave out the body, the block enclosed in curly brackets:

```
returnType FunctionName(type parameter1, type parameter2 ...)
```

Naming the parameters is pointless as the compiler doesn't make use of them, so this can be simplified to:

```
returnType FunctionName(type, type ...)
```

Some programmers prefer the brevity of just listing the types, some think that providing the parameter names informs the reader what the function does, especially so if a comment is used. For example:

```
int sum(int, int);
```

defines the sum function as taking two integers and returning an integer, but

```
int sum(int a, int b); // returns a+b
```

This works when the function is simple, but is less effective as the complexity and number of parameters increases. In most cases it is better to include a brief declaration and leave the comments for the definition.

Once you know about declaring functions, a C program can have a standard form:

```
function declarations
main(){...}
function definitions
```

and to make this even easier to read, it is conventional to put the function declarations into a header file.

```
#include declarations.h
main(){...}
function definitions
```

Things are a little more subtle than this in that the function definitions don't have to be in the same file/compilation unit. By default function declarations are assumed to be extern, i.e. external. This means that if you declare a function and do not define the function within the same file, the linker will look for the function within the libraries that have been specified.

What this means is that by default any function you declare and define in a file can be used from other files. In this sense every function is by default global to the entire project.

If you want to restrict the function to be “local” and defined in the same file prefix the declaration with *static*:

```
static int sum(int, int);
```

this means that the *sum* function has to be defined in the same file and it is not available for use in other compilation units – it is internal to the file. Use *static* in a function declaration when you want to avoid name clashes with functions in any libraries you might be using.

What about variables that are not function pointers, do you need to declare them?

In most cases you can declare and define a variable in the usual way:

```
int myInteger;
```

This allocates the memory needed as well as telling the compiler the type of the variable. Of course, variables have to be declared before they are used, but where they are declared modifies where the memory needed is allocated from. The only example of declaring a variable without defining it is when you declare the variable as *extern*:

```
extern int myInteger;
```

This informs the compiler that *myInteger* is an *int*, but doesn’t allocate any storage for it as it is assumed that this is done in another compilation unit. That is *myInteger* is a variable in another compilation unit (file).

You can declare a variable as many times as necessary, but you can only define it once.

## Function Pointers and Type

The concept of a “first-class function” is a relatively recent one and C’s functions were thought up well before it became an issue. The basic idea is that a first-class function is one that is treated the same as other objects in the language. Where “objects” can mean simple things like ints or floats or bigger things like class-derived instances of complex data structures. However, the key feature when a function is “first-class” is the ability to pass it as a parameter to another function and C has allowed this from the start.

A function name is a pointer to the starting address of the function. If you write:

```
printf("Address = %X",&myFunction);
```

or

```
printf("Address = %X",myFunction);
```

you will see the address that *myFunction* starts at. In other words the *&* is optional when dealing with a function name.

What this means is that you can pass a function, using its name, to another function and then call it from within that function. The only problem we have is, what type is a function? To define a parameter as accepting a particular function, we need to be able to define the type of a function. The type of a function is simply a pointer to a function.

This is easy in principle, but slightly difficult to read:

```
function return type (*function name)(parameter types);
```

So, for example:

```
int (*myFunction)(int,int);
```

defines a function that returns an int and accepts two ints as parameters. Notice that this is similar to the usual function declaration:

```
int myFunction(int a, int b);
```

When you create a type for a function you can include parameter names if you want to. Notice that the parentheses around the function name are necessary as:

```
int *myFunction(int a, int b)
```

is a function that returns a pointer to int.

To be clear:

```
int (*myFunction)(int,int);
```

defines the variable myFunction to be a pointer to a function that accepts two ints and returns an int. Notice that the name of the pointer isn’t at the end of the declaration as it usually is – this makes reading such declarations more difficult.

For example:

```
int (*myFunctionPointer) (int,int);
myFunctionPointer=sum;
int result=myFunctionPointer(1,2);
```

The function pointer can be set to reference the function sum as it has the same signature. Once you have a function pointer, you can use it to call the function in the normal way.

As function types are complicated to read, it is usually better to define a type using typedef. In this case the name supplied is used as the name of the type:

```
typedef int (*myFnctype) (int,int) ;
myFnctype myFunctionPointer;
myFunctionPointer=sum;
int result3=myFunctionPointer(1,2);
```

Notice that the name of the type defined by the typedef isn’t at the end of the statement which is where you usually look for it. However the declaration of the function pointer is now more usual in that the name of the variable is at the end rather than in the middle.

Notice that any function that matches the type in terms of the number and type of its parameters and return type can be considered to be of that type. You can even define multiple identical, but differently-named, types and they will all be treated as the same.

You cannot use a raw function pointer to define a function. That is you cannot write:

```
int (*myFunction)(int a,int b)
{
    return a+b;
}
```

You have to define a function and then assign it to the function pointer.

### Function Parameters and Return Types

You can use a function pointer as a parameter in a function so that you can pass a function into another function as an argument.

For example:

```
void myFunction(int (*myFuncParm)(int,int)){
    printf("%d\n",myFuncParm(1,2));
}
```

and again notice that the name of the parameter, `myFuncParm`, is not at the end of the type specification.

This can be made much easier to read with the help of a `typedef`:

```
typedef int (*myFuncType) (int,int);

void myFunction(myFuncType myFunction){
    printf("%d\n",myFunction(1,2));
}
```

Defining the type of the return as a function pointer is messy, but it is rarely needed as C functions are not dynamic. That is, a function cannot create a function and return it. What this means is that a function that returns a function can only return a function that already exists and is in scope.

To define the return type of a function as a function you have to supply the type in front of the function definition as usual but in this case the type includes the name of the function.

```
return type (*name of function(parameters1)) (parameters2)
```

where the function returned has type:

```
return type (*)(parameters2);
```

and the function being defined is:

```
name of function(parameters1)
```

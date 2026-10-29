When something is “thrown,” something goes from one place to another place. In C++, what goes from one place to another is the flow of control (as well as the value thrown). When an exception is thrown, the code in the surrounding try block stops executing, and another portion of code, known as a catch block, begins execution. Executing the catch block is called catching the exception or handling the exception. When an exception is thrown, it should ultimately be handled by (caught by) some catch block. In Display 18.2, the appropriate catch block immediately follows the try block. We repeat the catch block in what follows:

```
```cpp
catch (int e)
{
    cout << e << " donuts, and No Milk!\n"
         << "Go buy some milk.\n";
}
```
```

This catch block looks very much like a function definition that has a parameter of type int. It is not a function definition, but in some ways a catch block is like a function. It is a separate piece of code that is executed when your program encounters (and executes) the following (within the preceding try block):

```
```cpp
throw Some_int;
```
```

So, this throw statement is similar to a function call, but instead of calling a function, it calls the catch block and says to execute the code in the catch block. A catch block is often referred to as an exception handler, which is a term that suggests that a catch block has a function-like nature.

What is that identifier e in the following line from a catch block?

```
```cpp
catch (int e)
```
```

That identifier e looks like a parameter and acts very much like a parameter. In fact, the identifier, such as e, in the catch-block heading is called the catch-block parameter. Each catch block can have at most one catch-block parameter. The catch-block parameter does two things:

+   1. The catch-block parameter is preceded by a type name that specifies what kind of thrown value the catch block can catch.
+   2. The catch-block parameter gives you a name for the thrown value that is caught, so you can write code in the catch block that does things with that value.

We will discuss these two functions of the catch-block parameter in reverse order. This subsection discusses using the catch-block parameter as a name for the value that was thrown and is caught. The subsection entitled “Multiple Throws and Catches,” later in this chapter, discusses which catch block (which exception handler) will process a value that is thrown. Our current example has only one catch block. A common name for a catch-block parameter is e, but you can use any legal identifier in place of e.

Let us see how the catch block in Display 18.2 works. When a value is thrown, execution of the code in the try block ends and control passes to the catch block (or
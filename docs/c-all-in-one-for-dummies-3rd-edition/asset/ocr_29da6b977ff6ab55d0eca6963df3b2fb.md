![](bbox=[0.115, 0.128, 0.205, 0.2])

If you want to use the -M option to generate your dependencies (but only want to list the header files in your project and not all those other bizarre ones that live inside the main include directory), you can throw in an extra *M*:

```
```
g++ -MM main.cpp
```
```

When we run this, we see only the header files in our project. Here’s the output we get:

```
```
main.o: main.cpp main.h
```
```

Often, this is more useful because it’s rare that the system header files change.

# ### Compiling and linking with make

To really use make in your projects, you need rules that tell make to run the compiler. For each of your source code files, you want to build an object file; and from there, you want to link the object files into a single executable. You can write a `Makefile` that specifies these rules, such as the following:

```
```
mystuff.o: mystuff.cpp
        g++ -c mystuff.cpp -o mystuff.o
```
```

The first line says that our object file depends on the source file. The second line is the command to run to create the object file.

Linking is a bit more complex because to successfully link an application, you need to include several libraries. Which libraries you include depends on which compiler you use.

The beauty of using `Makefile`, however, is that after the information for compiling and linking is there, you don’t need to do anything else. When it’s time to build your application, you simply type

```
```
make
```
```

![](bbox=[0.085, 0.71, 0.195, 0.79])

Certainly, you will be compiling and linking. Remember that with `Makefiles`, the best way to use them is to simply understand them. That way, you can take an existing one and fix them up so that they work with your particular project. Writing one from scratch requires a strong knowledge of the intricate workings of the inference rules. Toward the end of this appendix (in the sidebar “Discovering more about make”), we tell you where you can find that information if you really want to study it.
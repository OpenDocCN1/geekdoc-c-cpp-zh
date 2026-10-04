# 294 Modularity Using Functions

The engine, transmission, and other modules "know" only the universe bounded by their inputs and outputs. The driver doesn't need to know the internal operation of the modules being called. All that's required is understanding what each unit does and how to use it. The driver simply "calls" on a module, such as the brakes, when that module's output is required. Communication between modules is restricted to passing inputs to each module as it's called to perform its task, and each module operates in a fairly independent manner. Programmers use this modular approach to create and maintain maintainable C++ programs using functions.

As you have seen, each C++ program must contain a main() function. In addition to this required function, C++ programs can also contain any number of other functions. In this chapter, you learn how to write these functions, pass data to them, process the passed data, and return a result.

# 6.1 Function and Parameter Declarations

In creating C++ functions, you must be concerned with the function itself and how it interacts with other functions, such as main(). Interaction with a function involves passing data to a function correctly when it's called and returning values from a function when it ceases operation. This section describes the first part of the interface, passing data to a function and having the function receive, store, and process the transmitted data correctly.

As you have already seen with mathematical functions, a function is called, or used, or by giving the function name in the parentheses (see Figure 6.1). The called function must be able to accept the data passed to it by the function doing the calling. Only after the called function receives the data successfully can the data be manipulated to produce a useful result.

```
function-name (data passed to function):
This identifies This passes data to the called function
```

Figure 6.1 Calling and passing data to a function

To clarify the process of sending and receiving data, take a look at Program 6.1, which calls a function named findMax(). The program, as shown, is not yet complete. After the function findMax() is written and included in Program 6.1, the completed program, consisting of the functions main() and findMax(), can be compiled and executed.
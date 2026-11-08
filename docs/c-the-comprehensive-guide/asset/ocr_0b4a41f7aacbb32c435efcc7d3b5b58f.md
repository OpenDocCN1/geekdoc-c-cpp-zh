# Chapter 3

# C++ for Newcomers

This chapter is primarily aimed at those transitioning from Java or C#, but newcomers from other higher-level languages, especially object-oriented languages, will also benefit, as will those refreshing their C++ skills after some time. I provide a general overview of the idiosyncrasies of C++ that may surprise or pose difficulties for newcomers.

All other readers can skip this chapter; the overview and introduction follow.

The following elements are ones that many developers should recognize:

+   - **Statements**  
+     Programs are executed statement by statement, one after the other—at least per thread, at least in the model. The rule of thumb is that semicolons separate statements from each other. Statements can be combined into blocks.
+   
+   - **Expressions**  
+     An expression recursively consists of expressions down to indivisible units such as literals or variables. Arithmetic expressions contain mathematical calculations, for example. In C++, an exact type can be assigned to every expression.
+   
+   - **Data types**  
+     C++ offers a range of simple data types such as `int` and `double`. There are also pointers and references, which are separate types in C++. An `int` and a pointer to `int*` are different types. You can aggregate several types together to obtain new types.
+   
+   - **Functions and methods**  
+     To prevent programs from turning into long spaghetti, reused areas can be outsourced to functions. Functions that are in a data type are called *methods*.
+   
+   - **Classes**  
+     Data types that you also bundle with behavior—that is, to which you add methods—are called *classes*.
+   
+   - **Function calls**  
+     A function call takes parameters and returns a result. What happens within the function is partially invisible from the outside.
+   
+   - **Parameters**  
+     Functions receive parameters. In C++, the function decides whether the parameter is to be used as a value (*by value*) or as a reference—or pointer (*by reference*)—not the caller.
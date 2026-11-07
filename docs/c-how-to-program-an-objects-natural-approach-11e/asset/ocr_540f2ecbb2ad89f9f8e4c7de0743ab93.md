When a conversion constructor or conversion operator is used to perform an implicit conversion, C++ can apply only one implicit constructor or operator function call (i.e., a single user-defined conversion) per expression to try to match the needs of that expression. The compiler will not satisfy an expression's needs by performing a series of implicit, user-defined conversions.

# ### Checkpoint

+   1. *(Fill-in)* ________ constructors enable the compiler to convert among user-defined types or between user-defined types and fundamental types.  
+      **Answer:** conversion.
+   2. *(True/False)* The compiler can use cast operators and conversion constructors implicitly to create objects.  
+      **Answer:** True.
+   3. *(True/False)* C++ can satisfy an expression's needs by performing a series of implicit, user-defined conversions.  
+      **Answer:** False. Actually, C++ can apply only one user-defined conversion per expression.

# ## 11.9 explicit Constructors and Conversion Operators

Recall that we've been declaring as `explicit` every constructor that can be called with one argument, including multiparameter constructors for which we specify default arguments. Except for copy and move constructors, any constructor that can be called with a *single argument* and is not declared `explicit` can be used by the compiler to perform an *implicit conversion*. The constructor's argument is converted to an object of the class in which the constructor is defined. The conversion is automatic—a cast is not required.

In some situations, implicit conversions are undesirable or error-prone. For example, our `MyArray` class defines a constructor that takes a single `size_t` argument. The intent of this constructor is to create a `MyArray` object containing a specified number of elements. However, if this constructor were not declared `explicit`, it could be misused by the compiler to perform an implicit conversion.

Unfortunately, the compiler might use implicit conversions in cases that you do not expect, resulting in execution-time logic errors or ambiguous expressions that generate compilation errors.

# ### Accidentally Using a Single-Argument Constructor as a Conversion Constructor

The program (Fig. 11.7) uses Section 11.6's `MyArray` class to demonstrate an improper implicit conversion. To allow this implicit conversion, we removed the `explicit` keyword from line 16 in `MyArray.h` (Fig. 11.4).
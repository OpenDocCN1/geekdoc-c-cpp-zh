# Pitfall
COMPILER COMPLICATIONS

Many compilers do not allow separate compilation of templates, so you may need to include your template definition with your code that uses it. As usual, at least the function declaration must precede any use of the function template.

Some C++ compilers have additional special requirements for using templates. If you have trouble compiling your templates, check your manuals or check with a local expert. You may need to set special options or rearrange the way you order the template definitions and the other items in your files.

The template program layout that seems to work with the widest selection of compilers is the following: Place the template definition in the same file in which it is used and have the template definition precede all uses (all invocations) of the template. If you want to place your function template definition in a file separate from your application program, you can #include the file with the function template definition in the application file.

# Self-Test Exercises

+   1. Write a function template named maximum. The function takes two values of the same type as its arguments and returns the larger of the two arguments (or either value if they are equal). Give both the function declaration and the function definition for the template. You will use the operator < in your definition. Therefore, this function template will apply only to types for which < is defined. Write a comment for the function declaration that explains this restriction.

+   2. We have used three kinds of absolute value function: abs, labs, and fabs. These functions differ only in the type of their argument. It might be better to have a function template for the absolute value function. Give a function template for an absolute value function called absolute. The template will apply only to types for which < is defined, for which the unary negation operator is defined, and for which the constant 0 can be used in a comparison with a value of that type. Thus, the function absolute can be called with any of the number types, such as int, long, and double. Give both the function declaration and the function definition for the template.

+   3. Define or characterize the template facility for C++.

+   4. In the template prefix
+   ```
+   template <class T>
+   ```
+   what kind of variable is the parameter T? Choose from the answers listed below.
+   a. T must be a class.
+   b. T must not be a class.
+   c. T can be only a type built into the C++ language.
+   d. T can be any type, whether built into C++ or defined by the programmer.
+   e. T can be any kind of type, whether built into C++ or defined by the programmer, but T does have some requirements that must be met. (What are they?)
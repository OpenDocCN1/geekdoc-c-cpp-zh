case. Usually your default case will generate an error by using a **throw** statement. Simply printing an error (as happens in our example) is a bad idea.

# ## 4.7 Scope

The flow of control statements above make use of curly brackets. If you define a variable within curly brackets, it can only be used within those brackets. Once the execution of the program leaves the brackets, the variable is deleted. The part of the code in which you can refer to a variable is called the *scope* of the variable.

Here is an example code snippet that computes the sum of the squares of the first 10 integers (starting from 0, of course).

```
```
int n=0;
int total;
for (int i=0; i<10; i++) {
    int squareValue = i*i;
    total += squareValue;
}
std::cout << n;
// std::cout << squareValue;
// std::cout << i;
```
```

The variable *squareValue* is only valid within the curly brackets. The variable *i* is only valid within the for statement itself and within the curly brackets. If you were to try to remove the comment characters `//` on the last two lines, the code would not compile.

The scope of variables is used to control the use of memory in C++. When variables go out of scope, the memory can be safely reused. Often you won’t need to think about the memory management in C++. However, there are times when you will want to take control of memory management yourself. We will discuss this in Chapter 11.

# ## 4.8 Flow of control in operators

A technical point is that certain operators in C++ actually control the flow of the program in subtle ways.
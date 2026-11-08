What is the output of each of the following program segments?

```
a. `cout << find(15) << endl;`

b. `cout << discover(3, 9) << endl;`

c. `cout << find(10) << " " << discover(10, find(10)) << endl;`

d. `x = 12; y = 8;`
   `cout << discover(y, x) << endl;`
```

9. Consider the following function prototypes:

```
int func1(int, double);
double func2(string, int, double);
char func3(int, int, double, char);
string join(string, string);
```

Answer the following questions:

+   a. How many parameters does the function func1 have? What is the type of the function func1?
+   
+   b. How many parameters does function func2 have? What is the type of the function func2?
+   
+   c. How many parameters does function func3 have? What is the type of the function func3?
+   
+   d. How many parameters does function join have? What is the type of the function join?
+   
+   e. How many actual parameters are needed to call the function func1? What is the type of each actual parameter, and in what order should you use these parameters in a call to the function func1?
+   
+   f. Write a C++ statement that prints the value returned by the function func1 with the actual parameters 3 and 8.5.
+   
+   g. Write a C++ statement that prints the value returned by function join with the actual parameters "John" and "Project Manager", respectively.
+   
+   h. Write a C++ statement that prints the next character returned by function func3. (Use your own actual parameters.)

10. Why do you need to include function prototypes in a program that contains user-defined functions?

11. Write the definition of a function that takes as input a char value and returns true if the character is uppercase; otherwise, it returns false.

12. Consider the following function:

```
int mystery(int x, double y, char ch)
{
    if (x == 0 && ch > 'A')
        return(static_cast<int>(pow(y, 2)) + static_cast<int>(ch));
    else if (x > 0)
        return(x + static_cast<int>(sqrt(y)) - static_cast<int>(ch));
}
```
```
```cpp
if (second > 50)
    num1 = first / 10;
else
    num2 = second / 20;

return num1 + num2;
}
int discover(int one, int two)
{
    int secret = 1;
    for (int i = one; i < two; i++)
        secret = secret * i;

    return secret;
}
```
```

What is the output of each of the following program segments?

+   a. `cout << find(15, 25) << endl;`
+   
+   b. `cout << discover(3, 9) << endl;`
+   
+   c. `cout<<find(10, 10)<<" "<<discover(10, find(10, 10))<<endl;`
+   
+   d. `x = 20; y = 10;`
+      `cout << discover(x, y) << endl;`

9. Consider the following function prototypes:

```
```cpp
int func1(int, double);
double func2(string, int, double);
char func3(int, int, double, char);
string join(string, string);
```
```

Answer the following questions: (3, 4)

+   a. How many parameters does the function func1 have? What is the type of the function func1?
+   
+   b. How many parameters does function func2 have? What is the type of the function func2?
+   
+   c. How many parameters does function func3 have? What is the type of function func3?
+   
+   d. How many parameters does the function join have? What is the type of function join?
+   
+   e. How many actual parameters are needed to call the function func1? What is the type of each actual parameter, and in what order should you use these parameters in a call to the function func1?
+   
+   f. Write a C++ statement that prints the value returned by the function func1 with the actual parameters 3 and 8.5.
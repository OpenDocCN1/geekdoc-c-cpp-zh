# Answers to Self-Test Exercises

+   1. Hello
+   Goodbye
+   One more time:
+   Hello
+   End of program.

2. No, a void function definition need not contain a return statement. A void function definition may contain a return statement, but one is not required.

3. Omitting the return statement in the function definition for initializeScreen in Display 5.2 would have absolutely no effect on how the program behaves. The program will compile, run, and behave exactly the same. Similarly, omitting the return statement in the function definition for showResults also will have no effect on how the program behaves. However, if you omit the return statement in the function definition for celsius, that will be a serious error that will keep the program from running. The difference is that the functions initializeScreen and showResults are void functions, but celsius is not a void function.

```
4. #include <iostream>

void productOut(int n1, int n2, int n3);
int main()
{
    using namespace std;
    int num1, num2, num3;
    cout << "Enter three integers: ";
    cin >> num1 >> num2 >> num3;
    productOut(num1, num2, num3);
    return 0;
}

void productOut(int n1, int n2, int n3)
{
    using namespace std;
    cout << "The product of the three numbers "
         << n1 << ", " << n2 << ", and "
         << n3 << " is " << (n1 * n2 * n3) << endl;
}
```

5. These answers are system dependent.

6. A call to a void function followed by a semicolon is a statement. A call to a function that returns a value is an expression.
```
18: {
19:     cout << "Argument in function is " << num << endl;
20: }
```

In the preceding code snippet, we loop over a set of instructions for five times and prompt a user to input five different values that are printed in the function. This shows how arguments can be passed from one function to another and accessed from there.

Following is the output of the preceding code snippet:

```
I'm in Main
Enter a number: 5
Argument in function is 5
Enter a number: 9
Argument in function is 9
Enter a number: 45
Argument in function is 45
Enter a number: 234
Argument in function is 234
Enter a number: 56
Argument in function is 56
I'm in Main again
```

Similarly, we can pass any other data type variable (float, double, and char) or user-defined variable (classes and structures) as an argument to a function.

+   - **References—** A reference provides an alias, that is, a different name for a variable. One of the most important uses for references is in passing arguments to functions. As already learned, we can pass arguments to functions using two methods: pass by reference and pass by value. When we pass arguments by reference, the formal arguments (variables found in the function definition) in the called function become aliases to the actual arguments (values passed in the calling function). This means that when the function is working with its own arguments, it is actually working on the original data. On the other hand, when we pass arguments by value, the call to the function creates a new set of variables and copies the values of the arguments into them before starting the execution. The following program demonstrates the difference between the two methods by swapping data between two variables:

```
1:  //Demonstrating functions in C++ with pass by reference
2:  #include <iostream>
3:  using namespace std;
4:
5:  void swap_ref(int& a, int& b);
6:  void swap_value(int x, int y);
7:
8:  int main()
9:  {
10:         int x = 5, y = 10;
11:         cout<<"Calling function with pass by value."<<endl;
12:         cout<<"Before swap_value: x= "<<x<<" y= "<<y<<endl;
13:         swap_value (x, y);
14:         cout<<"After swap_value: x= "<<x<<" y= "<<y<<endl;
15:         cout<<"Calling function with pass by reference."<<endl;
16:         cout<<"Before swap_ref: x= "<<x<<" y= "<<y<<endl;
17:         swap_ref (x, y);
18:         cout<<"After swap_ref: x= "<<x<<" y= "<<y<<endl;
19:  return 0;
20: }
21:
```
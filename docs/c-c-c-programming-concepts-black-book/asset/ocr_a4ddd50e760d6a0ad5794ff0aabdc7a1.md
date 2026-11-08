```
```cpp
22: void swap_value(int x, int y)
23: {
24:     int temp = x;
25:             x = y;
26:             y = temp;
27: }
28: void swap_ref(int& a, int& b)
29: {
30:     int temp = a;
31:             a = b;
32:             b = temp;
33: }
```
```

As shown in the preceding program, we have taken two local variables x and y and assigned them some initial values in the main() function. In addition, we have defined two functions in the program: swap_value and swap_ref. The swap_value function takes two integers as arguments and swaps the value between them; whereas, the swap_ref function takes arguments as reference to two integers and swaps the value between them. Following is the output of the preceding program:

```
```text
Calling Function with pass by value.
Before swap_value: x= 5 y= 10
After swap_value: x= 5 y= 10
Calling Function with pass by reference.
Before swap_ref: x= 5 y= 10
After swap_ref: x= 10 y= 5
```
```

Now, we will move on to the next section on functions with default arguments.

# ## Default Arguments in Function

In the previous section, we have learned about functions and different types of arguments to functions. It is very interesting to know that in C++, we can make a call to a function without specifying all its arguments; however, this does not work with just any function. To make a function work with default arguments, we must specify default values to the function parameters, which does not have matching arguments in the function call, at the time of function declaration. The compiler checks the prototype for the number of arguments that a function uses and alerts the program for possible default values. Let's demonstrate this with the help of the following example:

```
```cpp
float simple_interest(float p, int n, float r = 11);
```
```

In the preceding function declaration, we will be calculating the simple interest, with principle amount, time in years, and rate. The value of rate is set at default to 11, so users can ignore this if they want the rate to be 11%; else, they might supply another rate value. In this case, calculation will be made using the value given by the user. Let's write the following program to observe how it behaves with default arguments:

```
```cpp
1: //Demonstrating a C++ program calculating simple interest with default arguments
2: #include <iostream>
3: using namespace std;
4: 
5: float simple_interest (float p, int n, float r = 11);
6: 
7: int main ()
8: {
9:     float amount;
10:            amount = simple_interest (1000, 1);
11:            cout<<"Amount after simple interest addition is "<<amount<<endl;
12:            amount = simple_interest (2000, 3, 15);
13:            cout<<"Amount after simple interest addition is "<<amount<<endl;
```
```
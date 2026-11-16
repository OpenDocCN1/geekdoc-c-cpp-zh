```
cout<<add(5,6);
}
int add(int x,int y)
{
 return x+y;
}
```

Output
3
7
11

See here, In the first call to the function since we have not passed any value, so automatically 1 and 2 which was used in function declaration was taken. In the second calling we have passed a value, so this value was considered as first argument and so 5 and 2 was added to give 7. Then in third calling we passed both the arguments to the function, So the result 11 was returned.

See the function declaration contains the default arguments, not the function definition.

# Function overloading

C++ has the capacity to differentiate different functions on the basis of type of arguments being passed to them. This gives us the power to use many functions with the same name.

Consider the following program:

```
#include<iostream>
using namespace std;
void disp();
void disp(int);
void disp(char);
void disp(int,char);
int main()
```
particular, the function definition for equal shown in Display 11.2 does not include the qualifier DayOfYear:: in the function heading. Also, the equal function is not called by using the dot operator. The function equal takes objects of type DayOfYear as arguments the same way that any other nonmember function would take arguments of any other type. However, a friend function definition can access the private member variables and private member functions of the class by name, so it has the same access privileges as a member function.

# PROGRAMMING TIP Define Both Accessor Functions and Friend Functions

It may seem that if you make all your basic functions friends of a class, then there is no need to include accessor and mutator functions in the class. After all, friend functions have access to the private member variables and so do not need accessor or mutator functions. This is not entirely wrong. It is true that if you made all the functions in the world friends of a class, you would not need accessor or mutator functions. However, making all functions friends is not practical.

In order to see why you still need accessor functions, consider the example of the class DayOfYear given in Display 11.2. You might use this class in another program, and that other program might very well want to do something with the month part of a DayOfYear object. For example, the program might want to calculate how many months there are remaining in the year. Specifically, the main part of the program might contain the following:

```
DayOfYear today;
cout << "enter today's date: \n";
today.input();
cout << "There are " << (12 - today.getMonth())
    << " months left in this year.\n";
```

You cannot replace today.getMonth() with today.month because month is a private member of the class. You need the accessor function getMonth.

You have just seen that you definitely need to include accessor functions in your class. Other cases require mutator functions. You may think that, because you usually need accessor and mutator functions, you do not need friends. In a sense, that is true. Notice that you could define the function equal either as a friend without using accessor functions (Display 11.2) or not as a friend and use accessor functions (as in Display 11.1). In most situations, the only reason to make a function a friend is to make the definition of the function simpler and more efficient; but sometimes, that is reason enough.
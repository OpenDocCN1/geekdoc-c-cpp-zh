
After these statements execute, the objects and static members are as shown in Figure 10-13.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_719_0.png)

**FIGURE 10-13** illusObject1 and illusObject2 after the statements `illustrate::incrementY();` and `illustrate::count++;` execute

The output of the statement:

```
illusObject1.print();
```

is:

```
x = 3, y = 1, count = 1
```

Similarly, the output of the statement:

```
illusObject2.print();
```

is:

```
x = 5, y = 1, count = 1
```

Now consider the statement:

```
illustrate::count++;
```

After this statement executes, the objects and static members are as shown in Figure 10-14.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_719_1.png)

**FIGURE 10-14** illusObject1 and illusObject2 after the statement `illustrate::count++;` executes

The output of the statements:

```
illusObject1.print();
illusObject2.print();
```

is:

```
x = 3, y = 1, count = 2
x = 5, y = 1, count = 2
```

The program in Example 10-12 further illustrates how static members of a class work.

## EXAMPLE 10-12

```cpp
#include <iostream>

#include "illustrate.h"

using namespace std;

int main()
{
    illustrate illusObject1(3);                 //Line 1
    illustrate illusObject2(5);                 //Line 2

    illustrate::incrementY();                   //Line 3
    illustrate::count++;                        //Line 4
    illusObject1.print();                       //Line 5
    illusObject2.print();                       //Line 6
    cout << "Line 7: ***Increment y using "
         << "illusObject1***" << endl;         //Line 7

    illusObject1.incrementY();                  //Line 8
    illusObject1.setX(8);                       //Line 9
    illusObject1.print();                       //Line 10
    illusObject2.print();                       //Line 11

    cout << "Line 12: ***Increment y using "
         << "illusObject2***" << endl;         //Line 12

    illusObject2.incrementY();                  //Line 13
    illusObject2.setX(23);                      //Line 14
    illusObject1.print();                       //Line 15
    illusObject2.print();                       //Line 16

    return 0;
}
```

### Sample Run:

```
x = 3, y = 1, count = 1
x = 5, y = 1, count = 1
Line 7: ***Increment y using illusObject1***
x = 8, y = 2, count = 1
x = 5, y = 2, count = 1
Line 12: ***Increment y using illusObject2***
x = 8, y = 3, count = 1
x = 23, y = 3, count = 1
```

The preceding program works as follows. The static member variables y and count are initialized to 0. The statement in Line 1 declares illusObject1 to be an object of the class illustrate and initializes its member variable x to 3. The statement in Line 2 declares illusObject2 to be an object of the class illustrate and initializes its member variable x to 5.

The statement in Line 3 uses the name of the class illustrate and the function incrementY to increment y. Now, count is a public static member of the class illustrate. So the statement in Line 4 uses the name of the class illustrate to directly access count and increment it by 1. The statements in Lines 5 and 6 output the data stored in the objects illusObject1 and illusObject2. Notice that the value of y for both objects is the same. Similarly, the value of count for both objects is the same.

The statement in Line 7 is an output statement. The statement in Line 8 uses the object illusObject1 and the function incrementY to increment y. The statement in Line 9 sets the value of the member variable x of illusObject1 to 8. Lines 10 and 11 output the data stored in the objects illusObject1 and illusObject2. Notice that the value of y for both objects is the same. Similarly, the value of count for both objects is the same. Moreover, notice that the statement in Line 9 changes only the value of the member variable x of illusObject1 because x is not a static member of the class illustrate.

The statement in Line 13 uses the object illusObject2 and the function incrementY to increment y. The statement in Line 14 sets the value of the member variable x of illusObject2 to 23. Lines 15 and 16 output the data stored in the objects illusObject1 and illusObject2. Notice that the value of y for both objects is the same. Similarly, the value of count for both objects is the same. Moreover, notice that the statement in Line 14 changes only the value of the member variable x of illusObject2, because x is not a static member of the class illustrate.

Here are some additional comments on *static* members of a class. As you have seen in this section, a *static* member function of a class does not need any object to be invoked. It can be called using the name of the class and the scope resolution operator, as illustrated. Therefore, a *static* member function cannot use anything that depends on a calling object. In other words, in the definition of a *static* member function, you cannot use a non-static member variable or a non-static function unless there is an object declared locally that accesses the non-static member variable or the non-static member function.

Let us again consider the class illustrate, as defined in Example 10-11. This class contains both static and non-static member variables. When we declare objects of this class, each object has its own copy of the member variable $x$, which is non-static, and all objects share the member variables $y$ and count, which are static. Earlier in this chapter, we defined the terminology instance variables of a class using the class clockType. However, at that point, we did not discuss static member variables of a class. A class can have static as well as non-static member variables. We can, therefore, make the general statement that non-static member variables of a class are called the instance variables of the class.

## PROGRAMMING EXAMPLE: Juice Machine

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_722_0.png)

A common place to buy juice is from a machine. A new juice machine has been purchased for the gym, but it is not working properly. The machine sells the following types of juices: orange, apple, mango, and strawberry-banana. You have been asked to write a program for this juice machine so that it can be put into operation.

The program should do the following:

- 1. Show the customer the different products sold by the juice machine.
- 2. Let the customer make the selection.
- 3. Show the customer the cost of the item selected.
- 4. Accept money from the customer.
- 5. Release the item.

**Input** The item selection and the cost of the item.

**Output** The selected item.

A juice machine has two main components: a built-in cash register and several dispensers to hold and release the products.

## PROBLEM ANALYSIS AND ALGORITHM DESIGN

### Cash Register

Let us first discuss the properties of a cash register. The register has some cash on hand, it accepts the amount from the customer, and if the amount deposited is more than the cost of the item, then—if possible—it returns the change. For simplicity, we assume that the user deposits the money greater than or equal to the cost of the product. The cash register should also be able to show to the juice machine’s owner the amount of money in the register at any given time. The following class defines the properties of a cash register:

```cpp
class cashRegister
{
public:
    int getCurrentBalance() const;
        //Function to show the current amount in the cash
        //register.
        //Postcondition: The value of cashOnHand is returned.

    void acceptAmount(int amount);
        //Function to receive the amount deposited by
        //the customer and place the amount in the register.
        //Postcondition: cashOnHand = cashOnHand + amount;

    cashRegister(int cashIn = 500);
        //Constructor
        //Sets the cash in the register to a specific amount.
        //Postcondition: cashOnHand = cashIn;
        //              If no value is specified when the
        //              object is declared, the default value
        //              assigned to cashOnHand is 500.

private:
    int cashOnHand;  //variable to store the cash
                    //in the register
};
```

Figure 10-15 shows the UML class diagram of the class cashRegister.

![](img/dc1b115c1ae2ec0d8a557b7c2b830e8c_723_0.png)

**FIGURE 10-15** UML class diagram of the class cashRegister

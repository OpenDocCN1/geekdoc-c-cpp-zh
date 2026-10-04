
// Program 17_3
// Vending Machine non-default constructor
#include <iostream>
using namespace std;

class vending_machine {
private:
    float price;
    float credit;
    float money_collected;
    int inventory;

public:
    vending_machine() {
        price = 1.0;
        credit = 0.0;
        money_collected = 0.0;
        inventory = 100;
    }

    vending_machine(int starting_inventory) {
        price = 1.0;
        credit = 0.0;
        money_collected = 0.0;
        inventory = starting_inventory;
        cout << "Created a new vending machine." << endl;
    }

    int number_remaining() {
        return inventory;
    }
};

int main() {
    vending_machine lobby_machine(50);
    cout << "There are " << lobby_machine.number_remaining() << " items." << endl;
}

## Exercise

Write a constructor that takes in both an item price and an initial level of inventory and call that to create a vending_machine that has 75 items, costing $5 each.

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_194_0.png)

Let's see how you could define a new constructor for your vending_machine.

Suppose you want to be able to specify a specific inventory level, rather than a default level, at the object is allocated. In case, you'd want a constructor that takes in one integer parameter. Remember, this is no longer the default constructor—but a new constructor.

Again, the name is just the class, but now it takes in a single integer, starting_inventory (22). And the function itself sets all the other values to its defaults, but sets the inventory to parameter value that should be passed in (26).

When declaring a new vending_machine, you give the variable name, which in case is again lobby_machine, but also parentheses in which you have a single integer argument (38). Then, when you run this program, the new constructor—default will be used to initialize the object.

So, in this case, you passed 50 as an argument when you declared the vending_machine, you have an initial inventory level of 50.

You can pass in arguments that are variables just as easily as other values. In this case, you read in from a user of initial items that the machine should be stocked with. Then, you can declare a vending machine with that number.

Notice that this sort of initialization could not occur if variables were just set to default values by assignment statements in the class declaration.

```
int main() {
    cout << "How many items does the machine start with? " << endl;
    int init_number;
    cin >> init_number;
    vending_machine lobby_machine(init_number);
    cout << "There are " << lobby_machine.number_remaining() << " items." << endl;
}
```

> Be aware that you should not try to declare an object using the default constructor by just using parentheses with no arguments. If you're using the default constructor, just leave off the parentheses entirely. Only use parentheses when you want to use a non-default constructor or when you're declaring the constructor within the class.

## // OPERATOR OVERLOADING

You have already frequently encountered function overloading, where you can use the same function name but take different parameters to get different behavior. **Operator overloading** is similar, but you take different operands to get different behavior from **operator**.

You've already seen examples of operator overloading. You've seen how + can be used for addition for numbers or concatenation for string types. The operator has "overloaded" to take on more than one meaning; it has different meanings depending on the implementation.

When you have the stream operator to output a floating-point number, it behaves one way: It analyzes the number and displays the digits of the number with the decimal point in the correct position. When you use the streaming operator to output a string, it behaves a different way: It analyzes the array of characters kept in the string and outputs each character in the string to the stream.

> If you did not have operator overloading, you would have to have different operators for outputting integers, outputting floats, outputting strings, and so on.

Using stream operators to stream from input shows the same differences; the input is treated in a way that is specific to the type you are wanting to read. So, you can use the operator—the stream operator—but it is specialized to the type you need.

> Operator overloading is more than just a clever way to put familiar characters to a new use; it can be a fundamental part of making a class more useful.

In fact, the stream operator can also be used with an integer on the left, where it has a totally different operation from when there is a stream on the left. With integers, the stream operator actually means "shift the bits of the integer left or right a certain number of spaces." While shifts can be used in making really efficient code, that operation has nothing to do with streaming input or output!

```
1 // Program 17_6
2 // Example of shifting bits
3 #include <iostream>
4 using namespace std;
5
6 int main() {
7 int i = 1;
8 int j = i << 3; // Shifting bits spaces left
9 cout << j << endl;
10 }
```

There is a wide variety of operators you can overload. Binary operators take 2 elements per operand. Examples include arithmetic operators, stream operators, comparison operators, and Boolean operators.

```
+ - * / % <<
>> > < <= =
== != &&
& ^ [ ] ->
```

There are also a few unary operators, which take just a single element.

```
+ ++
- ! &
```

All of these operators, and even a few common ones, are those you can overload; you can create your own version of how they should operate for a particular class or combination of classes.

## OVERLOADING BINARY OPERATORS

One way of overloading a binary operator involves defining an operator in a very similar manner to how you define a function.

The result of result is basically the return type of the operator function, which will take exactly 2 parameters: the object type of the first and second operands. The only "different" part is the function name, which will have the keyword operator, followed by the particular operation. And all of this gets just like any other function—not as part of any class.

Whenever a binary operator is used, there are going to be 2 operands: one before the operator and one immediately after. Then, there will be a result of some type. For example, a comparison operator should probably give a Boolean result.

Lecture 17 | Object-Oriented Constructors and Operators

## Program 17.8

```
// Operator * multiplying light
#include<iostream>
using namespace std;

class lightbulb {
public:
    int watts_used;
    int lumens;
    int temperature;

    lightbulb() {
        watts_used = 60;
        lumens = 900;
        temperature = 2700;
    }

    lightbulb operator *(lightbulb bulb, int increase_factor) {
        lightbulb ans;
        ans.watts_used = bulb.watts_used * increase_factor;
        ans.lumens = bulb.lumens * increase_factor;
        ans.temperature = bulb.temperature;
        return ans;
    }


int main() {
    lightbulb bulbba, bulbb;
    cout << bulbba.watts_used << " << " << bulbb.lumens << " << " << bulbb.temperature << endl;
}
```

Suppose you have a class that is using to keep track of lightbulbs. Every bulb will have three pieces of data: the number of watts used, the number of lumens (luminous), and the equivalent color temperature of the bulb.

You can define a class with member variables, as you can see in the code. Notice that all 3 member variables are public in this case and a default constructor is used to set initial values for the 3 values (c).

Let's say you want the ability to create a new bulb that is a factor multiple of an existing bulb. For example, if a bulb is 2 times many watts as another, it would produce 2 times as many lumens but the same color temperature.

Inside the function position, you create a new lightbulb, called ans, for answer, because it will be the answer return from the operator. You set the watts and lumens as the bulb multiplied by increase_factor. The color temperature is the same as bulb. Then, you return ans (d).

In your main routine, you can create 2 bulbs bulbba and bulbb, where both is initialized with the default constructor that it has 600 watts, 900 lumens, and a 2700 color temperature. You set bulb to bulba times 2. This will call the multiplication operator on a lightbulb times integer, so bulbb should have twice the number of watts, or 120, and twice the number of lumens, or 1800, while having the same color temperature, 2700, from bulba. And that's indeed what you see as result.

Let's see how you could define a multiplication operator for the lightbulb. Your operator should take 2 arguments: one lightbulb and an integer that you are multiplying the lightbulb by. And the result is a new lightbulb, one that produces more watts and lumens. So, your operator definition should produce another lightbulb as a result, the definition has a return type

Note that operators are not automatically commutative; in other words, you cannot switch the order of the operands. So, you could not multiply an integer times a lightbulb; if you defined a lightbulb times an integer, but not the other way around.

![](img/bdf1aaea7e08f6cbf15b0a740771ecdc_197_0.png)

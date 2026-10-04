You can pass in arguments that are variables just as easily as other values. In this case, you read in from a user of initial items that the machine should be stocked with. Then, you can declare a vending machine with that number.

Notice that this sort of initialization could not occur if variables were just set to default values by assignment statements in the class declaration.

```
int main() {
    cout << "How many items does the machine start wtiih? " << ";
    int init_number;
    cin >> init_number;
    vending_machine_lobby = init_number;
    cout << "There are " << lobby_machine.number_remaining() << " items." << endl;
}
```

> Be aware that you should not try to declare an object using the default constructor by just using parentheses with no arguments. If you're using the default constructor, just leave off the parentheses entirely. Only use parentheses when you want to use a non-default constructor or when you're declaring the constructor within the class.

# // OPERATOR OVERLOADING

You have already frequently encountered function overloading, where you can use the same function name but take different parameters to get different behavior. **Operator overloading** is similar, but you take different operands to get different behavior from **operator**.

You've already seen examples of operator overloading. Youve see how + can be used for addition for numbers or concatenation for string types. The operator has "overloaded" to take on more than one meaning; it has different meanings depending on the implementation.

When you have the stream operator to output a floating-point number, it behaves one way: It analyzes the number and displays the digits of the number with the decimal point in the correct position. When you use the streaming operator to output a string, it behaves a different way: It analyzes the array of characters kept in the string and outputs each character in the string to the stream.

> If you did not have operator overloading, you would have to have different operators for outputting integers, outputting floats, outputting strings, and so on.
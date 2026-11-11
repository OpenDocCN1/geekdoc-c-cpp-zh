```
```cpp
};

void NumberAddition:: numAccept()
{
    cout<<"Enter any two numbers:";
    cin>>a>>b;
}
int NumberAddition:: add()
{
    return a+b;
}
void NumberAddition:: display()
{
    cout<<"The Addition of two numbers is ="<<add();
}

void main()
{
    NumberAddition na;
    na.numAccept();
    na.display();
}
```
```

# Output:

```
```text
Enter any two numbers:34
89
The Addition of two numbers is =123
```
```

In Listing 4, two random numbers are given as input values and then the program displays their sum. This program has a class, NumberAddition, which has a and b as its private data members; and numAccept(), add(), and display() are defined as its member functions.

The numAccept() function accepts the input values for the variables a and b. The add() function returns the sum of the values stored in the a and b variables. The return type of the add() function is of the int type; and its scope is private in the class NumberAddition. The display() function is used to display the value returned by the add() function as well as a user-defined message. Note that an object cannot invoke a private function of a class; however, the same private member function can be invoked indirectly, through a public member function of the same class.
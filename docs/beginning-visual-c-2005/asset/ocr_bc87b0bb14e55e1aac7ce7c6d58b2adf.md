# Implementing an Overloaded Operator

To implement an overloaded operator for a class, you have to write a special function. Assuming that it is a member of the class CBox, the declaration for the function to overload the > operator within the class definition is as follows:

```
class CBox
{
    public:
        bool operator>(CBox& aBox) const;  // Overloaded 'greater than'
    // Rest of the class definition...
};
```

The word operator here is a keyword. Combined with an operator symbol or name, in this case, >, it defines an operator function. The function name in this case is operator>( ). You can write an operator function with or without a space between the keyword operator and the operator itself, as long as there’s no ambiguity. The ambiguity arises with operators with names rather than symbols such as new or delete. If you were to write operatornew and operatordelete without a space, they are legal names for ordinary functions, so for operator functions with these operators, you must leave a space between the keyword operator and the operator name itself. Note that you declare the operator>( ) function as const because it doesn’t modify the data members of the class.

With the operator>( ) operator function, the right operand of the operator is defined by the function parameter. The left operand is defined implicitly by the pointer this. So, if you have the following if statement:

```
if(box1 > box2)
    cout << endl << "box1 is greater than box2";
```

the expression between the parentheses in the if will call our operator function and is equivalent to this function call:

```
box1.operator>(box2);
```

The correspondence between the CBox objects in the expression and the operator function parameters is illustrated in Figure 8-3.

![](bbox=[0.25, 0.78, 0.8, 0.9])

Figure 8-3
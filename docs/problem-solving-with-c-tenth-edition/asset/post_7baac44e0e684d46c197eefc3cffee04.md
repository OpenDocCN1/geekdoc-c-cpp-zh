
## Copy Constructor

A copy constructor is a constructor that has one call-by-reference parameter that is of the same type as the class. The one parameter must be a call-by-reference parameter. Normally, the parameter is also a constant parameter, that is, preceded by the const parameter modifier. The copy constructor for a class is called automatically whenever a function returns a value of the class type. The copy constructor is also called automatically whenever an argument is "plugged in" for a call-by-value parameter of the class type. A copy constructor can also be used in the same ways as other constructors.

Any class that uses pointers and the new operator should have a copy constructor.

## The Big Three

The copy constructor, the `operator=`, and the destructor are called the big three because experts say that if you need to define any of them, then you need to define all three. If any of these is missing, the compiler will create it, but it may not behave as you want. So it pays to define them yourself. The copy constructor and overloaded `operator=` that the compiler generates for you will work fine if all member variables are of predefined types such as int and double, but they may misbehave on classes that have class or pointer member variables. For any class that uses pointers and the new operator, it is safest to define your own copy constructor, overloaded `=`, and destructor.

= must be a member

## SELF-TEST EXERCISES

- 23. If a class is named MyClass and it has a constructor, what is the constructor named? If MyClass has a destructor, what is the destructor named?

- 24. Suppose you change the definition of the destructor in Display 11.12 to the following. How would the sample dialogue in Display 11.11 change?

```cpp
StringVar::~StringVar()
{
    cout << endl
        << "Good-bye cruel world! The short life of\n"
        << "this dynamic array is about to end.\n";
    delete [] value;
}
```

- 25. The following is the first line of the copy constructor definition for the class `StringVar`. The identifier `StringVar` occurs three times and means something slightly different each time. What does it mean in each of the three cases?

```cpp
StringVar::StringVar(const StringVar& stringObject)
```

- 26. Answer these questions about destructors.
  - a. What is a destructor and what must the name of a destructor be?
  - b. When is a destructor called?
  - c. What does a destructor actually do?
  - d. What should a destructor do?

## Overloading the Assignment Operator

Suppose `string1` and `string2` are declared as follows:

```cpp
StringVar string1(10), string2(20);
```

The class `StringVar` was defined in Displays 11.11 and 11.12. If `string2` has somehow been given a value, then the following assignment statement is defined, but its meaning may not be what you would like it to be:

```cpp
string1 = string2;
```

As usual, this predefined version of the assignment statement copies the value of each of the member variables of `string2` to the corresponding member variables of `string1`, so the value of `string1.maxLength` is changed to be the same as `string2.maxLength` and the value of `string1.value` is changed to be the same as `string2.value`. But this can cause problems with `string1` and probably even cause problems for `string2`.

The member variable `string1.value` contains a pointer, and the assignment statement sets this pointer equal to the same value as `string2.value`. Thus, both `string1.value` and `string2.value` point to the same place in memory. If you change the string value in `string1`, you will therefore also change the string value in `string2`. If you change the string value in `string2`, you will change the string value in `string1`.

In short, the predefined assignment statement does not do what we would like an assignment statement to do with objects of type `StringVar`. Using the predefined version of the assignment operator with the class `StringVar` can only cause problems. The way to fix this is to overload the assignment operator `=` so that it does what we want it to do with objects of the class `StringVar`.

The assignment operator cannot be overloaded in the way we have overloaded other operators, such as `<<` and `+`. When you overload the assignment operator, it must be a member of the class; it cannot be a friend of the class. To add an overloaded version of the assignment operator to the class `StringVar`, the definition of `StringVar` should be changed to the following:

```cpp
class StringVar
{
public:
    void operator =(const StringVar& rightSide);
    //Overloads the assignment operator = to copy a string
    //from one object to another.
    <The rest of the definition of the class can be the same as in
    Display 11.11.>
```

The assignment operator is then used just as you always use the assignment operator. For example, consider the following:

```cpp
string1 = string2;
```

In this call, string1 is the calling object and string2 is the argument to the member operator =.

The definition of the assignment operator can be as follows:

```cpp
//The following is acceptable, but
//we will give a better definition:
void StringVar::operator =(const StringVar& rightSide)
{
    int newLength = strlen(rightSide.value);
    if ((newLength) > maxLength)
        newLength = maxLength;
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```

Notice that the length of the string in the object on the right side of the assignment operator is checked. If it is too long to fit in the object on the left side of the assignment operator (which is the calling object), then only as many characters as will fit are copied to the object receiving the string. But suppose you do not want to lose any characters in the copying process. To fit in all the characters, you can create a new, larger dynamic array for the object on the left-hand side of the assignment operator. You might try to redefine the assignment operator as follows:

```cpp
//This version has a bug:
void StringVar::operator =(const StringVar& rightSide)
{
    delete [] value;
    int newLength = strlen(rightSide.value);
    maxLength = newLength;
    value = new char[maxLength + 1];
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```

Calling object for =

This version has a problem when used in an assignment with the same object on both sides of the assignment operator, like the following:

```cpp
myString = my_string;
```

When this assignment is executed, the first statement executed is

```cpp
delete [] value;
```

But the calling object is myString, so this means

```cpp
delete [] myString.value;
```

So, the string value in myString is deleted and the pointer myString.value is undefined. The assignment operator has corrupted the object myString, and this run of the program is probably ruined.

One way to fix this bug is to first check whether there is sufficient room in the dynamic array member of the object on the left-hand side of the assignment operator and to delete the array only if extra space is needed. Our final definition of the overloaded assignment operator does just such a check:

```cpp
//This is our final version:
void StringVar::operator = (const StringVar& rightSide)
{
    int newLength = strlen(rightSide.value);
    if (newLength > maxLength)
    {
        delete [] value;
        maxLength = newLength;
        value = new char[maxLength + 1];
    }
    for (int i = 0; i < newLength; i++)
        value[i] = rightSide.value[i];
    value[newLength] = '\0';
}
```

For many classes, the obvious definition for overloading the assignment operator does not work correctly when the same object is on both sides of the assignment operator. You should always check this case and be careful to write your definition of the overloaded assignment operator so that it also works in this case.

## SELF-TEST EXERCISE

- 27.
  - a. Explain carefully why no overloaded assignment operator is needed when the only data consists of built-in types.
  - b. Same as part (a) for a copy constructor.
  - c. Same as part (a) for a destructor.

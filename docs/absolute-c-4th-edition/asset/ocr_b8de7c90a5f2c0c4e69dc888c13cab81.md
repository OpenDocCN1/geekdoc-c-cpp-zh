```
```cpp
//Uses istream:
istream& operator >> (istream& inputStream,
                                Percent& aPercent)
{
    char percentSign;
    inputStream >> aPercent.value;
    inputStream >> percentSign; //Discards the % sign.
    return inputStream;
}

//Uses iostream:
ostream& operator <<(ostream& outputStream,
                                const Percent& aPercent)
{
    outputStream << aPercent.value << '%';
    return outputStream;
}
```
```

12. It is legal, but the meaning is not what you might want. (a++) increases the value of the member variables in a by one, but (a++)++ raises the value of the member variables in a++ by one, and a++ is a different object from a. (It is possible to define the increment operator so that (a++)++ will increase the value of the member variables by two but that requires use of the this pointer which is not discussed until Chapter 10.)

# PROGRAMMING PROJECTS

+   1. Modify the definition of the class Money shown in Display 8.5 so that the following are added:
+   
+      a. The operators <, <=, >, and >= have each been overloaded to apply to the type Money. *(Hint: See Self-Test Exercise 8.)*
+   
+      b. The following member function has been added to the class definition. (We show the function declaration as it should appear in the class definition. The definition of the function itself will include the qualifier `Money::`.)

```
```cpp
const Money percent(int percentFigure) const;
//Returns a percentage of the money amount in the calling object.
//For example, if percentFigure is 10, then the value returned is
//10% of the amount of money represented by the calling object.
```
```

For example, if purse is an object of type Money whose value represents the amount $100.10, then the call

```
```cpp
purse.percent(10);
```
```

returns 10% of $100.10; that is, it returns a value of type Money that represents the amount $10.01.
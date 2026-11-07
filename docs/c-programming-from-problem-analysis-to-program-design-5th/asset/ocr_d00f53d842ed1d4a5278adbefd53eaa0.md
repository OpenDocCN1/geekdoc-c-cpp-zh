```
```cpp
cout << "Exiting the try block." << endl;
}
catch (int x)
{
    cout << "Exception: " << x << endl;
    result = 120;
}
catch (string str)
{
    cout << "Exception: " << str << endl;
}

cout << "After the catch block" << endl;
```
```

What is the output if:

+   a. The value of lowerLimit is 50, and the value of divisor is 10?
+   
+   b. The value of lowerLimit is 50, and the value of divisor is 0?
+   
+   c. The value of lowerLimit is 150, and the value of divisor is 10?
+   
+   d. The value of lowerLimit is 150, and the value of divisor is 0?

+   10. If you define your own exception class, what typically is included in that class?

+   11. What type of statement is used to rethrow an exception?

+   12. Define an exception class called tornadoException. The class should have two constructors, including the default constructor. If the exception is thrown with the default constructor, the method what should return "Tornado: Take cover immediately!". The other constructor has a single parameter, say, m, of the int type. If the exception is thrown with this constructor, the method what should return "Tornado: m miles away; and approaching!"

+   13. Write a C++ program to test the class tornadoException specified in Exercise 12.

+   14. Suppose the exception class myException is defined as follows:

```
```cpp
class myException
{
public:
    myException()
    {
        message = "myException thrown!";
        cout << "Immediate attention required!"
             << endl;
    }

    myException(string msg)
    {
        message = msg;
        cout << "Attention required!" << endl;
    }
```
```
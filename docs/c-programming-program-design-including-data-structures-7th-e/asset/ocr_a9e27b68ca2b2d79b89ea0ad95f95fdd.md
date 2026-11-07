What is the output if:

+   a. The value of `lowerLimit` is 50, and the value of `divisor` is 10?
+   
+   b. The value of `lowerLimit` is 50, and the value of `divisor` is 0?
+   
+   c. The value of `lowerLimit` is 150, and the value of `divisor` is 10?
+   
+   d. The value of `lowerLimit` is 150, and the value of `divisor` is 0?

+   16. Which classes are directly derived from the `class exception`? (5)

+   17. Which class is used to deal with illegal arguments used in a function call? (5)

+   18. If you define your own exception class, what is typically included in that class? (6)

+   19. What type of statement is used to rethrow an exception? (7)

+   20. Define an exception class called `tornadoException`. The class should have two constructors, including the default constructor. If the exception is thrown with the default constructor, the method `what` should return "Tornado: Take cover immediately!". The other constructor has a single parameter, say, m, of the `int` type. If the exception is thrown with this constructor, the method `what` should return "Tornado: m miles away; and approaching!" (6, 7)

+   21. Write a C++ program to test the `class tornadoException` specified in Exercise 20. (6, 7)

+   22. Suppose the exception `class myException` is defined as follows: (6, 7)

```
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

    string what()
    {
        return message;
    }

private:
    string message;
}
```
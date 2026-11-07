+   19. What type of statement is used to rethrow an exception? (7)

+   20. Define an exception class called `tornadoException`. The class should have two constructors including the default constructor. If the exception is thrown with the default constructor, the method `what` should return **"Tornado: Take cover immediately!"**. The other constructor has a single parameter, say `m`, of the `int` type. If the exception is thrown with this constructor, the method `what` should return **"Tornado: m miles away; and approaching!"** (6, 7)

+   21. Write a C++ program to test the class `tornadoException` specified in Exercise 20. (6, 7)

+   22. Suppose the exception class `myException` is defined as follows: (6, 7)

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
};
```

Suppose that in a user program, the `catch` block has the following form:

```
catch (myException eM)
{
    cout << eM.what() << endl;
}
```

What output will be produced if the exception is thrown with the default constructor? Also, what output will be produced if the exception is thrown with the constructor with parameters with the following actual parameter?

"May Day, May Day"
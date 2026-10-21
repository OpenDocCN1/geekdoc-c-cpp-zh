# Chapter 9

```
public delegate void UBHandler(ThisClass^, int value);
```

The first argument specifies the type of the this pointer for which a delegate of type UBHandler can call an instance function; the function must have a single parameter of type int and a return type of void. Thus a delegate of type UBHandler can only call a function for an object of type ThisClass but for any object of that type. This may sound a bit restrictive but turns out to be quite useful; you could use the delegate to call a function for each element of type ThisClass^ in an array for example.

You can create a delegate of type UBHandler like this:

```
UBHandler^ ubh = gcnew UBHandler(&ThisClass::Sum);
```

The argument to the constructor is the address of a function in the ThisClass class that has the required parameter list and return type.

Here’s a definition for ThisClass:

```
public ref class ThisClass
{
public:
    void Sum(int n, String^ str)
    { Console::WriteLine(L"Sum result = {0}", value + n); }

    void Product(int n, String^ str)
    { Console::WriteLine(L"Product result = {0}", value*n); }

    ThisClass(double v) : value(v) {}

private:
    double value;
};
```

The Sum() function is a public instance member of the ThisClass class so invoking the ubh delegate will call the Sum() function for any object of this class type.

When you call an unbound delegate, the first argument is the object for which the functions in the invocation list are to be called, and the subsequent arguments are the arguments to those functions. Here’s how you might call the ubh delegate:

```
ThisClass^ obj = gcnew ThisClass(99.0);
ubh(obj, 5);
```

The first argument is a handle to a ThisClass object that you created on the CLR heap by passing the value 99.0 to the class constructor. The second argument to the ubh call is 5, so it results in the Sum() function being called with an argument of 5 for the object referenced by obj.

You can combine unbound delegates using the + operator to create a delegate that calls multiple functions. Of course, all the functions must be compatible with the delegate, so for ubh they must be instance functions in the ThisClass class that have one parameter of type int and a void return type. Here’s an example:

```
ubh += gcnew UBHandler(&ThisClass::Product);
```
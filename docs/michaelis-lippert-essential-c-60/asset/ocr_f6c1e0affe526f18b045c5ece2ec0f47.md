and if the data types for the arguments are not compatible with the parameters, the C# compiler reports an error.

# Declaring a Delegate Type

You just saw how to define a method that uses a delegate, and you learned how to invoke a call to the delegate simply by treating the delegate variable as a method. However, you have yet to learn how to declare a delegate type. To declare a delegate type, you use the delegate keyword and follow it with what looks like a method declaration. The signature of that method is the signature of the method that the delegate can refer to, and the name of the delegate type appears where the name of the method would appear in a method declaration. Listing 12.4 shows how to declare the ComparisonHandler delegate type to require two integers and return a Boolean value.

# LISTING 12.4: Declaring a Delegate Type

```
public delegate bool ComparisonHandler (
    int first, int second);
```

Just as classes can be nested in other classes, so delegates can also be nested in classes. If the delegate declaration appeared within another class, the delegate type would be a nested type, as shown in Listing 12.5.

# LISTING 12.5: Declaring a Nested Delegate Type

```
class DelegateSample
{
    public delegate bool ComparisonHandler (
        int first, int second);
}
```

In this case, the data type would be DelegateSample.ComparisonHandler because it is defined as a nested type within DelegateSample.

# Instantiating a Delegate

In this final step of implementing the BubbleSort() method with a delegate, you will learn how to call the method and pass a delegate instance—specifically, an instance of type ComparisonHandler. To instantiate a delegate, you need a method with parameters and a return type that matches the
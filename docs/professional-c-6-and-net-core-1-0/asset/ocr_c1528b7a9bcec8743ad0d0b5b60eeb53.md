# Multicast Delegates

So far, each of the delegates you have used wraps just one method call. Calling the delegate amounts to calling that method. If you want to call more than one method, you need to make an explicit call through a delegate more than once. However, it is possible for a delegate to wrap more than one method. Such a delegate is known as a multicast delegate. When a multicast delegate is called, it successively calls each method in order. For this to work, the delegate signature should return a void; otherwise, you would only get the result of the last method invoked by the delegate.

With a void return type, you can use the Action<double> delegate (code file MulticastDelegates/Program.cs):

```
class Program
{
    static void Main()
    {
        Action<double> operations = MathOperations.MultiplyByTwo;
        operations += MathOperations.Square;
```

In the earlier example, you wanted to store references to two methods, so you instantiated an array of delegates. Here, you simply add both operations into the same multicast delegate. Multicast delegates recognize the operators + and +=. Alternatively, you can expand the last two lines of the preceding code, as in this snippet:

```
Action<double> operation1 = MathOperations.MultiplyByTwo;
Action<double> operation2 = MathOperations.Square;
Action<double> operations = operation1 + operation2;
```

Multicast delegates also recognize the operators – and -= to remove method calls from the delegate.

> NOTE In terms of what’s going on under the hood, a multicast delegate is a class derived from System.MulticastDelegate, which in turn is derived from System.Delegate.
> System.MulticastDelegate has additional members to allow the chaining of method calls into a list.

To illustrate the use of multicast delegates, the following code recasts the SimpleDelegate example into a new example: MulticastDelegate. Because you now need the delegate to refer to methods that return void, you have to rewrite the methods in the MathOperations class so they display their results instead of returning them (code file MulticastDelegates/MathOperations.cs):

```
class MathOperations
{
    public static void MultiplyByTwo(double value)
```